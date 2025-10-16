## Esquema para el ejercicio
![Imagen](esquema-4-ejercicio.PNG)

### Crear la red
```
docker network create net-wp -d bridge
```

### Crear el contenedor mysql a partir de la imagen mysql:8, configurar las variables de entorno necesarias
```
docker run -d --name mysql-service --network net-wp -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=wppass mysql:8
```

### Crear el contenedor wordpress a partir de la imagen: wordpress, configurar las variables de entorno necesarias
```
docker run -d --name wordpress --network net-wp -e WORDPRESS_DB_HOST=mysql-service:3306 -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=wppass -e WORDPRESS_DB_NAME=wordpress -p 9300:80 wordpress
```

De acuerdo con el trabajo realizado, en el esquema del ejercicio el puerto a es **9300**

Ingresar desde el navegador al wordpress y finalizar la configuración de instalación.
<img width="1096" height="986" alt="wordpress instalation" src="https://github.com/user-attachments/assets/0043e08d-267d-4990-8ad9-01d84053fec5" />


Desde el panel de admin: cambiar el tema y crear una nueva publicación.
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress
<img width="1910" height="698" alt="wordpress new entry" src="https://github.com/user-attachments/assets/91461124-dc50-4858-9a95-59dc1d216b57" />


### Eliminar el contenedor wordpress
```
docker rm -f wordpress
```

### Crear nuevamente el contenedor wordpress
Ingresar a: http://localhost:9300/ 
recordar que a es el puerto que usó para el mapeo con wordpress

### ¿Qué ha sucedido, qué puede observar?
Al recrear el contenedor WordPress, las publicaciones y la configuración almacenadas en el contenedor MySQL se mantienen, pero los archivos del contenedor WordPress (temas, plugins y subidas) se pierden. Por eso, si se había cambiado el tema, WordPress intenta cargar un tema inexistente y muestra una pantalla en blanco; si se usan los temas por defecto, el sitio funciona correctamente. Esto muestra que los cambios en archivos requieren un volumen persistente para conservarse.
