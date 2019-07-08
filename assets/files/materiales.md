---
#layout: post
#title: Materiales
#description: Carro Autónomo
---

# Materiales

Vamos a modificar un carro de control remoto a escala 1/16.
Estos son los materiales que utilizaremos:

### Carro a control remoto
Este es un carro electrico que normalmente se maneja con un control remoto a frecuencia 2.4 GHz. Vamos a remover el chasis de platico con el que viene y los replasaremos con un chasis que acomoda la cámara, raspberry pi, el servo, y una pila para el raspberry pi.
<br>
<img align="center" width="600" src="{{ site.baseurl }}/assets/img/donkeycar/RC-AntesDespues.png"><br>

<br>
<img align="center" width="600" src="{{ site.baseurl }}/assets/img/donkeycar/partes_carro.png"><br>

### Raspberry pi
Minicomputador que usaremos como el sistema del carro. En el raspberry pi vamos a grabar las imgenes de la cámara con los correspondientes datos de acerelación y dirección que tomamos cuando manejamos el carro. Cuando tengamos un modelo entrendo -- nuestro piloto autónomo -- correremos el modelo en el raspberry pi.  
<img align="center" width="500" src="{{ site.baseurl }}/assets/img/donkeycar/raspberrypi.png"><br>

### Controlador de servomotores
El controlador de servomotores es la interface entre el motor y el controlador de circuitos (en este caso el raspberry pi). Su funcionamiento es tomar una señal de control de baja corriente, y convertirla en una señal de alta corriente, que en torno conduce el motor. En nuestro caso esto incluye aceleración y dirección.  

<img align="center" width="400" src="{{ site.baseurl }}/assets/img/donkeycar/servo.jpg"><br>

### Camara
La cámara tomara fotos mientras el carro se maneja.   
<img align="center" width="400" src="{{ site.baseurl }}/assets/img/donkeycar/camara.png"><br>

### Chasis
Vamos a remplazar el chasis del carro por uno donde podamos instalar una cámara y todos los electrónicos que necesitamos.  
<img align="center" width="400" src="{{ site.baseurl }}/assets/img/donkeycar/chasis.png"><br>

### Pila para el raspberry pi
### Pila para el carro

____________________________

# Ensamblaje


1. Quitar el chasis platico del carro y guardar los pins. Desconecta los cables señalados, halando de la parte plastica negra. Con mucho cuidado desliza el cable por la brinda y luego corta la brinda.
<img align="center" width="450" src="{{ site.baseurl }}/assets/img/donkeycar/cables_rm.png"><br>  
2. Para poner el chasis nuevo, tenemos que añadir unos adaptadores de plastico al frente y atras del carro.<br>  
    a. Desatornilla las partes de plastico señaladas en rojo.  
    <img align="center" width="450" src="{{ site.baseurl }}/assets/img/donkeycar/outofbox_frente.png"><br>
    b. Usa los tornillos que conseguiste en el paso previo y pon los adaptadores de platico en la parte de al frente (front) y la parte de atras (back) del carro.  
    c. Para verificar que los adatadores estan en la posicion correcta, intenta poner la parte plana del chasis.  
3. Atornillar el raspberry pi a la parte plana del chasis con los tornillos plateados. Trabaja despacio para evitar apretar los tornillos de mas.    
<img align="center" width="400" src="{{ site.baseurl }}/assets/img/donkeycar/chasis_pi.png"><br>
4. Atornillar servo en su lugar, asegurate que los pins esten alineados en el mismo lado que los pins del raspberry pi. Aca solo necesitamos dos tornillos en diagonal (esquina derecha de arriba y esquina izquierda abajo)<br>
<img align="center" width="350" src="{{ site.baseurl }}/assets/img/donkeycar/chasis_servo_pi.png"><br>  

5. Asegurate que el rapberry pi y el servo esten firmes en su lugar. (verifca con un instructor o monitor)
6. Alinea la jaula del chasis con la parte plana, voltea las dos partes y asegura su posicion con los 3 tornillos negros en el kit.
<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/donkeycar/chasis_jaula_upright.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/donkeycar/chasis_jaula_patasarriba.png" alt="" title="example image"/>
</div>

7. Conecta el raspberry pi con el servo. Mira el diagrama abajo.
<img align="center" width="350" src="{{ site.baseurl }}/assets/img/donkeycar/raspberrypi-servo-connection.png"><br>

8. Instala la camara. _Tengan mucho cuidado con la camara, NUNCA la cogan por el lente._ Sosteniendo la camara por el conector, deslizalo por el espacio disponible en la jaula del chasis. Luego conecta el contacto al raspberry pi-- tines que rotar la cinta de la camara para que los contactos esten alineados con los del raspberry pi.
<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/donkeycar/camara_chasis.png" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/donkeycar/camara_y_pi.jpg" alt="" title="example image"/>
</div>  
9. Ahora pon la plataforma con todos los electronicos en el carro, asegurate que haga click cuando lo pases por las referencias de platico y asegura cada uno con un pin.
10. Pasa los cables que controlan la dirección y accerelación del carro y conectalos al servo.
