# Practica 3. Balanceo de carga
Realizada por Elena María Gómez Ríos y Guillermo Sandoval Schmidt.

## Objetivos
- Configurar una máquina e instalar el `nginx` como balanceador de carga.
- Configurar una máquina e instalar el `haproxy` como balanceador de carga.
- Someter a la granja web a una alta carga, generada con la herramienta `Apache Benchmark`, teniendo primero `nginx` y después `haproxy`.

## Instalación y configuración de nginx
<p style="text-align: justify;">
Lo primero que tenemos que hacer es crearnos otra máquina virtual, en nuestro caso M3-B, que no tenga instalado Apache para que no ocupe el puerto 80.
</p>

<p style="text-align: justify;">
Una vez creada configuramos las redes como hicimos en la práctica 1, para que las máquinas se vean entre ellas.
</p>

![](img/1.png)

<p style="text-align: justify;">
Para instalar `nginx` hacemos lo siguiente, cómo se indica en el guión de prácticas:
</p>

```
sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove
sudo apt-get install nginx
sudo systemctl start nginx
```

<p style="text-align: justify;">
Una vez se ha instalado correctamente `nginx` procedemos a su configuración como balanceador de carga.
</p>

<p style="text-align: justify;">
Para ello tenemos que modificar el fichero de configuración `/etc/nginx/conf.d/default.conf`, si existe el fichero tenemos que eliminar el contenido que tenga y si no existe lo creamos con el siguiente contenido:
</p>

![](img/2.png)

<p style="text-align: justify;">
Para asegurarnos de que `ngnix` no funcione como servidor web tenemos que comentar la siguiente línea en el archivo `/etc/nginx/nginx.conf`:
</p>

![](img/3.png)

<p style="text-align: justify;">
Una vez se ha configurado lanzamos el servicio `nginx` con `sudo systemctl start nginx`, si no sale ningún mensaje de error es que todo está correcto y podemos probar el balanceador haciendo peticiones a la IP de esta máquina. Se puede observar como el balanceador reparte el trabajo. En vez de modificar el index.html de cada máquina, hemos modificado el contenido de hola.html y por ello para comprobar el funcionamiento ponemos curl IP/hola.html.
</p>

![](img/4.png)

## Instalación y configuración de HAProxy
<p style="text-align: justify;">
Al igual que hicimos para nginx, creamos una máquina virtual, en este caso M3-B2, que no tenga instalado LAMP y configuramos la red, dándole la misma IP que a la máquina M3-B.
</p>

<p style="text-align: justify;">
Una vez creada la máquina instalamos `HaProxy` con `sudo apt-get install haproxy`.
</p>

<p style="text-align: justify;">
Ahora procedemos a realizar la configuración de HaProxy como balanceador de carga modificando o creando el archivo `/etc/haproxy/haproxy.cfg` con el siguiente contenido:
</p>

![](img/5.png)

<p style="text-align: justify;">
Lanzamos el servicio haproxy mediante el comando `sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg`. Al ejecutar el comando salen 3 warning por utilizar directivas obsoletas, por lo que si no queremos que nos salgan los warnig podemos cambiar el archivo `/etc/haproxy/haproxy.cfg` de la siguiente forma:
</p>

![](img/6.png)

![](img/7.png)

<p style="text-align: justify;">
Ahora probamos que el balanceador funciona correctamente con curl, a igual que hicimos con nginx:
</p>

![](img/8.png)

## Someter a una alta carga el servidor balanceado con ab

### Nginx como servidor balanceado con round-robin
<p style="text-align: justify;">
Ejecutamos `ab -n 1000 -c 10 http://192.168.2.121/hola.html` en nuestra máquina anfitriona y comprobamos como afecta el nivel de peticiones a cada elemento de la granja web con el comando `htop`.
</p>

<img src="img/10.png" width="290"/> <img src="img/11.png" width="290"/>

<img src="img/12.png" width="290"/> <img src="img/13.png" width="290"/>
<img src="img/9.png" width="290"/> <img src="" width="290"/>

<p style="text-align: justify;">
Se puede observar que la CPU del balanceador está prácticamente al 100% mientras que en las máquinas M1 y M2 está al 50% ya que la carga está repartida entre ambas máquinas.
</p>

### Nginx como servidor balanceado con ponderación
<p style="text-align: justify;">
En este caso supondremos que la máquina 1 tiene el doble de capacidad que la máquina 2. Para que nginx funcione con ponderación tenemos que cambiar el archivo de configuración `/etc/nginx/conf.d/default.conf` de la siguiente forma:
</p>

![](img/14.png)

<img src="img/18.png" width="290"/> <img src="img/19.png" width="290"/>

<img src="img/16.png" width="290"/> <img src="img/17.png" width="290"/>
<img src="img/15.png" width="290"/> <img src="" width="290"/>

<p style="text-align: justify;">
En este caso se puede observar como el uso de la CPU de la máquina M1 es mayor que el de la máquina M2.
</p>

### Haproxy como servidor balanceado con round-robin
