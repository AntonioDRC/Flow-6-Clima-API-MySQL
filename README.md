# Flow-6-Clima-API-MySQL
Se creo el flow 6 en el cual se realizo la creacion de tablas y graficas asi como el manejo de base de datos en MySQL

# Material necesario
Para poder realizar necesario es necesario tener instalado:

1.- Node.js Usar la versión LTS v16x e instalar los build tools.
2.- Node-Red
3.- Ubuntu 20.04

# Material de referencia
Para hacer las instalaciones requeridas para este ejercicio se siguieron los pasos de los cursos siguientes:

1.- Instalación de Ubuntu 20.04 en VirtualBox Windows
2.- Instalación de NodeRed en Ubuntu 20.04
3.- Introducción a NodeRed

# Instrucciones 
## Instalar MySQUL

1.- Abrir la terminal y escribir el siguiente comando:
	1.1.-sudo apt update

2.- Una vez que se haya ejecutado, escribir el siguiente comando:
	2.1.-sudo apt install mysql-server

3.- Arrancar MySQL Server se usa el siguiente comando 
	3.1.-sudo mysql

## Parte MQTT

1.- Se abre una nueva ventana de la terminal y se escribe el siguiente comando 
	1.1.- node-red

2.- Abrimos el navegador de nuestra preferencia y escribimos lo siguiente 
	2.1.- localhost:1880

3.- Agregar el bloque mqtt in y editar el server colocando local host. Escribir el nombre del tema el cual es: codigoIoT/Mor/mqtt/flow4 (Recordemos que el nombre del tema va a cambiar dependiendo del flow en que estemos).

4.- Agregar un bloque json y en la sección de Action colocar la opción Always convert to JavaScript Object.

5.- Agregar dos bloques function y unirlos a las salida del bloque json. El primer bloque se llamará temperatura y contendrá el siguiente código:
	5.1.- msg.payload = msg.payload.temp;
	5.2.- msg.topic = "Temperatura";
	5.3.- return msg;
		Nota: Para el siguiente bloque se pondra el mismo codigo, solamente se cambiara "Temperatura" por "Humedad" y en vez de "temp" se pondra "hum"

6.- A la salida de cada uno de los bloques de nuestra funcion se insertaran dos bloques de tipo gauge. 
Para configurar cada uno de los bloques gauge se debe crear un grupo para cada variable, en este caso, un grupo para temperatura y otro para la humedad
		Nota: Es importante asignarles la escala y el tamaño adecuados ya que de lo contrario nos puede dar una visualizacion erronea

7.- Para hacer un Histórico que grafique ambos valores en una sola gráfica, se debe insertar un bloque gauge y crear un grupo para este gráfico.

8.- Para mandarle datos a nuestros gauge se tiene que abrir la terminal y escribir le siguiente comenando:
	8.1.-mosquitto_pub -h localhost -t codigoIoT/Mor/mqtt/flow4 -m '{"ID":"NOMBRE","temp":TEMPERATURA,"hum":HUMEDAD}' TEMPERATURA y HUMEDAD son valores numéricos.
		Nota: Se tiene cambiar los espacios que estan en mayusculas con los datos que se obtuvieron de la humedad y temperatura dependiendo del lugar donde estemos 
		
## Parte API

		
