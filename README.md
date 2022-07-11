1-	Crear un repositorio en Github configurado para que notifique a Jenkins cuando se genere un nuevo cambio.
2-	Dentro del repositorio encontraremos las dos app solicitadas (Node.js y Java), tome dos sample application para realizar esta prueba.

Para implementar Jenkins en GKE:

1-	Si no tenemos un proyecto, podemos crear uno nuevo, debemos habilitar la facturación y en este caso habilitar las APIs de GKE.
2-	Creamos una service account que será la que interactue entre Jenkins y nuestro cluster de kubernetes, en este caso le asignaremos el rol de Administrador de Kubernetes Engine, le crearemos una JSON key la cual descargaremos y guardaremos.
3-	Activamos Cloud Shell y clonamos nuestro repositorio de GitHub creado anteriormente.
4-	Dentro de nuestro repositorio en CloudShell, creamos nuestro cluster de GKE incluyendo el scope de “cloud-platform” para que Jenkins acceda a Container Registry donde almacenaremos las imágenes Docker.
5-	Asignar el cluster role de administrador de clústeres al usuario para poder dar permisos en el cluster.
6-	Implementamos Jenkins mediante Helm y personalizamos con nuestra configuración creada en Jenkins/values.yml dentro de nuestro repositorio.
7-	Configuramos la redirección de puertos de Jenkins.
8-	Ya podemos acceder a Jenkins dentro de la preview en el puerto indicado en el punto anterior.

Una vez implementado Jenkins, procedemos a la implementación de una app Node.js/Java en GKE:

1-	En caso de no estar activas, activar las API de Compute Engine y Cloud Build.
2-	Asignar el rol correspondiente a la Service Account de Jenkins, en producción siempre mantener la buena práctica de dar el mínimo privilegio necesario.
3-	Guardar las credenciales de la Service Account descargadas dentro de las credenciales globales de Jenkins.
4-	Creamos el job para el pipeline en Jenkins donde incluiremos el jenkinsfile con los stage necesarios para el deployment como son el checkout, el build, el push de la imagen y por ultimo el deploy en GKE
