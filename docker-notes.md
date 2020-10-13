1. construye una imagen con el nombre app

```dockerfile
docker build .

#construir una imagen con nombre
docker build -t node-app .

#contruir una imagen sin usar el cache
docker build -t node-app --no-cache .

#garantiza que docker siempre fue a descargar la imagen base
docker build -t node-app --no-cache --pull .
```

2. construye una imagen desde un docker file remoto

```
docker build github.com/creackd/docker-firefox
```

3. listar imagenes

```
docker images
```

4. ejecuta un contenedor con el o los comandos definidos en el entrypoint, le asigna el nombre app

```dockerfile
docker run --name app nginx

# '-d' ejecutar un proceso en modo background, para que cuando termine devuelva la terminal, de lo contrario docker se queda como dueño de la terminal

# '-p' mapea el puerto 80:8080 (puerto de la compu | puerto del contenedor)

docker run -d -p 80:8080 nombre-imagen

#esto devuelve un id del contendor

#se puede mapear mas de un puerto xD pero hay que ver en la docu

#para ponerle nombre al contenedor
#(nombre del contenedor & nombre de la imagen)
docker run -d -p 80:8080 node-app --name node-app node-app

```

4. ejecuta el comando "echo hola" dentro del contenedor con nombre app, el contenedor debe estar en ejecución

```
docker exec app echo hola
```

5. utiliiza para elimina la imagen nginx deteniendo los contenedores relacionados

```
docker rm nginx -f

#elimina contenedores
docker rm id
```

6. lista todos los contenedores

```
docker ps -a

#lista contenedores con toda la info relevante en ejecucuion
docker ps
```

7. detiene o inicia un contenedor

```
docker stop | start app
```

8. muestra los logs del contenedor de app en ejecución

```
docker log app -f
```



dockerfile->build->image->run->docker contaner

RUN se ejecuta cuando se esta construyendo una imagen, no se invoca la shel sino permite ejecutar programas que este contenga

CMD a diferencia de run, los comandaos de este se ejecutan cuando el contenedor se inicializa, mientras que run se utiliza para crear una imagen





##### Docker multistage

construye una imagen, usando multiples imagenes bases

sirve para aplicaciones compiladas, ejemplo: compilar  y luego ejecutar

```dockerfile
FROM node:14.5.0-alpine3.12 as build
RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app
WORKDIR /home/node/app
COPY app/ ./
USER node
RUN npm install
RUN npm test


FROM node:14.5.0-alpine3.12 as runtime
WORKDIR /home/node/app
COPY --from=build  /home/node/app ./
EXPOSE 8080
CMD ["node", "app"]

```

 

##### Publicar en dockerhub

```
docker login

#renombrar la imagen

docker tag node-app iddockerhub/node-app:v1

docker push iddockerhub/node-app:v1

docker run -d -p 8081:8080 iddockerhub/node-app:v1
```



##### Orquestador de contenedores

Adminstrar un entorno de contenedores

###### Docker compse

Una aplicaciones puede estar creada por varios componentes

Definir el entorno de la aplicacion en un dockerfile -> definir los servicios que componen la aplicacion  en un docker compose file -> ejecutar docker compuse up

```
docker-compose up -d

docker-compose up 

#parar el contenedor y los remueve
docker-compose down 
```

https://docs.docker.com/compose/install/

##### Docker volumnes

Permite persistir la informacion, asi la info no depende del ciclo de vida del contenedor

##### Instalación linux

Installing using repository

https://docs.docker.com/engine/install/ubuntu/

##### docker network modes

1. localhost

2. bridge
3. macvlan



docker-compose permite crear una red, para que los contenedores puedan perse entre si

```
#escalabilidad 'node-app' es el nombre del servicio en el file del docker-compose
docker-compose sacle node-app=3
```

