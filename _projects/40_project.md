---
layout: page
title: Carro Autónomo
description: CdC Colombia 2019
img: /assets/img/donkeycar/built_sans_camera.jpg
---

# Carro Autónomo — 
### Clubes de Ciencia Cali, Colombia -- julio 2019

En este club vamos a transformar un carro de control remoto y convertirlo en un carro autónomo. Vamos a adquirir la data necesaria para entrenar un modelo que se convertirá en nuestro piloto autónomo. Para esto usaremos la plataforma de [Donkeycar](https://www.donkeycar.com/). Esta plataforma nos permite fácilmente registrar imagenes de la cámara con las correspondientes señales de aceleración y dirección cuando manejamos el carro. El modelo que construyamos va a aprender una correlación entre images y acción (aceleración y dirección). De este modo podemos poder nuestro carro autónomo en la pista y al procesar imagenes, toma una acción de manera independiente.         

*Vamos a aprender sobre:*
- Computación
- El terminal y editores nativos como vi
- Machine Learning e inteligencia artificial
- Los pasos necesarios para entrenar un modelo
- ¡Carros autónomos!


# Parte I  

Antes de tomar data y entrenar el modelo, tenemos que construir el equipo, instalar software en nuestro computador local y el raspberry pi (en efecto, el computador del carro).  

____________________________

## Equipo
Conoce los diferentes [componentes del carro]({% link assets/files/materiales.md %}) y cómo contribuyen al ecosistema de nuestro carro autónomo.


## Instalación de software
Vamos a entrenar modelos en nuestro computador local y adquirir la data en el raspberry pi, así que las dos plataformas deben tener el código de donkeycar.
Sigue las instrucciones [aquí]({% link assets/files/software.md %}).

## La Pista
El carro necesita un ambiente donde entrenar. Entre todos vamos a diseñar y construir una pista donde vamos a entrenar a nuestros pilotos.
<br>

# Parte II

¡Ahora si estamos listos para empezar el proceso de crear nuestro piloto autónomo!  

____________________________

## Calibrar el Carro
Es importante que nuestro piloto (por medio de señales del servo) entienda que es derecha, izquierda, parar, adelante y reversa. De igual manera, tener carros calibrados nos abre la posibilidad de compartir pilotos y/o data para entrenar a un super piloto.    

## Data para el modelo
Vamos a usar la pista para obtener imagenes y data sobre aceleración y dirección.

## Entrenar un modelo
Ya con data podemos entrenar un modelo. Pero ojo, aseguremonos que la data este "limpia" y recuerden reservar una fracción de la data para prueba.  

## Piloto autónomo
¡A Correr el piloto!
