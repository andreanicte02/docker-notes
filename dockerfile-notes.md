Estructura basica de un docker file



1. define una variable que el usuario puede pasar en tiempo de ejecución es la única instrucción que puede ir antes del from

```
ARG [CLAVE]:[VALOR] (VERSION = latest)
```

2. inicia la construcción de una nueva imagen, especificando la imagen

```
FROM [repositorio/nombre_de_image:etiqueta] (yolix/nodeapp:${version})
```

3. ejecuta cualquier comando dentro del contenedor en construcción 

```
RUN [comandos] (mkdir -p /var/logs/app_logs)
```

4. la función principal de esta instrucción es proveer valores por defecto para un contenedor en ejecución 

```
CMD [[comandos]] (["node", "app.js"])
```

5. agrega meta-data a una imagen, el argumento debe ser llave valor

```
LABEL [llave]:[valor] (version:1.10 equpo:desarrollo)
```

6. notifica a docker que el contender va cuchar el puerto o los puertos especificos en tiempo de ejecucion

```
EXPOSE [puerto] | [puerto/protocolo] (80 | 80/tcp)
```

7. configura variables de enterno dentro de un contenedor, el argumento debe ser llave valor estas variables persisten luego de ser creada la imagen

```
ENV [nombre]:[valor] (app_logs=/var/logs/app_logs)
```

8. instrucción copa nuevos archivos, directorios y archivos remotos desde urls y los agrega al sistema de archivos del contenedor

```
ADD [fuente] [destino] (app/package.json /app | https://foo.com/app.zip /app)
```

9. copia nuevos archivos o directorios y los agrega al sistema de archivos del contenedor

```
COPY [fuente] [destino] (app/package.json /app)
```

10. permite configurar un contenedor ejecutable, normalmente con el procesos que queremos que exponga

```
ENTRYPOING [comandos] (node app.js)
```

11. crea un punto de montaje con el nombre especificado, lo marca para que pueda ser montado externamente 

```
VOLUME [directorio] (/data)
```

13. configura el usuario (o el uid), opcional mente el nombre del grupo o (GID) con el que se ejecuta los comando siguientes especificados en las instrucción: CMD | RUN | ENTRYPOING

```
USER [usuario]: [grupo] (node:node)
```

14. configura el directorio de trabajo, donde se ejecutan los comando especificados en la instrucción CMD | RUN | ENTRYPOINT

```
WORKDIR [directorio] (/tmp)
```

15. agrega a la imagen una instrucción de disparo para ser ejecutada después, cuando la imagen resultante sea utilizada como imagen base.

```
ONBUILD [INSTRUCCION] (ADD . /app/src)
```

16. se usa para configurar la señal de llamada al sistema que enviar al contenedor para salir 

```
STOPSIGNAR [signal] (SIGQUIT)
```

17. indica a docker como testear el contenedor para check si funciona

```
HEALTHCHECK [opciones] [comando] (--interval=m --timeout=3s CMD curl -f http://localhost/ || exit 1)
```

18. permite sobreescirbir el shell predeterminado en linux  es ["/ bin / sh," , "-c"] y en windows es ["cmd","/S", "/C"]

```dockerfile
SHELL ["powershell", "-command"]
```


