# Detector-de-Sintomas-COVID
Este repositorio contiene todo lo necesario para realizar un detector de síntomas COVID con NodeRed, ESP32CAM, el sensor MAX30100, el sensor MLX90614 y MySQL


## Introducción
Este ejercicio consiste en realizar una detector de sintomas COVID.

- Obtiene información de los siguientes sensores con ayuda del ESP32CAM por WiFi.
    - Sensor de oxigenacion y ritmo cardiaco MAX30100
    - Sensor de temperatura infrarrojo MLX90614
- El micro controlador envía la información de los sensores por MQTT de forma local con un mensaje JSON.
- Se cuenta con un Flow en NodeRed que obtiene la información del micro controlador por MQTT y muestra sus valores en un dashboard.
- El dashboard del Flow incluye una sección para que el paciente ponga sus nombre y correo.
- El dashboard cuenta con un boton que toma captura de los datos y realiza un proto diagnostico.
- El flow envía un correo al paciente desde la cuenta configurada.
- El flow mensiona con una voz sintetica el protodiagnostico.


### Importante:

Este flow no realiza un diagnostico médico, su proposito es realizar una consulta de los signos vitales del paciente y comprobar que se encuentren en un rango saludable. Este flow realiza un "proto diagnostico", el cual sugiere al paciente ir con un médico en caso de encontrar algo fuera de lo común.


### Material Necesario

Para realizar este ejercicio necesitarás contar con lo siguiente:

- Micro controlador ESP32CAM
- Convertidor de niveles FTDI
- Cable USB-A a USB-mini
- Jumpers MM
- Protoboard
- Sensor MAX30100
- Sensor MLX90614

### Software necesario

Para poder hacer funcionar este proyecto, es necesario contar con el siguiente software:
- [Ubuntu 20.04](https://releases.ubuntu.com/20.04/)
- [Arduino IDE](https://www.arduino.cc/en/software)
    - [Gestor de tarjetas ESP32](https://github.com/iotechbugs/esp32-arduino/blob/master/docs/arduino-ide/boards_manager.md)
    - [Configuración de la IDE de Arduino para trabajar con el ESP32CAM](https://github.com/iotechbugs/esp32-arduino)
    - [Biblioteca PubSubClient](https://github.com/knolleary/pubsubclient)
- [Mosquitto MQTT Broker](https://mosquitto.org/download/)
    - [Listener en puerto 1883 para 0.0.0.0 y conexiones no autentificadas activadas](https://mosquitto.org/man/mosquitto-conf-5.html)
- [NodeJS](https://nodejs.org/es/)
    - [NPM](https://www.npmjs.com/)
    - [NodeRed](https://nodered.org/docs/getting-started/local)
    - [Nodos Dashboard: node-red-dashboard](https://flows.nodered.org/node/node-red-dashboard)
    - [Nodos MySQL: node-red-node-mysql](https://flows.nodered.org/node/node-red-node-mysql)
    - [Nodos eMail: node-red-node-email](https://flows.nodered.org/node/node-red-node-email)
- [MySQL Server](https://dev.mysql.com/doc/mysql-getting-started/en/)

### Material de referencia

En los siguientes enlaces puedes encontrar cursos en la plataforma de edu.codigoiot.com que te permitirán realiar las configuraciones necesarias

- [Instalación de Virutal Box y Ubuntu 20.04](https://edu.codigoiot.com/course/view.php?id=812)
- [Configuración de Arduino IDE para ESP32CAM](https://edu.codigoiot.com/course/view.php?id=850)
- [Instalación de NodeRed](https://edu.codigoiot.com/course/view.php?id=817)
- [Introducción a NodeRed](https://edu.codigoiot.com/course/view.php?id=278)
- [Instalación de Mosquitto MQTT](https://edu.codigoiot.com/course/view.php?id=818)
- [Instalación de MySQL](https://edu.codigoiot.com/course/view.php?id=294)
- [Medición de indicadores COVID](https://edu.codigoiot.com/course/view.php?id=805)

## Instrucciones

### Requisitos previos
Para realizar este ejercicio necesitas cumplir con los siguientes requisitos previos

1. Tener configurado en entorno de desarrollo. Para esto es necesario contar con la IDE de Arduino configurada para poder cargar programas al ESP32CAM
2. Entorno de NodeJS configurado para trabajar con NodeRed. Deberás tener agregados los nodos Dashboard, nodos MySQL y nodos eMail.
3. Entorno de Mosquitto MQTT configurado. Deberás tener modificado el archivo mosquitto.conf para que acepte conexiones externas y no autentificadas. Deberás tener el firewall de Ubuntu abierto para permitir conexiones en el puerto 1883.

### Instrucciones de preparación de entorno
Para poder configurar tu entorno y realizar este ejercicio, encesitas lo siguiente

1. Realiza el circuito. Las instrucciones se encuentran en el encabezado del código para el ESP32CAM. Deberás cambiar lo siguiente:
    - El tema de publicación y suscripción
    - Nombre de red y contraseña al que deseas conectarte
    - Tiempo de espera entre envío de datos en milisegundos
2. Arrancar NodeRed y cargar el Flow. Deberás modificar lo siquiente:
    - Temas MQTT a reportar. Deberás ajustarlos de acuerdo a tus fines
    - Servidor de correo, nombre de usuario y contraseña de la cuenta desde la que se enviará el correo
    - Idioma de la voz sintética
    - Realizar una lectura de prueba para cambiar el nivel de bias de la lectura de temperatura del sensor MLX90614
3. Energiza el circuito. Asegurate de energizar el circuito realizado y de que este se encuentre en rango de la red de WiFi seleccionada

### Instrucciones de operación

Para observar el funcionamiento de este proyecto, deberás realizar lo siguiente:
- Abrir el Dashboard: generalmente puedes encontrarlo en http://localhost:1880/ui desde la computadora que ejecuta NodeRed.
- Introducir nombre y correo del paciente
- Colocar un dedo sobre el sensor MAX30100 y MLX90614
- Esperar a que se estabilice la lectura del sensor, aproximadamente despupes de 30 segundos
- Presionar el boton "Realizar diagnostico"


# Evidencias
A continuación puedes ver enlaces a las evidencias de este proyecto

- [Repositorio](https://github.com/joseomarojeda/Detector-de-Sintomas-COVID.git)


# Créditos

Desarrollado por Jose Omar Ojeda Aguilar
- (https://github.com/joseomarojeda)
