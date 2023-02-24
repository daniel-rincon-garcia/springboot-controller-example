# springboot-controller-example
This project shows how to configure an Spring Boot application and how to create a rest controller that exposes a web service.

Spring Boot:
- Se descargó lo siguiente:
  * IntelliJ --> ideaIU-2022.3.2.exe
  * Java SE Runtime Environment --> JavaSetup8u361.exe --> No es necesario instalarlo.
  * Maven --> apache-maven-3.9.0-bin.zip --> No es necesario instalarlo.
  * Java 11 --> amazon-corretto-11.0.18.10.1-windows-x64.msi
  * STS (Spring Tool Suite) --> spring-tool-suite-4-4.17.2.RELEASE-e4.26.0-win32.win32.x86_64.self-extracting.jar
- Instalación:
  * IntelliJ:
    + Desde "Variables de usuario para <user>" de "Variables de entorno" en Windows se añadió a la variable Path:
	  %IntelliJ IDEA% 
	+ Luego desde "Variables de entorno" de Windows se estableció en "Variables de usuario para <user>" las siguientes variables:
	  IntelliJ IDEA: C:\Program Files\JetBrains\IntelliJ IDEA 2022.3.2\bin  
  * Java 11:
    + https://www.youtube.com/watch?v=c7RNlNyx5OI
	+ La primera razón para usar esta versión de Java es que Java 8 ya se encuentra un poco desfasado (aunque tiene soporte hasta 2026 e incluso ciertas cosas hasta 2030).
	+ Java 11 es una versión LTS, esto quiere decir que es una versión con un tiempo más largo de soporte.
	+ Vamos a https://aws.amazon.com/es/corretto/, una vez dentro descargamos el JDK que provee Amazon Coretto pulsando en "Descargar Amazon Corretto" y bajamos el .msi del JDK de Windows x64. No nos descargamos el JDK que provee Oracle ya que este JDK sufrió algunos cambios a nivel de licencias por tanto para desarrollar con el de Oracle necesitamos pagar las licencias comerciales. Amazon Corretto es una distribución que utiliza Amazon en el desarrollo de sus servicios que parte del OpenJDK que es una distribución abierta para desarrollos con Java.
	+ Vamos a Panel de control --> Programas --> Programas y características y desinstalamos Java 8 para que no haya conflictos.
	+ Instalamos el paquete de Amazon Coretto 11.
    + Desde "Variables del sistema" de "Variables de entorno" en Windows se añadió a la variable Path:
	  C:\Program Files\Amazon Corretto\jdk11.0.18_10\bin o bien %JAVA_HOME%\bin
	  C:\Program Files (x86)\Common Files\Oracle\Java\javapath
	+ Luego desde "Variables de entorno" de Windows se estableció en "Variables del sistema" las siguientes variables:
	  JAVA_HOME: C:\Program Files\Amazon Corretto\jdk11.0.18_10	  
  * Maven:
    + Se descomprimió el .zip de maven en C:\maven\apache-maven-3.9.0.
	+ Desde "Variables del sistema" de "Variables de entorno" en Windows se añadió a la variable Path:
	  %MAVEN_HOME%\bin
	+ Luego desde "Variables de entorno" de Windows se estableció en "Variables del sistema" las siguientes variables:
	  MAVEN_HOME: C:\maven
  * STS (Spring Tool Suite): es un IDE basado en eclipse pero adapatado para trabajar con Spring y Spring Boot.
    + https://www.youtube.com/watch?v=89Mr-dYcHxA
    + Ponemos en Google "sts download", nos llevará a https://spring.io/tools, una vez dentro descargamos "Spring Tools 4 for Eclipse" --> "4.17.2-WINDOWS X86_64", esto nos descargará un jar.
	+ Le damos doble click al jar, no a extraer y nos generará una carpeta llamada "sts-4.17.2.RELEASE".
	+ Para ejecutar el "Spring Tool Suite", damos doble click al ejecutable SpringToolSuite4.exe.
	+ Creamos una carpeta llamada workspace en C:\Proyectos\workspace.
	+ Seleccionamos el path del workspace que hemos creado antes y hacemos click en "Launch".
	+ Como podemos ver se parece mucho a eclipse.
	+ Tenemos que apuntar al JDK de Java que hemos instalado ya que por lo general STS apunta al JRE pero es importante apuntar al JDK ya que el JDK es el entorno deonde Java tiene la mayoría de bibliotecas y clases para trabajar. Para ello vamos a Window --> Preferences --> Java --> Installed JREs, aquí dejamos que apunte al JRE y hacemos que apunte al JDK de antes, el C:\Program Files\Amazon Corretto\jdk11.0.18_10. Para ello damos a Add --> Standard VM --> Next y en JRE home ponemos C:\Program Files\Amazon Corretto\jdk11.0.18_10 y aparecerán los jar's que tiene el JDK para poder crear aplicaciones con Spring Tool Suite y con Spring framework.
	+ Window --> Preferences --> Java --> Compiler y seleccionamos 11 en "Compiler compliance level" ya que por alguna razón viene 14 por defecto.
- Crear proyecto Spring Boot:
  * https://www.youtube.com/watch?v=J4wyBKVgJx0	
  * Seleccionar jars con maven. Vamos a google y ponemos "spring initializr" y vamos a https://start.spring.io/
    + En Project seleccionamos Maven, en Language seleccionamos Java, en Spring Boot seleccionamos 3.0.3.
	+ En Group ponemos "com.ejemplo.springboot", en Artifact ponemos "spring-boot-ejemplo".
	+ Luego vamos a la parte más interesante de crear un proyecto Spring Boot que es la parte de dependencias, añadimos por ejemplo la web que sirve para crear proyectos MVC.
	+ Una vez que lo tengamos hacemos click en Generate. Esto creará el zip llamadado spring-boot-ejemplo.zip. Lo copiamos a C:\Proyectos\workspace y lo descomprimimos.
	+ Crear la aplicación. Abrimos el STS e importamos el proyecto que se ha descomprimido antes. Damos a File --> Import --> Maven --> Existing Maven Projects --> Next --> Browse --> C:\Proyectos\workspace\spring-boot-ejemplo --> Aceptar y Finish.
	+ El proyecto se importará y se actualizarán dependencias de Maven.
	+ Si nos vamos al fichero pom.xml veremos que contiene la dependencia web (la de MVC) con lo que se podrá crear un proyecto sencillo.
	+ Lo bueno de Spring Boot es que no tenemos que desplegarlo en un servidor, ya que Spring Boot crea las aplicaciones automaticamente como servicios. Como podemos ver, existe una clase con la anotación @SpringBootApplication que tiene el método main que sirve para ejecutar el proyecto en un servidor embebido.
	+ Creamos un controlador. Vamos a src/main/java --> New Class --> en Package ponemos "com.ejemplo.springboot.springbootejemplo.controller", en Name ponemos "HolaMundo".
	+ Se creará la clase que la ponemos la anotación @RestController, esto le dice a Spring Boot que esta clase va a ser un controlador que atiende peticiones rest de webservices.
	+ También ponemos la anotación @RequestMapping, esto le dice a Spring Boot que cuando busquemos un recurso la url va a ir a este controlador. Le ponemos el string / que quiere decir que cuando escribamos la url / se va a ir a mapear a este controlador.
	+ Creamos un método llamado home() que retorne "Hola Mundo!". Ponemos la anotación @RequestMapping(method=RequestMethod.GET). Por tanto cuando pongamos / en el navegador se va a ir al método home() del controlador.
	+ Desplegar en servidor. Damos click en Run (o click derecho en proyecto y en Run As elegimos Spring Boot App) y podemos ver que en la consola se levanta el servicio, como podemos ver Spring Boot trae un Tomcat embebido.
	
	
	
