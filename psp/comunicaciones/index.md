---
title: Comunicaciones en red
layout: unit
---

# Comunicaciones en red 

- [Introducción](#introducción)
- [Conceptos teóricos](#conceptos-teóricos)
  * [Elementos de la comunicación](#elementos-de-la-comunicación)
  * [Arquitectura cliente/servidor](#arquitectura-cliente-servidor)
  * [Arquitectura de redes](#arquitectura-de-redes)
    + [Modelo de referencia OSI](#modelo-de-referencia-osi)
    + [Arquitectura TCP/IP](#arquitectura-tcp/ip)
    + [Arquitectura en niveles o capas](#arquitectura-en-niveles-o-capas)
  * [Arquitectura TCP/IP](#arquitectura-tcp/ip-1)
    + [Nivel de acceso a la red](#nivel-de-acceso-a-la-red)
    + [Nivel de Internet](#nivel-de-internet)
    + [Nivel de transporte](#nivel-de-transporte)
      - [Protocolo TCP](#protocolo-tcp)
      - [Protocolo UDP](#protocolo-udp)
    + [Nivel de aplicación](#nivel-de-aplicación)

## Introducción

Una red de computadoras u ordenadores es un conjunto de dispositivos interconectados físicamente entre ellos con el fin de compartir información y recursos. Todos tenemos en casa un red privada que interconecta los diferentes dipositivos (móviles, ordenadores, televisión, etc.) ya sea de forma alámbrica y/o inalámbrica. El término Internet hace referencia a al conjunto de redes interconectadas entre ellas a nivel mundial.

Hoy en día la gran mayoría de aplicaciones hacen uso Internet para compartir información (chats, streaming de video, almacenamiento en la nube, etc.). 

El proceso de comunicación entre dos aplicaciones que se ejecutan en diferentes máquinas es complejo ya que involucra una gran cantidad de protocolos y dispositivos. No obstante veremos que los lenguajes de programación como Java simplifican mucho esta tarea a los programadores.

## Conceptos teóricos

En este apartado estudiaremos los principales conceptos relacionados con las comunicaciones en red como es el modelo de referencia OSI y la arquitectura TCP/IP.

En este apartado no se pretende realizar un estudio detallado del funcionamiento de las redes y sus protocolos ya que este artículo trata sobre las comunicaciones en red en Java. No obstante considero importante tener asentados una serie de conocimientos generales antes de empezar a teclear código.

### Elementos de la comunicación

Los elementos que participan toda comunicación son:
- **Emisor**: Agente que genera la información y la transfiere al medio.
- **Receptor**: Agente que recibe la información a través del medio.
- **Mensaje**: Información que se transmite.
- **Canal o medio**: Elemento físico que transmite el mensaje.
- **Código**: Sistema de señales o signos utilizados para transmitir el mensaje

### Arquitectura cliente/servidor

La **arquitectura cliente/servidor** es el modelo más utilizado para realizar la comunicación entre dispositivos.

Se trata de un modelo de diseño de software en el que las tareas se reparten entre los proveedores de recursos o servicios, llamados servidores, y los demandantes, llamados clientes.

El **servidor** es el dispositivo que ofrece un servicio como por ejemplo compartir un recurso. Los servidores permanecen a la espera de que un cliente se conecte y les hagan peticiones. Un ejemplo clásico son los servidores web.

Por su parte el **cliente** es el dispositivo que hace uso de los servicios ofrecidos por los servidores. Se conecta a ellos para hacerles peticiones. Un ejemplo son los navegadores de Internet.

<div style="text-align: center">
<img src="./img/img1.png" alt="Servidor y cliente web" min-width=200px width="70%">
</div>

### Arquitectura de redes

A finales de los años 70 los fabricantes desarrollaban diferentes dispositivos para crear redes privadas. En aquella época no se pensaba en la compatibilidad de hardware y software entre fabricantes por lo que los dispositivos solo funcionaban si se conectaban a otros dispositivos del mismo fabricante.

#### Modelo de referencia OSI

En 1983 la Organización Internacional de Estándares ISO (International Organization for Standardization) desarrolla el modelo de Interconexión de Sistemas Abiertos **OSI (Open Systems Interconnection)** con el que pretendían normalizar la comunicación entre dispositivos.

OSI es un modelo conceptual, esto quiere decir que ofrece los fundamentos de diseño, pero no define sus protocolos. Estructura el proceso de comunicación en siete niveles o capas que interaccionan entre sí. 

> Un **protocolo** es un sistema de reglas que permiten que dos o más dispositivos se comuniquen entre ellos.

#### Arquitectura TCP/IP

Desde finales de los años 70, esto es varios años antes del desarrollo del modelo OSI, la Agencia de Proyectos de Investigación Avanzados de Defensa  (DARPA) perteneciente al Departamento de Defensa de los Estados Unidos había estado trabajando en la red ARPANET con el objetivo de interconectar diferentes instituciones académicas de Estados Unidos. ARPANET hacía uso de una arquitectura de protocolos denominada **arquitectura TCP/IP** que acabó imponiéndose al modelo OSI.

> [Breve historia de cómo TCP/IP se impuso a OSI (Parte 1)](https://www.javiergarzas.com/2013/09/tcpip-se-impuso-a-osi-1.html)
>
> [Breve historia de cómo TCP/IP se impuso a OSI (Parte 2)](https://www.javiergarzas.com/2013/09/tcpip-se-impuso-a-osi-2.html)

#### Arquitectura en niveles o capas

Tanto el modelo OSI como la arquitectura TCP/IP se basan en niveles o capas. Cada capa proporciona servicios a la capa contigua superior y utiliza los servicios que le presta la capa contigua inferior. De esta forma el problema de comunicar dos dispositivos se divide en subproblemas más pequeños y por tanto más manejables.

> [¿Por qué estructurar la arquitectura en niveles o capas?](./res/modelo_niveles.pdf)

### Arquitectura TCP/IP

La arquitectura TCP/IP está compuesta por cuatro niveles: aplicación, transporte, Internet y acceso a la red.

Al enviar datos cada nivel añade una serie de cabeceras a los datos. Dicha cabecera incluye información relevante para los protocolos del propio nivel. Al recibir los datos estas cabeceras se van quitando.

<div style="text-align: center">
<img src="./img/img2.gif" alt="Cabeceras de los datos" min-width=200px width="70%">
</div>

#### Nivel de acceso a la red

La principal función de este nivel es transformar la información recibida del nivel superior (nivel de Internet) en señales que puedan ser transmitidas a través del medio físico. También se encarga del proceso inverso, es decir, a partir de las señales recibidas reconstruir la información original y transferirla al nivel de Internet.

Este nivel permite la comunicación entre dos máquinas que estén conectadas directamente. Hoy en día esta conexión generalmente se realiza a través de un switch. Es en este nivel en el que se implementa el direccionamiento físico mediante el uso de direcciones MAC. En las cabeceras de las tramas de este nivel se incluye la dirección MAC de origen y destino.

#### Nivel de Internet

El nivel de Internet permite el envío de datos desde un dispositivo origen a un dispositivo destino a través de diferentes redes interconectadas por routers o encaminadores. El principal protocolo de este nivel es el **protocolo IP** que se caracteriza por:

- Ser un protocolo no orientado a conexión, esto significa que los datos se transmiten sin necesidad de anunciar previamente que se van a enviar o requerir que se acepte la conexión.
- La entrega de datos es no confiable, nada asegura que vayan a llegar.
- Solo proporciona mecanismos de detección de errores en sus cabeceras, no asegura que los datos del cuerpo del mensaje vayan a llegar bien.
- Hace uso de las direcciones IP para identificar las interfaces (dispositivos que se pueden comunicar).
- Mediante mecanismos de enrutamiento se decide el camino que deben seguir los paquetes para llegar a su destino.

La direcciones IP están compuestas por 32 bits que permiten identificar de forma única una interfaz de red. Las cabeceras de los datagramas IP incluyen la dirección IP de origen y las direcciones IP de destino.

#### Nivel de transporte

Mientras que el nivel de Internet permite que un datagrama llegue desde un dispositivo origen a otro que puede estar al otro lado del mundo, el nivel de transporte se encarga de entregar la información a la aplicación correspondiente. De esta forma un mismo ordenador puede tener múltiples aplicaciones enviando y recibiendo datos desde/a diferentes fuentes/destinos. Pero, ¿Cómo puede saber la capa de transporte a qué aplicación debe entregar los datos?

El proceso de decidir a qué aplicación entregar los datos recibe el nombre de demultiplexación. Para llevarlo a cabo se hace uso de los puertos, números que permiten identificar el origen/destino entre aplicaciones.

El puerto de origen y destino es uno de los datos que se incluyen en la cabecera del segmento. Se utilizan 16 bits para el puerto de origen y otros 16 para el puerto de destino. Por tanto existen 65536 puertos, que van del 0 al 65535. Los puertos inferiores al 1024 son los puertos bien conocidos y están reservados para el sistema operativo y usados por "protocolos bien conocidos". Por ejemplo, el puerto 21 es utilizado por los servidores FTP y el 80 por los servidores web.

Los protocolos de este nivel son **TCP (Transmission Control Protocol)** y **UDP (User Datagram Protocol)**.

##### Protocolo TCP

Este nivel se encarga de que los paquetes lleguen en secuencia y sin errores desde la aplicación de origen hasta la aplicación de destino. Las principales características del protocolo son:
- Es un protocolo orientado a la conexión.
- Demultiplexa los datos.
- Asegura el orden de los segmentos  y que los datos llegan a su destino.
- Asegura que llegan sin errores. 
- Evita la saturación de la red (control de flujo).

##### Protocolo UDP

Las principales características del protocolo son:
- Es un protocolo no orientado a la conexión.
- Demultiplexa los datos.
- No asegura que los datos lleguen a su destino.
- No asegura que lleguen sin errores. 
- No lleva a cabo control de flujo.

#### Nivel de aplicación

Este es el nivel más alto y en él encontramos los protocolos que  utilizan las aplicaciones para comunicarse entre ellas. Algunos de estos protocolos son HTTP, FTP, IMAP, SMTP o DNS.

> El navegador web utiliza un protocolo de la capa o nivel de aplicación llamado HTTP.

A continuación, se muestra un ejemplo de mensaje HTTP que podría enviar un servidor web a un cliente como respuesta a una petición.

```
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2009 12:28:53 GMT
Server: Apache/2.2.14 (Win32)
Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
Content-Length: 88
Content-Type: text/html
<html>
<body>
<h1>Hello, World!</h1>
</body>
</html>
```

Este mensaje se compone de una cabecera:

```
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2009 12:28:53 GMT
Server: Apache/2.2.14 (Win32)
Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
Content-Length: 88
Content-Type: text/html
```

Que incluye información relativa a la fecha y hora en la que se envió el mensaje, la longitud del cuerpo del mensaje y su tipo, etc.

Por otro lado tenemos el cuerpo:

```
<html>
<body>
<h1>Hello, World!</h1>
</body>
</html>
```
Que incluye el contenido del mensaje, en este caso un documento HTML.