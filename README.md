# Integración con Apache Camel y RabbitMQ
Nombre: David Teran                                                                                                                       
Materia: Integración de Software                                                                                                          
Fecha: 12 - 06 - 2025

# CAPTURAS DE CONSOLA RABBIT MQ
![image](https://github.com/user-attachments/assets/c7789e8c-4739-4edf-b301-5810f2b9cc49)
![image](https://github.com/user-attachments/assets/46da40ab-0c5d-47ee-9964-2d6242d59d53)

# CAPTURAS DE CONSOLA DE LOG DE CAMEL 
![image](https://github.com/user-attachments/assets/2fd0ce18-2064-490c-ad45-719422d29eab)


# 1. Patrón de integración aplicado
En este taller se aplicó el patrón de integración Producer-Consumer (Productor-Consumidor) mediante el uso de un broker de mensajería, RabbitMQ. Este patrón permite que un componente (el productor) envíe mensajes a una cola sin necesidad de que el receptor (consumidor) esté disponible inmediatamente para procesarlos. RabbitMQ actúa como intermediario, almacenando los mensajes en la cola test.camel.queue hasta que el consumidor esté listo para recibirlos.
Este patrón es fundamental en arquitecturas desacopladas, facilitando la comunicación asincrónica y permitiendo que los sistemas puedan operar con diferentes velocidades y tiempos de respuesta sin bloquearse mutuamente.

# 2. Cómo se logró el desacoplamiento productor-consumidor?
El desacoplamiento entre productor y consumidor se logró usando RabbitMQ como intermediario. El productor, desarrollado con Apache Camel, genera mensajes periódicos y los envía a la cola test.camel.queue sin esperar una respuesta inmediata ni depender del estado del consumidor.
Por su parte, el consumidor, también implementado con Camel, se suscribe a esta cola y procesa los mensajes cuando están disponibles. Esta separación permite que ambos procesos se ejecuten de manera independiente, facilitando la escalabilidad y tolerancia a fallos, ya que la cola actúa como un buffer que asegura la entrega de mensajes incluso si uno de los extremos está temporalmente inactivo.

# 3. Ventajas observadas durante la práctica
Durante el desarrollo de este taller se observaron varias ventajas clave de utilizar un sistema basado en colas con Camel y RabbitMQ:     a) Desacoplamiento claro: Productor y consumidor no dependen de la disponibilidad simultánea, permitiendo mayor flexibilidad en el diseño del sistema.                                                                                                                              
b) Escalabilidad: Se puede aumentar la cantidad de consumidores para procesar mensajes en paralelo sin cambiar el productor.              c) Resiliencia: Si el consumidor está fuera de línea, los mensajes permanecen almacenados en la cola, evitando pérdida de información.    d) Facilidad de monitoreo: RabbitMQ provee una consola administrativa clara para visualizar colas, mensajes y conexiones.                 e) Integración simple con Camel: La configuración de rutas en Camel permite conectar el flujo de mensajes fácilmente con pocas líneas de código.
