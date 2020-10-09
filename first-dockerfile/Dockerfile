#se indica la imagen (esta es obteneida de docker hub en este caso) y la version
FROM node:14.5.0-alpine3.12
#voy a crear una carpeta, en esta carpeta voy a instalar mis dependenicias
#la carpeta /home/node/app va ser propiedad del usuario node
RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app
#Configurar el directorio "actual" donde voya estar ejecutando las instrucciones sig dentro del contenedor
WORKDIR /home/node/app
#voy a copiar los archivos necesario
#en workdir se indicio cual va ser el dirctorio actual
#lo de la carpeta app se va copiar en en ./ osea el direcotorio que se indicio en el workdir
COPY app/ ./
#usuario que va tomar control en las instrucciones siguientes
USER node
#instalo despendencias
RUN npm install
#indica que se esta ejecutano la app en el puerto 8080, se expone el host
EXPOSE 8080
#define con que comando se ejecute el contenedor cuando se le de un docker ru
CMD ["node","app"]