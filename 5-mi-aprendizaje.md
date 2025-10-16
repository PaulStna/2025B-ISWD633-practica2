# Aprendizajes de la Práctica 2 de Docker  
Antes de realizar la práctica, tenía conocimientos básicos sobre Docker y sabía que era necesario crear redes para que los contenedores se comunicaran, pero desconocía los detalles de los distintos tipos de redes y la gestión de datos confidenciales. Después de completar la tarea, aprendí que la red **bridge** es la predeterminada, que se pueden crear **redes bridge personalizadas** para organizar contenedores y definir subredes específicas, y que existen otras redes como **host**, que comparte la red del equipo, y **none**, que deshabilita la red. También comprendí que los cambios en los archivos de un contenedor requieren un **volumen** para persistir.

# Consulta sobre Docker Secrets
**Docker Secrets** permite almacenar información sensible como contraseñas o claves API de forma segura. Los contenedores pueden usar estos secretos sin exponerlos en variables de entorno, lo que garantiza que los datos confidenciales estén protegidos incluso en entornos compartidos o de producción. 

# Conclusiones
Con esta práctica aprendí más sobre cómo funcionan las redes en Docker y la importancia de usar volúmenes para que los datos persistan. Esto me ayuda a entender mejor cómo administrar contenedores de manera eficiente en proyectos futuros.
