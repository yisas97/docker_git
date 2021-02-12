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

## Virtualizacion

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

