# Definición o Modelado del REST API utilizando Swagger

Para realizar el modelado de la definición de nuestra API vamos a utilizar **Swagger**, que es un lenguaje de modelado o descripción de REST API. Swagger sigue los lineamientos de OpenAPI Specification (OAS).

La especificación OpenAPI Specification (OAS) establece una interfaz para describir una API de una manera que permita a cualquier desarrollador o aplicación descubrirla y comprender completamente sus parámetros y funcionalidades, entre ellos puntos finales disponibles (end-points), operaciones permitidas en cada end point, parámetros de operación, métodos de autenticación y otra información. 

Para más información acerca de lineamientos de OpenAPI Specification te recomiendo visitar este enlace --> [LINK](https://github.com/OAI/OpenAPI-Specification/blob/main/versions/3.1.0.md)

## Definición de nuestro REST API
1. Acceder a la página de Swagger [https://swagger.io/](https://swagger.io/)
2. Una vez en la página hacer clic en el botón "Sign In" ubicado en la parte superior derecha<br><br>
![image](https://user-images.githubusercontent.com/99369122/171200302-584e70fe-01a7-4cbc-804e-678f85f9cc94.png)<br><br>
3. A continuación nos aparecerá una pantalla para hacer Log In, hay distintas formas de loguearnos, yo recomiendo hacerlo con nuestra cuenta de GitHub<br><br>
![image](https://user-images.githubusercontent.com/99369122/171201174-de4ddd4c-c3ca-4c14-8c9d-563ddff66bcd.png)<br><br>
4. Llenamos los campos con el usuario de nuestra cuenta de GitHub y damos clic en "Sign in"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171201534-9cc87445-2a5d-4baf-8032-18ae909cf350.png)<br><br>
5. Una vez logueados correctamente nos aparecerá la siguiente pantalla, nosotros vamos a hacer clic en el botón "CREATE API" ubicado en la parte inferior de la pantalla<br><br>
![image](https://user-images.githubusercontent.com/99369122/171203282-e4e7d8af-ffdf-425b-8cd2-fcac3185620b.png)<br><br>
6. Nos aparecerá la siguiente ventana, la cual llenaremos de la siguiente forma. Noten que **personas-api** es el nombre que decidimos para ponerle a nuestro proyecto, ustedes pueden remplazarlo por el nombre de su proyecto, y el apartado **Owner**a, parece de acuerdo con el perfil de GitHub con el que hayan hecho Log In. Una vez llenados todos los campos, vamos a hacer clic sobre "Create API"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171204397-8886cdf4-b358-4154-a181-a49f850931d4.png)<br><br>
7. Nos aparecerá una ventana como la siguiente. Swagger nos ayuda dándonos un ejemplo de cómo comenzar y cómo modelar nuestro REST API. Si quieres saber más acerca de este proceso, te invito a revisar el ejemplo que nos da Swagger, para que te familiarices con la estructura, la sintaxis y los elementos con los que trabaja Swagger para el modelado de un REST API.<br><br>
![image](https://user-images.githubusercontent.com/99369122/171205641-b5d9ac5d-79ae-47dc-88fd-7aadb48599f8.png)<br><br>
8. Nosotros borraremos el ejemplo que viene de forma determinada, e iremos escribiendo nuestra definición paso a paso. <br><br>
9. Comenzamos introduciendo los datos generales de nuestra API, tales como descripción, baseURL, versión, tipo de contenido que producirá nuestra API,etc:

```yml
    openapi: 3.0.0
servers:
  # Added by API Auto Mocking Plugin
  - description: Personas-API
    url: https://virtserver.swaggerhub.com/RobertoPeredo/personas-api/1.0.0
   
info:
  description: Esta es la definición de un REST API que sirve para los datos de un conjunto de datos de personas
  version: "1.0.0"
  title: Personas-API
  contact:
    email: robertopgzm@gmail.com
  license:
    name: Apache 2.0
    url: 'http://www.apache.org/licenses/LICENSE-2.0.html' 
    
```

10.Después de esto, definimos los componentes, que son: nuestro modelo de Persona, que son prácticamente todos los datos que puede tener una persona en nuestro proyecto. También definimos el formato de los mensajes de error que devolverán nuestros servicios. Los definimos de esta forma, para que después los podamos referenciar y no tengamos que estar repitiendo código.

```yml
components:
  schemas:
    Persona:
      type: object
      required:
        - Nombre
        - Apellido
        - Edad
        - Mail
        - Celular
      properties:
        Nombre:
          type: string
          example: Roberto
        Apellido:
          type: string
          example: Peredo
        Edad:
          type: integer
          example: 25
        Mail:
          type: string
          example: roberto@correo.com
        Celular:
          type: integer
          example: 2222222222
    PersonaId:
      type: object
      required:
        - id
        - Nombre
        - Apellido
        - Edad
        - Mail
        - Celular
      properties:
        id:
          type: integer
          example: 3
        Nombre:
          type: string
          example: Roberto
        Apellido:
          type: string
          example: Peredo
        Edad:
          type: integer
          example: 25
        Mail:
          type: string
          example: roberto@correo.com
        Celular:
          type: integer
          example: 2222222222
    Error:
      type: object
      required:
        - code
        - message
      properties:
        code:
          type: integer
          format: int32
          example: 404
        message:
          type: string
          example: NotFound
   
```

11.Finalmente definimos los endpoints y métodos http que nuestro API tendrá:

```yml
paths:
  /personas:
  
##################### GET #################
    get:
      tags:
        - END-POINTS
      summary: Obtener los datos de todas las personas
      description: Al hacer la consulta GET en el path "/personas", recibimos como respuesta un arreglo con todos las personas y sus respectivos datos
      responses:
        '200':
          description: Consulta correcta
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/PersonaId'
        default:
            description: Error inesperado
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
                  
            
##################### POST #################
    post:
      tags:
        - END-POINTS
      summary: Añadir el registro de una persona
      description: Al hacer la consulta POST en el path "/personas",mandamos los datos necesarios para modificar a una persona en nuestra lista de peronas
      requestBody:
        description: Datos de la persona a agregar
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Persona'
        
      responses:
        '201':
          description: Registro creado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PersonaId'
        default:
            description: Error inesperado
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
      
  
  /personas/{id}:
  
##################### GET #################
    get:
      tags:
        - END-POINTS
      summary: Obtener los datos una persona de acuerdo a su Id
      description: Al hacer la consulta GET en el path "/personas/{id}", se hace la consulta de una persona de acuerdo a su id y  recibimos como respuesta un arreglo con los datos de esta persona
      parameters: 
         - name: id
           in: path
           description: Id de la persona la cual se va a consultar
           required: true
           schema:
             type: integer
      responses:
        '200':
          description: Consulta correcta
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PersonaId'
        default:
            description: Error inesperado
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
  
    ##################### DELETE #################
    delete:
      tags:
        - END-POINTS
      summary: Eliminar persona de acuerdo a  su Id
      description: Al hacer la consulta DELETE en el path "/personas/{id}", se hace la consulta de una persona de acuerdo a su id y  se elimina de la lista de personas
      parameters: 
         - name: id
           in: path
           description: Id de la persona a eliminar
           required: true
           schema:
             type: integer
      responses:
        '204':
          description: Registro eliminado
          content: 
            application/json:
              schema:
                type: integer
                example: 3
        default:
            description: Error inesperado
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'
                  
                  
      ##################### PUT #################
    put:
      tags:
        - END-POINTS
      summary: Modifica el registro de una persona de acuerdo a  su Id
      description: Al hacer la consulta PUT en el path "/personas/{id}", se hace la consulta de una persona de acuerdo a su id y  se modifica el registro de la misma
      requestBody:
        description: Datos de la persona a agregar
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Persona'
      parameters: 
         - name: id
           in: path
           description: Id de la persona a modificar.
           required: true
           schema:
             type: integer
       
             
      responses:
        '204':
          description: Registro actualizado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/PersonaId'
        default:
            description: Error inesperado
            content:
              application/json:
                schema:
                  $ref: '#/components/schemas/Error'

```
12.La definición de nuestra API está terminada, a continuación, le comparto el LINK de nuestra API en Swagger, por si se realiza alguna modificación en el futuro, para que puedan interactuar con nuestra API y para que tengan acceso al código completo:

 [PERSONAS-API](https://app.swaggerhub.com/apis/RobertoPeredo/personas-api/1.0.0)
 
 
 También les dejo la documentación que nos genera Swagger, para que observen cómo es que va a estar funcionando nuestro REST API
 
 [DOCUMENTACIÓN](https://app.swaggerhub.com/apis-docs/RobertoPeredo/personas-api/1.0.0)
 
 
 Pueden descargar el API en formato tipo JSON y comenzar a hacer pruebas del funcionamiento en algún servicio como POSTMAN, nosotros lo estaremos utilizando en la siguiente parte del tutorial, la cual consiste en que una vez tengamos definida nuestra API la vamos a implementar en Node.Js

 ¡Esto es todo! Ya tenemos nuestra API definida, prototipada y lista para ser utilizada y desarrollada.

    
    
 


