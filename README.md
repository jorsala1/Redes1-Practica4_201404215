# Redes1-Practica4_201404215
Práctica 4 Curso Redes de Computadoras 1
#### Jorge Luis Salazar Peralta
#### 201404215

---
## Manual de Configuración

  - ### Configuración de la Topología de la Red
  Para la configuración de la red se utilizó el porgrama GNS3 en el cual se seleccionó los dispositivos necesarios para hacer funcionar la red solicitada en la práctica, el equipo seleccionado fue:
  
    - 1 router
    - 1 maquina virtual
    - 3 etherswitch
    - 2 switch
    - 3 vpc's

Luego de ralizar la conexión de lineas virtuales la topología generada es la siguiente:

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/modelo.PNG)

- Para ingresar al area de configuración tecleamos el comando **configure terminal** para degradar el etherswitch  y quitarle el ruteo al mismo, esto con el comando **no ip routing** para luego crear el dominio de la vlan y en el caso del primer etherswitch configurarlo como el server de la conexión, esto con los comandos:
    - vlan database
    - vtp domain <<nombre_red>>
    - vtp password <<password>>
    - vtp v2-mode

y luego volverlo server con el comando **vtp server** para luego salir de esa configuración:

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/1.PNG)

- En el caso de los otros 2 la coniguración es exactamente la misma, con la diferencia que al final estos se convierten en clientes del primero que fue configurado. Esto con el comando **vtp client**

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/2.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/3.PNG)

- Después de eso procedemos a setear las configuraciones básicas a todos los etherswitch las cuales son la velocidad, el tipo de comunicacion que estas tendran,  y asi mismo al levantamiento de los puertos asociados a esta configuración.
- 
![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/4.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/5.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/6.PNG)

- Luego procedemos a hacer esa configuración en el Router principal de la topología, el cual es habilitar los puertos que se encuentran conectados y colocarle sus valores básicos para el funcionamiento de la red.

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/7.PNG)

- En este punto procedemos a realizar el tipo de acceso el cual para nuestro caso será **Modo Trunk**, el cual se configura de la siguiente manera:


    - configure terminal
    - int range f#/# - # (numeros de puertos a utilizar)
    - switchpor mode trunk
    - exit para salir de la configuracion del puerto
    - exit para salir de la configuracion del terminal
  Este proceco se realiza en los 3 etherswitch.

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/8.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/9.PNG)


![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/10.PNG)


- Ahora se procede a la creación de las vlan's como tal, esto dentro del etherswitch server, de la siguiente manera

  -   vlan database
  -   vlan # name <<nommbre_vlan>>

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/11.PNG)

- luego procedemos a ingresar a los otros etherswitch para realizar la configuración de los port channel, la cual se realiza con los siguientes comandos:

  -   configure terminal
  -   int range f#/# - #
  -   channel-group  # mode on


![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/12.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/13.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/14.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/15.PNG)

- Ahora procedemos a la configuración de los switch normales en la pestaña de configuración de gns3 y colocando los puertos en el acceso que sea necesario de acuerdo al uso que se le dará a cada uno asi como tambien el acceso a la vlan que estara conectado cada puerto tambien, y quedará de la siguiente manera:

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/16.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/17.PNG)


- Luego de eso se procede a configurar las ip a las computadoras que estarán involucradas en el uso de la red generada.

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/18.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/19.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/20.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/21.PNG)


- Procedemos a visualizar el spanning tree para ver la distribucion de la red, esto con el comando **sh spanning-tree brief**

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/23.PNG)

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/24.PNG)

-   Se realiza la prueba de la captura de paquetes con wireshark en un punto en el que hay comunicacion entre los dispositivos que se encuentran compartiendo.

![](https://github.com/jorsala1/Redes1-Practica4_201404215/blob/master/Imagenes/22.PNG)