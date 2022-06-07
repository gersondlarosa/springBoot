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

##Genera un paquete que se llame com.bolsadeideas.springboot.backend.apirest.models.entity dandole click derecho en el main que es com.bolsadeideas.springboot.backend.apirest le daremos boton de recho new package

![pacage](https://user-images.githubusercontent.com/68626555/172486211-7f08a860-4505-424e-88cf-93a7dd713247.png)


Teniendo nuesto paquete crearemos una Clase Clientes que sera nuestro pojo de java con los dastos del cliente y generaremos nuestros Getters y Setters

	private Long id;
	private String nombre;
	private String apellido;
	private String email;
	private Date createAt;
  
  nuestra clase traeremos la interface Serializable pos esta trabajando con Spring y si queremos guardar los atributos de la sesion decoraremos con @Entity para indicar que es una entdiada y @Table para ponerle un nombre en la base de datos nuestros i lo decoraremos con @Id para indicar que es una llave primaria y con 
  @GeneratedValue(strategy = GenerationType.IDENTITY) identity es cuando los id se forman de manera se generan de manera incremental y se ocupa con el motor de MySQL
  y la fecha se decorara 	@Column(name = "create_at") @colum es para cambia el nombre en base de datos y 	@Temporal(TemporalType.DATE) se ocupara para ocupar el tipo     DATE para transforma la fecha de MySQL

  
   @Entity
   @Table(name = "clientes")
   public class Cliente implements Serializable {

	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;

	private String nombre;
	private String apellido;
	private String email;

	@Column(name = "create_at")
	@Temporal(TemporalType.DATE)
	private Date createAt;
	
	@PrePersist
	public void prePersist() {
		createAt = new Date();
	}

	public Long getId() {
		return id;
	}

	public void setId(Long id) {
		this.id = id;
	}

	public String getNombre() {
		return nombre;
	}

	public void setNombre(String nombre) {
		this.nombre = nombre;
	}

	public String getApellido() {
		return apellido;
	}

	public void setApellido(String apellido) {
		this.apellido = apellido;
	}

	public String getEmail() {
		return email;
	}

	public void setEmail(String email) {
		this.email = email;
	}

	public Date getCreateAt() {
		return createAt;
	}

	public void setCreateAt(Date createAt) {
		this.createAt = createAt;
	}

	/**
	 * 
	 */
	private static final long serialVersionUID = 1L;

}

  
  


![entity](https://user-images.githubusercontent.com/68626555/172488531-e0fd98c2-5d1e-4240-bd5e-0b72b711b15a.png)

y al correr nuestra entity debemos de verfica que se crea las tablas en base de datos en MySQL![CLIENTES](https://user-images.githubusercontent.com/68626555/172489062-50292058-8908-401f-9cda-bfd3a615c166.png)
