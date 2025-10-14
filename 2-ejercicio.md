### Crear contenedor de Postgres sin que exponga los puertos. Usar la imagen: postgres:15-alpine3.21
```
docker run -d --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword postgres:15-alpine3.21
```

### Crear un cliente de postgres. Usar la imagen: dpage/pgadmin4
```
docker run -d --name pgadmin -e PGADMIN_DEFAULT_EMAIL=admin@example.com -e PGADMIN_DEFAULT_PASSWORD=password -p 8080:80 dpage/pgadmin4
```

La figura presenta el esquema creado en donde los puertos son:
- a: 8080
- b: 80
- c: 5432
![Imagen](esquema-2-ejercicio.PNG)

## Desde el cliente
### Acceder desde el cliente al servidor postgres creado.

<img width="1441" height="747" alt="pgadmin login" src="https://github.com/user-attachments/assets/43a2ae5c-f93f-476f-a08d-8b6242072756" />  
<img width="1914" height="839" alt="pgadmin post login" src="https://github.com/user-attachments/assets/b5515a8c-17fa-41f2-897a-204b37a67701" />  

```
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' some-postgres
```
<img width="943" height="44" alt="docker inspect -f some-postgres" src="https://github.com/user-attachments/assets/e6adad92-6aa3-414d-97ce-801fd4874754" />

<img width="929" height="731" alt="register postgres server" src="https://github.com/user-attachments/assets/83968785-eb58-4159-899b-8db19ebd5ad5" />  

<img width="455" height="170" alt="postgres server" src="https://github.com/user-attachments/assets/ca051291-ffa5-457f-94fa-2168e428b4bf" />

### Crear la base de datos info, y dentro de esa base la tabla personas, con id (serial) y nombre (varchar), agregar un par de registros en la tabla, obligatorio incluir su nombre.
<img width="791" height="363" alt="info schema and data" src="https://github.com/user-attachments/assets/93cc7855-09ed-4e20-b961-04d1f457a171" />


## Desde el servidor postgresl
### Acceder al servidor
### Conectarse a la base de datos info
```
docker exec -it some-postgres psql -U postgres
```

```
\c info
```
### Realizar un select *from personas
<img width="589" height="273" alt="Screenshot 2025-10-13 221054" src="https://github.com/user-attachments/assets/d73d030a-8f62-4cbf-b5d3-ce5a9b3bb1ef" />

