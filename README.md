# springBoot
SpringBoot

#Se hace intalacion de MySQL y Spring Tool Suite 4

https://www.mysql.com/

https://spring.io/tools

#Luego configuramos nuestro proyecto 

Se creara un nuevo proyecto y le daremos en
File/new/other y parecela la sigueinte pantalla y le daremos en Spring Starter Project



![2022-05-24 19_30_02-](https://user-images.githubusercontent.com/68626555/170153454-f851e01e-c084-42b0-a92d-629888e7fa51.png)


Configuraremos de la siguiente manera o dependiendo de lo que quieras hacer 
en type lo dejaremos en Maven Project , Packaging lo dejaremos en jar, Java version yo tengo la version 8 ahi puedes poner la version que tu tengas en tu equipo y legnuaje java

![2](https://user-images.githubusercontent.com/68626555/170153691-b44da981-c78e-44db-99c6-4a47029e6873.png)

En la siguiente pantalla seleccionaremos la version de Sring Boot 2.7.0 dependiendo en que lugar o fecha te encuentre puede se que cambie tu version.
Vamos a marcar la dependencia web esta invluye las anotaciones para generar nuestros controladores rest full luego marcamos SQL y seleccionamos el Spring Data JPA luego marcamos MySQL que es nuestro motor de base de datos, despues marcamos Spring Boot Dev Tools que permite cambier cambio en nuestras clases se actualice de forma automatica el deploid depues damos finalizar y esperamos que se genere el proyecto puede tardar un poco a si que espremos


![3](https://user-images.githubusercontent.com/68626555/170154393-e9c04217-6e2b-4e48-8e70-e988a913f621.png)

al terminar nos debe de aparecer de la sigueitne manera nos va a crear un proyecto de springboot y ya tendra un pom.mx y una clase que tendra la anotacion
@SpringBootApplication que es la mas importante de nuestro proyecto si nos metemos a la anotacion veremos que ya trae configurada 

@SpringBootConfiguration .- Configuracion de SrpingBoot que podemos sobre escribir en aplication properties
@EnableAutoConfiguration .- Habilita la uto configuración 
@ComponentScan .- Busca y registra en el conenedor de Spring todas las clases anotasdas con @ResController, @Controller, @Component, @Repository y @Service


![2022-05-24 19_43_43-Window](https://user-images.githubusercontent.com/68626555/170154648-4c26838d-af01-486e-8de5-dd5ec2494cbe.png)


Se genera la base de datos 

# MySQL
MySQL
Ingresamos a Mysql y creasmo la base de datos que bamos a ocupar en mi caso la llame de la siguiente manera db_springboot_backend por el momento no tendra nada por que se desde bootstrap con persistencia

CREATE DATABASE db_springboot_backend;

USE db_springboot_backend;
SHOW databases;

![mysql](https://user-images.githubusercontent.com/68626555/170767266-580fa0a7-05e8-4ace-9c4d-2118ef385156.png)

Ahora generaremos la conexión base de datos en src/main/resources y buscamos application.properties


![properties](https://user-images.githubusercontent.com/68626555/170767655-fc6d7c87-5679-483e-ae45-6f9ccfae7492.png)


Aqui ponemos los guiente que es la configuracion de tu base de datos

//Este sirve para hacer la ruta a tu base de datso

spring.datasource.url=jdbc:mysql://localhost/db_springboot_backend?useSLL=false 

//Configuracion de nombre de usuario de mysql

spring.datasource.username=****** 

//Configuracion de nombre de password de mysql

spring.datasource.password=****

//Drivers de mysql

spring.datasource.dbcp2.driver-class-name=com.mysql.jdbc.Driver

//Perisistencia de hibernet

spring.jpa.database-platform=org.hibernate.dialect.MySQL57Dialect

//Este crea las tablas y las elimina al parar el proyeccto

spring.jpa.hibernate.ddl-auto=create-drop

//Esta línea registra las consultas SQL 

logging.lavel.org.hibernate.SQL=debug


![proper](https://user-images.githubusercontent.com/68626555/170770109-54ba6695-aae4-4015-a9dc-299c1a3af191.png)
