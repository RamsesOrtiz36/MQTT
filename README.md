# Broker Mosquitto alias MQTT
Borker local, broker publico, temas, suscripción, publicación y node red 

Para la instalación de MQTT en ubuntu usamos la sigueinte instrucción

    sudo apt-add-repository ppa:mosquitto-dev/mosquitto-ppa
	  
    sudo apt-get update
    
    sudo apt install mosquitto
         
Para comprobar que MQTT esta instalado se usa el comadno  

    netstat -an 
      
Debe aparecer una lista de servicios activos y nos interesa el que tenga **escucha en dirección local 1883**.

!(Comprobar MQTT)[Comprobar estado de MQTT.png]

En caso de no aparecer usar el siguiente comando:

    sudo apt install mosquitto-clients
    
Seguir las instrucciones que nos van a ir guiando para la instalación del mismo.
    
## Funcionamiento de mosquitto
Este tipo de servicio permite la transferecnia de datos por mensajes a temas y tomar datoss por mensajes desde los temas. 

La comunicación se realiza en la red local de internet entre los dispositivos que esten conectados a la misma señal de internet o al mismo Modem

+ Primero se crea un tema (epacio donde se envian los mensajes con los datos).
+ Despues se le pide información al tema por medio de una suscripción al tema (bajan datos del tema).

La ventaja de esto es que todo dispositivo con acceso a la red local puede enviar y recibir información. 

## Generar suscripción a un tema de mosquitto

En la computadora que tiene instlado MOSQUITTO podemos crear el tema siguiendo la el sigueinte comando en terminal. Con la subscripcón le decimos que se quede "escuchando" ese puerto y cada vez que reciva información nos la muestra en terminal.
   
    mosquitto_sub -h localhost -p 1883 -q 0 -t CodigoIoT/Ejercicio/MQTT/G7
    
Veamos que significa cada parte del comando:

**Mosquitto_sub** = Indicamos que va ser una subscripción a un tema.

**-h localhost** = Indica la opcion de ocnfiguración de host, en este caso quien hospeda al tema es "localhost".

**-p 1883** = En la red de comunicación usamos el puerto de comunicacion numero 1883 que es el dedicado a la comunicación por MQTT.

**-q 0** = Calidad de comunicación para envio de datos, 0, 1 y 2, 0= Maximo una vez envia mensaje, puede que no lo envia, 1= envia al menos 1 vez o más, 2= envia 
exactamente 1 vez.

**-t CodigoIoT/Ejercicio/MQTT/G7**= indica el nombre del tema se maneja por jerarquia de tema y se usa "/" para indicar otro subnivel, no hay limite y se recomienda usar varios niveles para ser mas especifico del tema y más seguro.

## Publicación en tema de MQTT
Para enviarle datos al tema de MQTT usamos el siguiente comando.

     mosquitto_pub -h localhost -p 1883 -q 0 -t CodigoIoT/Ejercicio/MQTT/G7 -m "Hola mosquitto, este e sun mensaje enviado al tema"
   
Se tiene la opción de -m = indicando el contenido del mensaje que se va enviar entre comillas dobles "".

Para ver la recepción del mensaje se una una terminal y para enviar el mensaje al tema se usa una segunda terminal.

Otra opción es la letra -i = nos sirve la darle un identificador de quien lo envia.

El orden de las letras de opciones no afecta, puede ir -i -h -p -m -t.

## Broker publico en internet
Lo que hemos visto se ha realizado en host   local = localhost= en la red de 1 modem, pero tambien se puede aplicar en internet, usamos la opción de -h para escribir la ip del servidor en internet que guarde el tema.

Hay paginas dedicadas con servideores apra esto por ejemplo el servicio de HiveMQ, en internet se busca la paginade HiveMQ y nos ofrece varios servicios el que es gratuito nos permite crear un tema en "la nube" con acceso a internet para enviar y recibir mensajes usando el protocolo MQTT, para ello usamos la ip de la pagina HiveMQ.
 
 En terminal de nuestra computadora usamos el comando para ver cual ip usa en ese momento la pagina, porque cambia cada cierto tiempo y debemos actualizar la ip a la que nos vamos a conectar.
 
    nslookup broker.hivemq.com





