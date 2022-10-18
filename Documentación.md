# Documentación

Con este archivo se pretende mostrar todo lo aprendido en el proceso de realización del entregable. Además se indicarán los enlaces usados para dicho proposito.

## Proceso de realización del entregable

Este entregable consiste en crear dos máquinas virtuales. La primera de ellas es un balanceador que enrutará todas las peticiones y el tráfico hacia la instancia de aplicación, que es la segunda máquina virtual. Ambas máquinas deben tener un acceso por ssh securizado y la segunda máquina debe tener Wordpress instalado por defecto además de no ser accesible desde Internet.

En los requisitos se recomienda utilizar Google Cloud o AWS y, dado que es la primera vez que realizo una tarea de este estilo, he optado por utilizar Google Cloud por la inmensa cantidad de documentación que se ofrece.

### Creación de las máquinas virtuales

Una vez he accedido a Google Cloud y he creado un proyecto para el entregable, me dispongo a crear las MV. La primera que realizaré es el balanceador.

El primer paso es ir a Compute Engine -> Instancias -> Crear instancia donde podremos poner las características que debe tener para el correcto funcionamiento. A destacar, se habilita el tráfico http y https, se pone la red default que utilizaré en ambas MV para que puedan comunicarse entre ellas y se habilita la opción de reenvío de IP para poder recibir y mandar las peticiones de la aplicación.

Para poder crear la instancia de wordpress, se ha utilizado un software proporcionado por Google Cloud que facilita el despliegue de una instancia con wordpress instalado. Con este despliegue, algunas de las opciones de configuración debían añadirse a posteriori ya que ese software no lo permitía al principio.

![Crear instancia wordpress](/images/Crear_instancia_wordpress2.jpeg)

 Una vez realizado ese paso, creamos un nuevo usuario y contraseña para las máquinas, de forma que tengan un acceso ssh securizado. 

![Crear usuario](/images/crear-usuario.jpeg)

Por defecto, google cloud utiliza una clave pública que puede mejorar la seguridad del ssh. En este proyecto se ha deshabilitado (aunque sea contradictorio) como se puede ver en la imagen porque si no se hiciera sería complicado acceder a las máquinas virtuales en la revisión del entregable. 

![Opción de llave pública deshabilitada](/images/Cambio-clave-publica.jpeg)

El siguiente requisito es una url con un dominio donde poder acceder a un Wordpress instalado por defecto. Como se ha mencionado en el entregable, se ha incluido en el archivo hosts el nombre para poder acceder. Después, se comprueba que funciona con el comando curl, que devuelve todo el contenido de la página.

![Inserción de la URL y comprobación](/images/url-hosts.jpeg)

Otra parte del entregable consistía en hacer que la instancia de la aplicación no tuviera accesibilidad desde Internet, es decir, que solo aceptara tráfico proveniente del balanceador. Aunque no lo he visto claro, he optado por modificar las IPs de enrutamiento porque es a lo que más sentido le he encontrado (también consideré cambiar algunas opciones del firewall pero me ha constado encontrar información al respecto). Haciendo esto, cualquier paquete de la aplicación sale por la ip del balanceador y por otro lado, el balanceador debe tener otra ruta que redirija los paquetes hacia la aplicación. Gracias a la opción habilitada al principio esto es posible. Por desgracia, me ha dado muchos errores al hacer esto. Algo que también se me ocurrió es crear un tunel entre las dos máquinas y cambiar la interfaz de salida en la aplicación por el túnel pero me ha faltado tiempo para realizarlo.

Por último, se pedía publicar la configuración de los servicios en el repositorio. Con esta parte estuve bastante tiempo ya que había comenzado desde la página de Google Cloud y la única forma que encontraba era utilizar un docker para subirlo todo. Por desgracia me di cuenta tarde de que usando infrastructure as code esta parte solucionaba muchos problemas y cuando empecé a buscar documentación al respecto ya era tarde (hice la configuración inicial para poder usar Terraform pero no ví factible realizar el proyecto entero con el poco tiempo que me quedaba). Como he empezado el proyecto sin conocimientos al respecto, pensé que sería mejor entender primero lo básico, dejando de lado Terraform. Este es el motivo por el que no he sido capaz de lograr el objetivo de publicar en el repositorio la configuración de los servicios (también hay un intento de documento .yaml por eso).

  ### Bibliografía
  
  Instancias de máquina virtual: https://cloud.google.com/compute/docs/instances?hl=es-419
  
  Crea e inicia una instancia de VM: https://cloud.google.com/compute/docs/instances/create-start-instance?hl=es-419
  
  Conéctate a instancias de VM de forma segura:
  https://cloud.google.com/solutions/connecting-securely?hl=es-419
  https://cloud.google.com/compute/docs/metadata/manage-guest-attributes
  
  
  Conéctate a un repositorio de GitHub: https://cloud.google.com/build/docs/automating-builds/github/connect-repo-github?hl=es-419
  
  Crea un archivo de configuración de compilación (para github): https://cloud.google.com/build/docs/configuring-builds/create-basic-configuration?hl=es_ES
  
  Información sobre terraform: 
  https://learn.hashicorp.com/tutorials/terraform/aws-build?in=terraform/aws-get-started
  https://www.youtube.com/watch?v=JQYgFSYFi-o
  
	
