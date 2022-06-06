
# Introducción

### ¿Qué es una API?

Las API son mecanismos que permiten a dos componentes de software comunicarse entre sí mediante un conjunto de definiciones y protocolos. API significa “interfaz de programación de aplicaciones”. En el contexto de las API, la palabra aplicación se refiere a cualquier software con una función distinta. La interfaz puede considerarse como un contrato de servicio entre dos aplicaciones. Este contrato define cómo se comunican entre sí mediante solicitudes y respuestas. La documentación de su API contiene información sobre cómo los desarrolladores deben estructurar esas solicitudes y respuestas.

####  ¿Cómo funcionan las API?

La arquitectura de las API suele explicarse en términos de cliente y servidor. La aplicación que envía la solicitud se llama cliente, y la que envía la respuesta se llama servidor.<br>

Las API pueden funcionar de cuatro maneras diferentes, según el momento y el motivo de su creación.

- API de SOAP <br>
Estas API utilizan el protocolo simple de acceso a objetos. El cliente y el servidor intercambian mensajes mediante XML. Se trata de una API menos flexible que era más popular en el pasado.
- API de RPC<br>
Estas API se denominan llamadas a procedimientos remotos. El cliente completa una función (o procedimiento) en el servidor, y el servidor devuelve el resultado al cliente.
- API de WebSocket<br>
La API de WebSocket es otro desarrollo moderno de la API web que utiliza objetos JSON para pasar datos. La API de WebSocket admite la comunicación bidireccional entre las aplicaciones cliente y el servidor. El servidor puede enviar mensajes de devolución de llamada a los clientes conectados, por lo que es más eficiente que la API de REST.
- API de REST<br>
Estas son las API más populares y flexibles que se encuentran en la web actualmente. El cliente envía las solicitudes al servidor como datos. El servidor utiliza esta entrada del cliente para iniciar funciones internas y devuelve los datos de salida al cliente. Veamos las API de REST con más detalle a continuación.

### ¿Qué es un REST API?

REST significa transferencia de estado representacional. REST define un conjunto de funciones como GET, PUT, DELETE, etc. que los clientes pueden utilizar para acceder a los datos del servidor. Los clientes y los servidores intercambian datos mediante HTTP.

La principal característica de la API de REST es la ausencia de estado. La ausencia de estado significa que los servidores no guardan los datos del cliente entre las solicitudes. Las solicitudes de los clientes al servidor son similares a las URL que se escriben en el navegador para visitar un sitio web. La respuesta del servidor son datos simples, sin la típica representación gráfica de una página web.

#### ¿Qué beneficios ofrecen las API de REST?
Las API de REST ofrecen cuatro beneficios principales:<br>

1. Integración <br>
Las API se utilizan para integrar nuevas aplicaciones con los sistemas de software existentes. Esto aumenta la velocidad de desarrollo, ya que no hay que escribir cada funcionalidad desde cero. Puede utilizar las API para aprovechar el código existente.
2. Innovación <br>
Sectores enteros pueden cambiar con la llegada de una nueva aplicación. Las empresas deben responder con rapidez y respaldar la rápida implementación de servicios innovadores. Para ello, pueden hacer cambios en la API sin tener que reescribir todo el código.
3. Ampliación<br>
Las API presentan una oportunidad única para que las empresas satisfagan las necesidades de sus clientes en diferentes plataformas. Por ejemplo, la API de mapas permite la integración de información de los mapas a través de sitios web, Android, iOS, etc. Cualquier empresa puede dar un acceso similar a sus bases de datos internas mediante el uso de API gratuitas o de pago.
4. Facilidad de mantenimiento<br>
La API actúa como una puerta de enlace entre dos sistemas. Cada sistema está obligado a hacer cambios internos para que la API no se vea afectada. De este modo, cualquier cambio futuro que haga una de las partes en el código no afectará a la otra.

Todo esto es solo un pequeño resumen acerca de los API, pero en realidad falta mucho por aprender de estos servicios. Si te gustaría saber aún más acerca de las API, te invito a visitar el siguiente enlace. De donde se obtuvo la información presentada anteriormente.<br>

[AWS ¿Qué es un API?](https://aws.amazon.com/es/what-is/api/#:~:text=API%20significa%20%E2%80%9Cinterfaz%20de%20programaci%C3%B3n,de%20servicio%20entre%20dos%20aplicaciones.)

<br>Ahora, veamos conceptos básicos acerca de las tecnologías que estaremos utilizando<br>



### ¿Qué es Swagger?  <img align="center" alt="SWAGGER" height="50" width="50"  src="https://user-images.githubusercontent.com/99369122/172023668-f18aa64d-c68f-447f-809a-f85c37b8ca5b.png"/>

Swagger es un conjunto de herramientas de software de código abierto para diseñar, construir, documentar, y utilizar servicios web RESTful. Fue desarrollado por SmartBear Software e incluye documentación automatizada, generación de código, y generación de casos de prueba
En otras palabras, es un lenguaje de descripción de REST APIs. Nosotros vamos a estar utilizando Swagger para crear la definición de nuestra API

Para más información te invito a pasar al sitio oficial de Swagger<br><br>
Sitio oficial:   [https://swagger.io/](https://swagger.io/)

### ¿Qué es Node.Js? <img align="center" alt="NODE" height="50" width="50" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg" />  

Node.js es un entorno en tiempo de ejecución multiplataforma, de código abierto, para la capa del servidor (pero no limitándose a ello) basado en el lenguaje de programación JavaScript, asíncrono, con E/S de datos en una arquitectura orientada a eventos y basado en el motor V8 de Google. Fue creado con el enfoque de ser útil en la creación de programas de red altamente escalables, como, por ejemplo, servidores web.

Para más información te invito a pasar al sitio oficial de Node<br><br>
Sitio oficial:   [https://nodejs.org/es/](https://nodejs.org/es/)


### ¿Qué es Express? <img align="center" alt="EXPRESS" height="50" width="50"  src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/express/express-original-wordmark.svg" />

Express es un framework de NodeJS que proporciona características amplias para la creación de aplicaciones web y móviles. Se utiliza para crear desde una sola página, multi páginas, hasta  aplicaciones web híbridas. Es una capa construida en NodeJS que ayuda a administrar servidores y rutas. Express fue creado para hacer API y aplicaciones web con facilidad,

Cuando hacemos uso de rutas en Express tenemos acceso a:

- request, -->> Que son las peticiones que realiza el cliente o que se realizan desde el front-end.
- response -->> Es un objeto que nos sirve para enviar nuestra respuesta, puedo ser por ejemplo, un status 404, un 202, o el mensaje que devolvemos en la data.
- next    --->> Esta es una función que hace referencia a que el programa continue, si se cumplen ciertas condiciones, como su nombre lo dice con la siguiente  función.

Para más información te invito a pasar al sitio oficial de Express<br><br>
Sitio oficial:   [https://expressjs.com/es/](https://expressjs.com/es/)

### ¿Qué es SQL? <img align="center" alt="MYSQL" height="50" width="50"  src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original-wordmark.svg" />

SQL es un acrónimo en inglés para Structured Query Language.  Un Lenguaje de Consulta Estructurado. Es un tipo de lenguaje de programación que te permite manipular y descargar datos de una base de datos relacional.  Una de sus principales características es el manejo del álgebra y el cálculo relacional para efectuar consultas con el fin de recuperar, de forma sencilla, información de bases de datos, así como realizar cambios en ellas. Es utilizado en la mayoría de las empresas que almacenan datos en una base de datos. Ha sido y sigue siendo el lenguaje de programación más usado para bases de datos relacionales.

Para más información te invito a pasar al sitio oficial de MySQL<br><br>
Sitio oficial:   [https://www.mysql.com/](https://www.mysql.com/)

### ¿Qué Azure? <img align="center" alt="AZURE" height="50" width="50"  src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/azure/azure-original-wordmark.svg" /> 

Microsoft Azure  es un servicio de computación en la nube creado por Microsoft para construir, probar, desplegar y administrar aplicaciones y servicios mediante el uso de sus centros de datos. Proporciona software como servicio (SaaS), plataforma como servicio (PaaS) e infraestructura como servicio (IaaS) y es compatible con muchos lenguajes, herramientas y marcos de programación diferentes, incluidos software y sistemas específicos de Microsoft y de terceros.

Para más información te invito a pasar al sitio oficial de Azure<br><br>
Sitio oficial:   [https://azure.microsoft.com/es-es/](https://azure.microsoft.com/es-es/)


<hr>

## Desarrollo 

Para realizar este proyecto vamos a ir mostrando paso a paso cada uno de los procesos, desde la definición de nuestra API hasta la implementación de la misma en Azure.

Para esto, vamos a dividir el proyecto, en varios proyectos terminados y funcionales, pero en cada paso lo iremos escalando un poco más. Cada paso estará contenido en una carpeta dentro de este mismo proyecto. 

Con base en lo anterior, los pasos que seguiremos son los siguientes:

- [Definición del REST-API (Swagger)](definicion.md)

En este paso, definiremos la estructura de nuestro API, por ejemplo, cuáles serán sus END-POINT, cómo y qué tipos de datos debemos mandarle a nuestra API para la correcta conexión con ésta, todo esto lo estaremos realizando con ayuda del software de Swagger

- [Desarrollo del REST-API con Node.js](desarrollo.md)

Una vez teniendo bien definida nuestro API, pasaremos a implementar nuestro API con base a la definición realizada, esto lo haremos en Node.js. Esta API va a tener una "base de datos local", vamos a almacenar los datos dentro de un array dentro de nuestra misma API. Pero no te preocupes conforma vayas avanzando en el proyecto, llegaremos a conectar nuestro API directamente a una base de datos montada sobre Azure.

- [Implementación de un API en un App Services de Azure](implementacion.md)

Una vez teniendo nuestro API funcionando correctamente, vamos a montar nuestro API en la nube un servicio de Azure, para que podamos tener acceso a ésta desde cualquier parte del mundo, y no limitarnos simplemente a nuestro servidor local.

- [Creación de una base de datos en Azure, modificación del API para trabar con DB y vinculación con el API](database.md)

En este apartado vamos primero a crear un servidor dentro de la nube de Azure, para posteriormente crear nuestra base de datos dentro de nuestro servidor. Vamos a modificar nuestro código para poder trabajar y vincular nuestro API con nuestra base de datos.

- [Asignación de API KEY a nuestro REST API](apiKey.md)

Los puntos de conexión de las API hacen que el sistema sea vulnerable a los ataques. La supervisión de las API es crucial para evitar su uso indebido. Por eso, vamos a agregarle a nuestro API un poco de seguridad implementando un API KEY en ésta.

- [Consumo del API desde el front-end](consumo.md)

Finalmente, veremos cómo hacer un sitio desde front-end para ver cómo podemos hacer para consumir nuestro REST-API


