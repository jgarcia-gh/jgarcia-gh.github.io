---
title: Comunicaciones en red
layout: unit
---
# Conceptos teóricos
Las redes permiten interconectar los ordenadores físicamente con el objetivo de que se puedan comunicar entre ellos. Hoy en día la gran mayoría de aplicaciones hacen uso de estas redes para compartir información (chats, streaming de video, almacenamiento en la nube, etc.). 

Como veremos el proceso de comunicación es complejo pero los lenguajes de programación como Java simplifican mucho esta tarea a los programadores. 
## Elementos que intervienen la comunicación
No podemos hablar de comunicación sin mencionar los elementos que participan en ella:
- Emisor: Agente que genera la información y la transfiere al medio.
- Receptor: Agente que recibe la información a través del medio.
- Mensaje: Información que se transmite.
- Canal o medio: Elemento físico que transmite el mensaje.
- Código: Sistema de señales o signos utilizados para transmitir el mensaje
## Arquitectura cliente/servidor
La arquitectura cliente/servidor es el modelo más utilizado para realizar la comunicación entre dispositivos.

Se trata de un modelo de diseño de software en el que las tareas se reparten entre los proveedores de recursos o servicios, llamados servidores, y los demandantes, llamados clientes.

El **servidor** es el dispositivo que ofrece un servicio como por ejemplo compartir un recurso. Los servidores permanecen a la espera de que un cliente se conecte y les hagan peticiones. Un ejemplo clásico son los servidores web.

Por su parte el **cliente** es el dispositivo que hace uso de los servicios ofrecidos por los servidores. Se conecta a ellos para hacerles peticiones. Un ejemplo son los navegadores de Internet.

![Servidor y cliente web](img/img1.png "Servidor y cliente web")

## Arquitectura de redes
A finales de los años 70 los fabricantes desarrollaban diferentes dispositivos para crear redes privadas. En aquella época no se pensaba en la compatibilidad de hardware y software entre fabricantes por lo que los dispositivos solo funcionaban si se conectaban a otros dispositivos del mismo fabricante.
### Modelo de referencia OSI
En 1983 la Organización Internacional de Estándares ISO (International Organization for Standardization) desarrolla el modelo de Interconexión de Sistemas Abiertos OSI (Open Systems Interconnection) con el que pretende normalizar la comunicación entre dispositivos.

OSI es un modelo conceptual: ofrece los fundamentos de diseño, pero no define sus protocolos.

Estructura el proceso de comunicación en siete niveles o capas que interaccionan entre sí. 

### Modelo TCP/IP

Desde finales de los años 70, esto es varios años antes del desarrollo del modelo OSI, la Agencia de Proyectos de Investigación Avanzados de Defensa  (DARPA) perteneciente al Departamento de Defensa de los Estados Unidos había estado trabajando en la red ARPANET con el objetivo de interconectar diferentes instituciones académicas. ARPANET hacía uso de la arquitectura TCP/IP imponiéndose al modelo OSI.

Si queréis saber más sobre el tema:

[Breve historia de cómo TCP/IP se impuso a OSI Parte 1](https://www.javiergarzas.com/2013/09/tcpip-se-impuso-a-osi-1.html)
[Breve historia de cómo TCP/IP se impuso a OSI Parte 2](https://www.javiergarzas.com/2013/09/tcpip-se-impuso-a-osi-2.html)

### Arquitectura en niveles o capas
Tanto el modelo OSI como la arquitectura TCP/IP se basan en niveles o capas. Cada capa proporciona servicios a la capa contigua superior y utiliza los servicios que le presta la capa contigua inferior. De esta forma el problema de comunicar dos dispositivos se divide en subproblemas más pequeños y por tanto más manejables.

[¿Por qué estructurar la arquitectura en niveles o capas?](res/modelo_niveles.pdf)
## Arquitectura TCP/IP
### Nivel de aplicación
### Nivel de red
### Nivel de transporte
# Comunicaciones en Java
## Direccionamiento
## Sockets
### Sockets no orientados a conexión
### Sockets orientados a conexión

# Bibliografía
https://ioc.xtec.cat/materials/FP/Recursos/fp_dam_m09_/web/fp_dam_m09_htmlindex/WebContent/u2/a1/continguts.html