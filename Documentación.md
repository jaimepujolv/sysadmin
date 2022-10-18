# Documentación

Con este archivo se pretende mostrar todo lo aprendido en el proceso de realización del entregable. Además se indicarán los enlaces usados para dicho proposito.

## Proceso de realización del entregable

Este entregable consiste en crear dos máquinas virtuales. La primera de ellas es un balanceador que enrutará todas las peticiones y el tráfico hacia la instancia de aplicación, que es la segunda máquina virtual. Ambas máquinas deben tener un acceso por ssh securizado y la segunda máquina debe tener Wordpress instalado por defecto además de no ser accesible desde Internet.

En los requisitos se recomienda utilizar Google Cloud o AWS y, dado que es la primera vez que realizo una tarea de este estilo, he optado por utilizar Google Cloud por la inmensa cantidad de documentación que se ofrece.

### Creación de las máquinas virtuales

Una vez he accedido a Google Cloud y he creado un proyecto para el entregable, me dispongo a crear las MV. La primera que realizaré es el balanceador.

El primer paso es ir a Compute Engine -> Instancias -> Crear instancia donde podremos poner las características que debe tener para el correcto funcionamiento. A destacar, se habilita el tráfico http y https, se pone la red default que utilizaré en ambas MV para que puedan comunicarse entre ellas, se habilita la opción de reenvío de IP para poder recibir y mandar las peticiones de la aplicación y se habilitan los atributos de invitado para realizar una conexión ssh segura. Esta sería la configuración básica de las dos máquinas virtuales.

Una vez realizado ese paso, creamos un nuevo usuario y contraseña para las máquinas, de forma que tengan un acceso ssh securizado. Por defecto, google cloud utiliza una clave pública que puede mejorar la seguridad del ssh. En este proyecto se ha deshabilitado (aunque sea contradictorio) como se puede ver en la imagen porque si no se hiciera sería complicado acceder a las máquinas virtuales en la revisión del entregable. 

![Opción de llave pública deshabilitada](/images/Cambio-clave-publica.jpeg)

El siguiente requisito es una url con un dominio donde poder acceder a un Wordpress instalado por defecto. Como se ha mencionado en el entregable, se ha incluido en el archivo hosts el nombre para poder acceder. 


