---
layout: page
title: Happy Miso
description: a two-sided marketplace
img: /assets/img/miso/scatter.png
---

# Happy Miso — 
## leveraging data for a two-sided marketplace
[Re-post from work circa 2017]

[Miso](https://www.getmiso.com/homeclean) is an on-demand home cleaning service based in South Korea. It allows customers to book next day cleaning services through its easy to use app, and accommodates for one-time bookings or recurring services. Unlike other cleaning platforms in South Korea, customers book a block of time (from 1–8 hrs) and specify what service they want to prioritize (laundry, dishes, general cleaning, etc.). Cleaners will do as much as they can in the allocated time. No subscription fees; no added fees for different types of services. Rather than waiting to be called from a central office, cleaners have the freedom to choose what jobs they want to take. Founded two years ago, this start-up is tapping on an expanding $5 billion industry as the number of dual-income houses increases, in one of the top ranking countries for hours worked per year. Miso, meaning smile in Korean, seeks to make the connection between customer and housekeeping services seamless, putting a smile on both the costumers and cleaners that use the service.

During my data science fellowship at Insight (summer 2017) I worked with Miso as a consultant. Miso is a two-sided marketplace matching customers, who request a housekeeping service, with cleaners, who see available jobs and decide which is right for them. **The problem at hand:** *How to provide better job recommendations to cleaners based on their preferences.*

## The Data
I looked at 5 months worth of booking data from Miso (~ 120,000 bookings) and data from their over 6,000 cleaner pool. The data was stored in a PostgreSQL database, accessible through an open source collaboration platform. Booking information includes residence location, requested job date and time, special precautions (baby, pet, etc.) or requests, availability to public transportation, method of booking, and a flag indicating if the request was successfully matched. Matched bookings have additional information including time stamps of different processes, as well as cleaner information. This includes the cleaner rating, age, years of experience, number of jobs completed to date, and demographic information. The cleaner table has additional information on previously serviced districts and preferred district of service, for each cleaner. After cleaning the data — no two-sided market place for that — and adding engineered features, I had ~90,000 bookings to work with.

## Understanding the Ecosystem

Cleaner behavior is very important in this market place: A job will be requested by a customer, the job specifications are sent to various cleaners, and the cleaners have the choice of accepting or rejecting the job. First I wanted to understand their behavior. I looked at the average number of hours worked per day, as a function of average bookings worked per day, for each cleaner. This would give me a sense on whether most cleaners are optimizing their schedule, assuming they want to work a full-day. In the scatter plot below, the darker, less transparent clusters, indicate more cleaner behavior. The curves plotted on the top and right axis correspond to

<img align="center" width="450" src="{{ site.baseurl }}/assets/img/miso/scatter.png"><br>

the density distribution for the average bookings per day, and average number of hours worked per day, respectively. The shaded orange region in the plot shows the density contours in the data. What is clear from this plot is that most cleaners are working one four-hour job. This could mean most cleaners only want to work part time, or that there are short-comings in the way jobs are recommended to the cleaners. The last is more likely the case, as this is a major source of income for most cleaners.  

I was also interested in seeing the transaction traffic as a function of geospatial location. Because the day of the week intuitively seems like an important variable, I binned transactions per day. Finer resolution was added by explicitly dividing each day into jobs that were scheduled in the morning (first column for each day) and in the afternoon (second column for each day). In the plot below, the size of the circle is proportional to the amount of matched bookings. Though calculated for all districts, this plot only shows data for the top three and bottom three performing districts in Seoul.

<img align="center" width="600" src="{{ site.baseurl }}/assets/img/miso/bubbble_week.png"><br>

From this visualization, really interesting trends start to pop out: for most districts there are less jobs matched in the afternoon than in the morning, and we can see fluctuations in transactions as a function of the day of the week. Digging deeper into the data, I found 36% of all bookings are requested for Mondays and Fridays; a clean home to start the week or to start the weekend. However looking at the percent of jobs matched per day as a function of day of the week (bar plot on the top axis), I find jobs are harder to match on weekends; cleaners are more reluctant to take jobs on weekends. Such is also the case if I include all Seoul districts in the calculation. A similar exercise for each district provides a metric on how well demand is being met for each district. That analysis is shown on the right axis.

## Model Implementation

In order to provide better job recommendations, I develop a model to understand cleaner preferences. I chose to use a random forest model. The random forest model uses an ensemble of decision trees, where the final prediction stems from the average vote of all trees. This type of model can run quickly for large data sets and can give an estimate of what variables are most important based on the votes from the ensemble. One can also extract estimates of the inner tree variability for each input parameter. This model is also great for non-linear classification problems, where there are interaction terms.

The model was trained on 7 input parameters (see below), corresponding to details cleaners would see when a job is recommended to them. The model then predicts if a job is matched. The training data was balanced by randomly under sampling the dominant class (matched transactions in this case; Miso currently matches 80% of their bookings). The data was split 70–30 into training and testing groups. Model validation using the unbalanced test data yielded a model accuracy of 69%. Hoping to improve on that, I implemented a second method for data balancing called SMOTE — Synthetic Minority Over-sampling Technique. This is a hybrid approach where synthetic data is generated for the minority class via a k-nearest neighbor technique. Using this data to train the model led to a higher accuracy of 76%, with an f1 score of 85%. The plot below shows the parameter importance from this model.

<img align="center" width="600" src="{{ site.baseurl }}/assets/img/miso/features1.png"><br>

Top important parameters include the day of the week of the booking, if public transportation is available, and the district where the job is located. This general model can be used to optimize scheduling for flexible customers, or as a metric to set incentives for cleaners for days that are more difficult to book (variable price rates, etc).  

At the start of this problem I was somewhat frustrated because the booking data is rich with cleaner information for matched bookings. Bookings that are not matched, by definition, have no cleaner. This meant I couldn’t use several parameters in the model, that perhaps give more poignant insight on cleaner schedules, effective travel time between jobs, or trends within groups of cleaners (age, experience, rating, etc.). I went back to the data to leverage additional information.  

Having records on the preferred districts to service and districts where services were previously provided by a cleaner, gave me the opportunity to generate two metrics that were associated with cleaner availability for each booking. Essentially this entailed counting the number of cleaners servicing each district for a given day, and normalizing it by the total number of cleaners servicing each district under category 1 (preferred) and category 2 (have worked in the past). The latter two features were added to the previous seven. The same process to train and validate the random forest model as described above was used, with little change to model metrics.  

<img align="center" width="600" src="{{ site.baseurl }}/assets/img/miso/features2.png"><br>

The two new metrics are among the top 5 parameters, with the remaining three matching those of the previous model. This model gives insight to other important interactions such as cleaner scheduling and availability. This model could be used on the back end to manage booking traffic on a per day basis, based on already booked and matched jobs.  

## Closing Remarks
The goal of this project was to find a method to improve job recommendations for cleaners, to ultimately increase the probability of a match. This first approach was a general model that was able to extract dominant parameters that influence the probability of a job request to be matched. The model showed the cleaners have a strong preference for the day of the week the job is requested for and necessities like public transportation. Because cleaner preferences are essential to this problem, future work would include tracking cleaner behavior before a match occurs. This would enable leveraging cleaner data in the model that could account for individual scheduling, time constraints, and trends among groups.  

*Special thanks to Miso and its crew; it was great working with you.*
