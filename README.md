###Escuela Colombiana de Ingeniería
###Procesos de desarrollo de Software – PDSW
###Laboratorio

En este ejercicio, va a implementar una aplicación Web muy básica, haciendo uso de los elementos de más bajo nivel de Java-EE (Enterprise Edition), con el fin de revisar los conceptos del protocolo HTTP. En este caso, se trata de un módulo de consulta de clientes Web que hace uso de una librería de acceso a datos disponible en un repositorio Maven local.


I. Para esto, realice lo siguiente:

1. Revise la clase SampleServlet incluida en el proyecto, e identifique qué hace. Revise qué valor tiene el parámetro 'urlPatterns' de la anotación @WebServlet, pues este indica qué URLs atiende las peticiones el servlet.
2. Revise en el pom.xml para qué puerto TCP/IP está configurado el servidor embebido de Tomcat (ser sección de plugins).
3. Compile y ejecute la aplicación en el servidor embebido Tomcat, a través de Maven con:

	```xml
	mvn package
	mvn tomcat7:run
```
4. Abra un navegador, y en la barra de direcciones ponga la URL con la cual se le enviarán peticiones al 'SampleServlet'. Tenga en cuenta que la URL tendrá como host 'localhost', y como puerto, el configurado en el pom.xml. Debería obtener un mensaje de saludo.
5. Observe que el Servlet 'SampleServlet' acepta peticiones GET, y opcionalmente, lee el parámetro 'nombre'. Ingrese la misma URL, pero ahora agregando un parámetro GET (si no sabe como hacerlo, revise la documentación en http://www.w3schools.com/tags/ref_httpmethods.asp). 
6. Agregue el repositorio en el cual se encuentra la dependencia requerida para el ejercicio:


	```xml
    <repositories>
        <repository>
            <id>ECI internal repository</id>
            <url>http://profesores.is.escuelaing.edu.co/hcadavid/mvnmirror</url>
        </repository>
    </repositories>
```


7. Agregue la dependencia requerida:

	```xml
	<dependency>
		<groupId>org2.pdsw.stubs</groupId>
		<artifactId>DataSourceStub</artifactId>
		<version>1.1</version>            
	</dependency>             
```


8. Cree una clase que herede de la clase HttpServlet, y para la misma sobrescriba el método heredado doGet (puede usar el asistente de NetBeans con: Source/InsertCode/Override method). Incluya la anotación @Override para verificar –en tiempo de compilación- que efectivamente se esté sobreescribiendo un método de las superclases.
3. Para indicar en qué URL el servlet interceptará las peticiones GET, agregue al método la anotación @WebServlet, y en dicha anotación, defina la propiedad urlPatterns, indicando la URL (usted decida cual) a la cual se asociará el servlet.

10. Teniendo en cuenta las siguientes métodos disponibles en los objetos ServletRequest y ServletResponse recibidos por el método doGet:

	* response.setStatus(N);  <- Indica con qué código de error N se generará la respuesta.
	* request.getParameter(param);  <- Consulta el parámetro recibido, asociado al nombre ‘param’.
	* response.getWriter() <- Retorna un objeto PrintWriter a través del cual se le puede enviar la respuesta a quien hizo la petición.

	Implemente dicho método de manera que:
	
	* Asuma que la petición HTTP recibe como parámetro el número de identificación de un cliente, y que dicha identificación es un número entero.
	
	* Con el identificador recibido, consulte los datos del cliente a través de la clase DataSourceStub, de la librería publicada en el repositorio de Maven.
	
	* Si el cliente existe:
		* Responder con el código 200, y como contenido de dicha respuesta, código html correspondiente a una página con una tabla que tenga los detalles del cliente.
	* Si el cliente no existe:
		* Responder con el código correspondiente a ‘petición inválida’, y con el código de una página html que indique que no existe un cliente con el identificador dado.

5. Una vez hecho esto, verifique el funcionamiento de la aplicación, recompile y ejecute la aplicación.

6. Intente hacer una consulta desde un navegador Web.

__Parte II.__

7. En su servlet, sobreescriba el método doPost, y haga la misma implementación del doGet.
8. Revise la estructura de directorios del proyecto, e identifique la localización de la página de inicio de la aplicación (index.html). En dicha página, cree un formulario que tenga un campo para ingresar el número de identificación del cliente (si no ha manejado html antes, revise http://www.w3schools.com/html/ ) y un botón. El formulario debe usar como método ‘POST’, y como acción, la ruta relativa del servlet (es decir la URL pero excluyendo 'http://localhost:8080/').

9. Recompile y ejecute la aplicación. Abra en su navegador http://localhost:8080/index.html , y rectifique que la página hecha anteriormente sea mostrada. Ingrese los datos y verifique los resultados. Cambie el formulario para que ahora en lugar de POST, use el método GET. Qué diferencia observa?
