# docker_git
Clases de Docker

## Primera Clase:

"Docker te permite construir, distribuir y ejercutar cualqueir aplicacion en cualquier lado".

PROBLEMATICAS DEL DESARROLLO DE SOFTWARE:


1.- Construir:  Escribir código en la máquina del desarrollador. (Compile, que no compile, arreglar el bug, compartir código, etc. )

```
Problematica:

- Entorno de desarrollo (paquetes)
- Dependencias (Frameworks, bibliotecas)
- Versiones de entornos de ejecución (runtime, versión Node)
- Equivalencia de entornos de desarrollo (compartir el código)
- Equivalencia con entornos productivos (pasar a producción)
- Servicios externos (integración con otros servicios ejem: base de datos)
```


2. Distribuir - Llevar la aplicación donde se va a desplegar (Transformarse en un artefacto)
```
Problemática:

- Output de build heterogeo (múltiples compilaciones)
- Acceso a servidores productivos (No tenemos acceso al servidor)
- Ejecución nativa vs virtualizada
- Entornos Serverless
```
3. Ejecutar - Implementar la solución en el ambiente de producción (Subir a producción)
El reto Hacer que funcione como debería funcionar
```
Problemática:

- Dependencia de aplicación (paquetes, runtime)
- Compatibilidad con el entorno productivo (sistema operativo poco amigable con la solución)
- Disponibilidad de servicios externos (Acceso a los servicios externos)
- Recursos de hardware (Capacidad de ejecución - Menos memoria, procesador más debil)
```

## Segunda Clase

### Virtualizacion

### Maquinas Virtuales(Virtual Machines)

Una maquina virtual nos permite tener varios ordenadores virtuales ejecutandoes sobre el mismo ordenador fisico. En informatica, la virtualizacion es la creacion a travez de software de una version virtual de algun recurso tecnologico, como puede ser una plataforma de hardware, un sistema operativo un dispositivo de almacenamiento o cualquier otro recurso de red.En los ámbitos de habla inglesa, este término se suele conocer por el numerónimo “v12n”.


### Problemas de la virtualizacion:

```
- PESO: En el orden de los GBs. Repiten archivos en común. Inicio lento.
- COSTO DE ADMINISTRACION: Necesita mantenimiento igual que cualquier otra computadora.
- MULTIPLES DE FORMATO: VDI, VMDK, VHD, raw, etc
```
### Container:

El empleo de contenedores para construir y desplegar software.
```
- Flexibles
- Livianos
- Portables
- Bajo acoplamiento
- Escalables
- Seguros
```
### Virtualizacion vs Containerización

```
- Virtualización: A diferencia de un contenedor, las máquinas virtuales ejecutan un sistema operativo completo, incluido su propio kernel.

- Containerización: Un contenedor es un silo aislado y ligero para ejecutar una aplicación en el sistema operativo host. Los contenedores 
se basan en el kernel del sistema operativo host (que puede considerarse la fontanería del sistema operativo), y solo puede contener aplicaciones 
y algunas API ligeras del sistema operativo y servicios que se ejecutan en modo de usuario.
```


## 3ra Clase

### Que es y como funciona Docker

![alt tag](https://ualmtorres.github.io/SeminarioDockerPresentacion/images/DockerEngine.png)

## 4ta clase

Comandos iniciales: 
```
$ docker run hello-world (corro el contenedor hello-world)
$ docker ps (muestra los contenedores activos)
$ docker ps -a (muestra todos los contenedores)
$ docker inspect <containe ID> (muestra el detalle completo de un contenedor)
$ docker inspect <name> (igual que el anterior pero invocado con el nombre)
$ docker run –-name hello-jesus hello-world (le asigno un nombre custom “hello-jesus”)
$ docker rename hello-jesus hola-platzy (cambio el nombre de hello-platzi a hola-jesus)
$ docker rm <ID o nombre> (borro un contenedor)
$ docker container prune (borro todos lo contenedores que esten parados)
```
## 5ta Clase

### Ciclo de Vidad de un contenedor

Cuando tu corres un contenedor, solo corre un proceso del Sistema Operativo en el cual seria el proceso principal. 

#### Main Proceso
```
Determina la vida del contenedor, un contenedor corre siempre y cuando su proceso este corriendo
```
#### Sub process
```
Un contenedor puede tener o lanzar procesos alternos al main process, si estos fallan el contenedor va a seguir encedido a menos que falle el main.
```

#### Example:
```
- Batch como Main process
- Agujero negro (/dev/null) como Main process
```
```
docker run --name alwaysup -d ubuntu tail -f /dev/null 

Esto regresa el ID del contenedor
```
Te puedes conectar al contenedor y hacer cosas dentro del él con el siguiente comando (sub proceso)

```
docker exec -it alwaysup bash
```
Se puede matar un Main process desde afuera del contenedor, esto se logra conociendo el id del proceso principal del contenedor que se tiene en la maquina. Para saberlo se ejecuta los siguientes comandos:

```
docker inspect --format '{{.State.Pid}}' alwaysup
```
_El output del comando es el process ID (2474) _

Para matar el proceso principal del contenedor desde afuera se ejecuta el siguiente comando (solo funciona en linux
```
Kill  2474
```
En caso de que no te permita
```
docker kill alwaysup
```
En caso de debian
``` 
sudo kill -9 "$(sudo docker inspect --format '{{.State.Pid}}' alwaysup)"``
```

## Clase 6
### Revisar los contenedores

Cada contenedor tiene su propio stack en el networking, su propia interfaz de red virtual. Necesitamos exponer el contenedor: docker run -d --name proxy -p 8080:80 nginx(8080 de mi máquina fisica y 80 del contenedor que quiero exponer)

``` 
$ docker run -d --name proxy nginx (corro un nginx)
$ docker stop proxy (apaga el contenedor)
$ docker rm proxy (borro el contenedor)
$ docker rm -f <contenedor> (lo para y lo borra)
$ docker run -d --name proxy -p 8080:80 nginx (corro un nginx y expongo el puerto 80 del contenedor en el puerto 8080 de mi máquina)
localhost:8080 (desde mi navegador compruebo que funcione)
$ docker logs proxy (veo los logs)
$ docker logs -f proxy (hago un follow del log)
$ docker logs --tail 10 -f proxy (veo y sigo solo las 10 últimas entradas del log)

```
## Clase 7

### Bind Mounts

Tener acceso a mis carpetas dentro de un proceso de Docker.

Comandos:

``` 
$ mkdir dockerdata (creo un directorio en mi máquina)
$ docker run -d --name db mongo
$ docker ps (veo los contenedores activos)
$ docker exec -it db bash (entro al bash del contenedor)
$ mongo (me conecto a la BBDD)

shows dbs (listo las BBDD)
use prueba ( creo la BBDD prueba)
db.users.insert({“nombre”:“jesus”}) (inserto un nuevo dato)
db.users.find() (veo el dato que cargué)
$ docker run -d --name db -v <path de mi maquina>:<path dentro del contenedor(/data/db mongo)> (corro un contenedor de mongo y creo un bind mount)
```
_Problemas con Windows 10_
Si corres en windows tendras algunos problemas.
Por ejemplo:
```
docker run -d --name db -v /mnt/d/dockerprueba/mongodata:/data/db mongo
```
Con ese comando el contenedor no se mantiene ejecutando, entonces se finalizaba
Para buscar el error se hace lo siguiente, ejecutar el comando:
```
docker logs db
```
Sale un texto largo, que al final es el contexto el error, en resumen dice que no tienes permiso

### _Soluciones_
1.- Se debe crear un volumen en docker con el siguiente comando:

```
docker volume create --name mongodata

```
Lo siguiente con los comandos que se dan, se reemplaza la ruta local que obtienes con el pwd por el nombre del volumen que has creado.
```
docker run -d --name db --v mongodata:/data/db mongo

```
2.- Es cambiar la ruta en la que te encuentras

Hacer un cambio de ruta en la linea de comando de la siguiente manera:

```
cd ~

```
Este comando nos lleva al home (~) de la distribucion (de esta afirmación no estoy del todo seguro)

Luego en esa ruta creas la carpeta para hacer las pruebas de la clase
```
mkdir mongodata

```
Finalmente, introducirías el comando para ejecutar poniendo la ruta local de la siguiente manera:
```
docker run -d --name db --v ~/mongodata:/data/db mongo
```




