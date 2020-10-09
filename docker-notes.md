#define una variable que el usuario puede pasar en tiempo de ejecucion
#es la unica instruccion que puede ir antes del from

ARG [CLAVE]:[VALOR] (VERSION = latest)

#inicia la construccion de una nueva imagen, especificando la imagen
FROM [repositorio/nombre_de_image:etiqueta] (yolix/nodeapp:${version})

#ejecuta cualquier comando dentro del contenedor en construccion 
RUN [comandos] (mkdir -p /var/logs/app_logs)

#la funcion principal de esta instruccion es proveer valores por defecto para un contenedor en ejecucion 
CMD [[comandos]] (["node", "app.js"])

#agrega meta-data a una imagen, el argumento debe ser llave valor
LABEL [llave]:[valor] (version:1.10 equpo:desarrollo)

#notifica a docker que el contender va cuchar el puerto o los puertos especificos en tiempo de ejecucion
EXPOSE [puerto] | [puerto/protocolo] (80 | 80/tcp)

#configura variables de enterno dentro de un contenedor, el argumento debe ser llave valor
#estas variables persisten luego de ser creada la imagen
ENV [nombre]:[valor] (app_logs=/var/logs/app_logs)

#instruccion copa nuevos archivos, direcotorios y archivos remotos desde URLs y los agrega al sistema de archivos del contenedor
ADD [fuente] [destino] (app/package.json /app | https://foo.com/app.zip /app)

#copia nuevos archivos o directorios y los agrega al sistema de archivos del contenedor
COPY [fuente] [destino] (app/package.json /app)

#permite configurar un contenedor ejecutable, normalmente con el procesos que queremos que exponga
ENTRYPOING [comandos] (node app.js)

#crea un punto de montaje con el nombre especificado, lo marca para que pueda ser montado externamente 
VOLUME [directorio] (/data)


#configura el usuario (o el uid), opcionalmente el nombre del grupo o (GID) con el que se ejecuta los comandos siguientes 
#especificados en las instruccion: CMD | RUN | ENTRYPOING
USER [usuario]: [grupo] (node:node)

#configura el directorio de trabajo, donde se ejecutan los comandos especificados en la instruccion CMD | RUN | ENTRYPOINT
WORKDIR [directorio] (/tmp)


#agrega a la imagen una instruccion de disparo para ser ejecutada despues, cuando la imagen resultante sea utilizada como imagen base.

ONBUILD [INSTRUCCION] (ADD . /app/src)

#se usa para configurar la señal de llamada al sistema que enviar al contenedor para salir 

STOPSIGNAR [signal] (SIGQUIT)

#indica a docker como testear el contenedor para check si funciona

HEALTHCHECK [opciones] [comando] (--interval=m --timeout=3s CMD curl -f http://localhost/ || exit 1)

#permite sobreescirbir el shell predeterminado en linux  es ["/ bin / sh," , "-c"] y en windows es ["cmd","/S", "/C"]

SHELL ["powershell", "-command"]
