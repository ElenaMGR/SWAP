# Tema 1. Introducción

## Ejercicio 1
#### Buscar información sobre las tareas o servicios web para los que se usan más los programas que comentamos al principio de la sesión:

- **Apache:** es usado principalmente para enviar páginas web estáticas y dinámicas en internet. Muchas aplicaciones web están diseñadas asumiendo como ambiente de implantación a Apache, o que utilizarán características propias de este servidor web.
- **Nginx:** originalmente, Nginx fue desarrollado para satisfacer las necesidades de varios sitios web que recibían muchas peticiones al día. También puede usarse como balanceador de carga y como proxy. Es un servidor web completo orientado a grandes volúmenes de peticiones (más de 10.000 conexiones simultáneas).
- **thttpd:** es un servidor web de código libre disponible para la mayoría de las variantes de Unix. Se caracteriza por ser simple, pequeño, portátil, rápido, y seguro, ya que utiliza los requerimientos mínimos de un servidor HTTP. Esto lo hace ideal para servir grandes volúmenes de información estática.
- **Cherokee:** es un servidor web multiplataforma, de software libre.​ Su objetivo es ser rápido y completamente funcional, sin dejar de ser liviano comparado con otros servidores web. Puede usarse como un sistema embebido.
- **node.js:** es un entorno en tiempo de ejecución multiplataforma, de código abierto, para la capa del servidor. Concebido como un entorno de ejecución de JavaScript orientado a eventos asíncronos, Node está diseñado para construir aplicaciones en red escalables

# Tema 2. Alta disponibiliad y escalabilidad

## Ejercicio 1
#### Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema).
A<sub>s</sub> = A<sub>c-1</sub> + (1 - A<sub>cn-1</sub>) * A<sub>cn</sub>

| Componentes | Disponibilidad (%) | Disponibilidad 2 (%) | Disponibilidad 3 (%) |
|-------------|--------------------|----------------------|----------------------|
|     Web     |         85         |         97,75        |        99,662        |
| Application |         90         |          99          |         99,9         |
|   Database  |        99,9        |        99,9999       |      99,9999999      |
|     DNS     |         98         |         99,96        |        99,999        |
|   Firewall  |         85         |         97,75        |        99,662        |
|    Switch   |         99         |         99,99        |        99,9999       |
| Data Center |        99,99       |         99,99        |         99,99        |
|     ISP     |         95         |         99,75        |        99,9875       |

Total = 99,214%

## Ejercicio 2
#### Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad.
- **PM2:** es un gestor de procesos que se usa en producción para las aplicaciones Node.js que tiene un balanceador de carga incorporado.
- **Angular:** es un framework de JavaScript de código abierto, mantenido por Google, que se utiliza para crear y mantener aplicaciones web de una sola página.
- **Bootstrap:** es una biblioteca multiplataforma o conjunto de herramientas de código abierto para diseño de sitios y aplicaciones web. A diferencia de muchos frameworks web, solo se ocupa del desarrollo front-end.
- **JQuery:** biblioteca de JavaScript para ayudar en el manejo de documentos HTML, manejo de eventos, animación e interacciones Ajax para el desarrollo web rápido.

## Ejercicio 3
#### ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor?
- **Top:** Sirve para conocer en tiempo real la actividad del procesador, así como una lista con los procesos que hacen un mayor uso de la CPU.
- **Gnome-System-Monitor:** es una aplicación (no instalada previamente) que permite monitorizar tanto los procesos como los sistemas de memoria y red.
- **Munin:** es un sistema de monitorización de código libre, que permite monitorizar la infraestructura y la red, y avisa de cualquier cambio o problema. Presenta además toda la información en gráficos a través de una interfaz web.
- **Nagios:** es un sistema de monitorización de código libre, que permite monitorizar servicios de red y recursos de sistemas hardware.
- **Ganglia:** permite monitorizar sistemas de cómputo distribuidos y permite una gran escalabilidad.
- **Zabbix:** es también de código libre y permite monitorizar el sistema.
- **Awstats:** es un monitor específico de servidores web.

## Ejercicio 4
#### Buscar ejemplos de balanceadores software y hardware (productos comerciales). Buscar productos comerciales para servidores de aplicaciones. Buscar productos comerciales para servidores de almacenamiento.
HaProxy y Nginx son balanceadores de carga por software que hemos utilizado en las prácticas de la asignatura. Algunos balanceadores mediante hardware son Cisco Load Balancer y Kemp Technologies.

# Tema 3. La red de una granja web

## Ejercicio 1
#### Buscar con qué órdenes de terminal o herramientas podemos configurar bajo Windows y bajo Linux el enrutamiento del tráfico de un servidor para pasar el tráfico desde una subred a otra.
En Linux se puede utilizar el comando iptables que permite interceptar y manipular paquetes de red.

Tanto en Linux como en Windows está el comando route, que permite manipular las tablas de enrutamiento, con distinta sintaxis según el sistema operativo:

Windows:
 ```
 route ADD [destino] MASK [mascara] [gateway] [metrica]
 ```
Linux:
 ```
 route add -net [destino] netmask [mascara] gw [gateway]
 ```

 ## Ejercicio 2
 #### Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.

Como ya se ha dicho en el ejercicio anterior en Linux podemos utilizar el comando iptables, que permite filtrar y bloquear paquetes tanto por dirección IP como por número de puerto o incluso por dirección MAC.

En Windows tenemos la herramienta IPsec, que permite filtar por IP y por número de puerto.
