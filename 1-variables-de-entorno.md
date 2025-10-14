# Variables de Entorno
### ¿Qué son las variables de entorno?
Las variables de entorno son pares clave-valor que almacenan información sobre el entorno donde se ejecuta un programa, como rutas, configuraciones o credenciales. Permiten que aplicaciones y scripts adapten su comportamiento sin modificar el código, mejoran la seguridad al guardar datos sensibles fuera del código y facilitan la portabilidad entre diferentes entornos.

### Para crear un contenedor con variables de entorno

```
docker run -d --name <nombre contenedor> -e <nombre variable1>=<valor1> -e <nombre variable2>=<valor2>
```

### Crear un contenedor a partir de la imagen de nginx:alpine con las siguientes variables de entorno: username y role. Para la variable de entorno rol asignar el valor admin.

```
docker run -d --name nginx-srv -e username=user -e role=admin nginx:alpine
```
<img width="610" height="217" alt="nginx-srv env" src="https://github.com/user-attachments/assets/16b39cb6-f309-4e9c-b0a9-6009b06a799b" />

### Crear un contenedor con la imagen de mysql, mapear todos los puertos
```
docker run -d --name mysql -p 3306:3306 mysql:latest
```

### ¿El contenedor se está ejecutando?
```
docker ps
```
El contenedor no está ejecutándose.  

<img width="643" height="44" alt="docker ps" src="https://github.com/user-attachments/assets/17d68108-a68b-40d2-96de-e1c631d4a759" />


### Identificar el problema
```
docker logs mysql
```
El error indica que la base de datos es nueva y no inicializada y que no se ha especificado una contraseña para el usuario root. MySQL requiere, al crear un contenedor por primera vez, que se establezca la contraseña de root mediante la variable de entorno MYSQL_ROOT_PASSWORD, se permita explícitamente una contraseña vacía (MYSQL_ALLOW_EMPTY_PASSWORD) o se genere una contraseña aleatoria (MYSQL_RANDOM_ROOT_PASSWORD). Al no cumplir ninguna de estas condiciones, el contenedor se detiene inmediatamente.

<img width="1017" height="179" alt="docker logs mysql" src="https://github.com/user-attachments/assets/90469f45-443b-4639-8768-f1b7b97a0dbc" />

El comando corregido sería aquel que incluye la variable de entorno MYSQL_ROOT_PASSWORD, por ejemplo:
```
docker run -d --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw mysql:latest
```


### Para crear un contenedor con variables de entorno especificadas
- Portabilidad: Las aplicaciones se vuelven más portátiles y pueden ser desplegadas en diferentes entornos (desarrollo, pruebas, producción) simplemente cambiando el archivo de variables de entorno.
- Centralización: Todas las configuraciones importantes se centralizan en un solo lugar, lo que facilita la gestión y auditoría de las configuraciones.
- Consistencia: Asegura que todos los miembros del equipo de desarrollo o los entornos de despliegue utilicen las mismas configuraciones.
- Evitar Exposición en el Código: Mantener variables sensibles como contraseñas, claves API, y tokens fuera del código fuente reduce el riesgo de exposición accidental a través del control de versiones.
- Control de Acceso: Los archivos de variables de entorno pueden ser gestionados con permisos específicos, limitando quién puede ver o modificar la configuración sensible.

### ¿Qué bases de datos existen en el contenedor creado?
```
docker exec -it mi-mysql mysql -uroot -p
```
<img width="748" height="521" alt="mysql" src="https://github.com/user-attachments/assets/0feba320-ca11-4e97-b368-2b702357aa6d" />

