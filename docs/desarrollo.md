# Desarrollo de la definición del API en Node.js (Utilizando base de datos local)

Una vez teniendo la definición de nuestra API, conocemos ahora los end-points con los que deber de contar nuestro REST API, los tipos de datos que debemos enviarle y los tipos de respuesta que esperamos.

## Prerrequisitos
Para continuar con la siguiente parte de nuestro tutorial, necesitamos tener instalado lo siguiente, el enlace de cada programa te lleva directamente a la página oficial de cada uno para que puedas descargarlos, todos de forma gratuita. 

- [Visual Studio Code](https://code.visualstudio.com/)  
- [NODE](https://nodejs.org/es/)
- [POSTMAN](https://www.postman.com/)


##  Inicio del proyecto


1.- Crear una carpeta vacía, en el directo de nuestra preferencia con el nombre de nuestro proyecto. En esta ocasión a la carpeta le puse por nombre PersonasAPILocal, haciendo referencia a que este proyecto se trabajará con una "base de datos" local, como bien lo dice en el título del proyecto, y lo pongo entre comillas porque en realidad vamos a guardar en un array varios objetos con los datos de algunas personas, posteriormente en la [parte 4](./implementacion.md) de este tutorial, lo vamos a vincular con una base de datos en la nube de Azure.<br><br>
![image](https://user-images.githubusercontent.com/99369122/171228427-5e8b944d-7873-4df3-bcde-f64591f29da8.png)<br><br>

2.- Abrimos Visual Studio y arrastramos la carpeta que creamos hacia la parte izquierda de nuestro Visual Studio, quedando de la siguiente manera:<br><br>
![image](https://user-images.githubusercontent.com/99369122/171228969-e60417ab-89e5-4885-8795-ff5d4f728222.png)<br><br>

3.- Vamos a crear un proyecto de **NODE**, para esto, vamos a abrir una nueva terminal en la carpeta de nuestro proyecto. Como ya tenemos abierta en VScode nuestra carpeta del proyecto, entonces simplemente vamos a ir al menú ubicado en la parte de arriba de VScode y vamos a hacer clic en "Terminal" y posteriormente en "New Terminal"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171229708-cf4bc41c-aa72-4d34-a4a2-93c5b0db4d53.png)<br><br>

4.- Una vez abierta la terminal, vamos a escribir el comando<br><br>``` npm init ```<br><br>Este comando es el que nos permite arrancar un nuevo proyecto de Node. Escribimos el comando y posteriormente presionamos la tecla "ENTER"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171231074-f0fc7cd9-b8da-42d0-a3f8-7160d4d7ea3e.png)<br><br>

5.- Después de presionar enter nos aparecerá un "Menú" como el que se muestra a continuación, lo cual nos pide algunos datos acerca de nuestro proyecto como son:  
<ul>
 <li>Name: (Dejaremos el nombre de la carpeta)</li>
 <li>Version: Versión del proyecto</li>
 <li>Description: Podemos agregar una descripción de nuestro proyecto.  </li>
</ul>
 Y algunos más, nosotros lo llenaremos de la siguiente manera. <br><br>
 ![image](https://user-images.githubusercontent.com/99369122/171232716-a353f795-032e-4d4d-94d8-c68458d93a7c.png) <br><br>
 6.- Presionamos "ENTER" y nos aparecerá un JSON con los datos introducidos, verificamos los datos y presionamos nuevamente "ENTER"<br><br>
 ![image](https://user-images.githubusercontent.com/99369122/171233054-6865a649-71db-4717-826c-569c91487db9.png)<br><br>
 7.- Una vez presionado "ENTER", en nuestra carpeta del proyecto se genera automáticamente un archivo llamado "package.json"<br><br>
  ![image](https://user-images.githubusercontent.com/99369122/171233376-12744941-593a-4110-a819-3e168ded835f.png)<br><br>
 8.- Como vamos a desarrollar nuestra API con ayuda de **express**, tenemos ahora que instalar esta dependencia. Para hacer esto, nuevamente vamos a escribir en nuestra terminal el comando:<br><br>
 ``
 npm install express --save
 ``
 <br><br>Ponemos el comando *--save*, porque es una dependencia de nuestro proyecto, no es una dependencia de desarrollo sino que es una dependencia de producción, es decir, para que nuestro proyecto funcione, necesita de express.<br><br> 
 Si se instaló de forma correcto, veremos un mensaje en el terminal parecido a este. <br><br>
 ![image](https://user-images.githubusercontent.com/99369122/171234930-63f8e6d0-ab96-4a1b-9925-35e763ec5acf.png)<br><br>
 También, se creó un archivo llamado "package-lock.json" dentro de la carpeta de nuestro proyecto.<br><br>
 ![image](https://user-images.githubusercontent.com/99369122/171235495-b8749d09-d1bb-43b2-8c6a-73afbfbf8743.png)<br><br>
 
 9.- Vamos a instalar ahora **Nodemon**, el cual es una aplicación que nos ayudará a recargar nuestro servidor en cuanto detecte algún cambio, esta aplicación es de mucha utilidad ya que nos ahorra tiempo por estar deteniendo y ejecutando nuevamente nuestro servidor<br><br>
 ``
 npm i -D nodemon
 ``
 <br><br>
 
 10.- Instalamos ahora **Body-paser** con el siguiente comando: <br><br>
   ``
 npm i body-parser
 ``
  <br><br>Usualmente el cuerpo de una petición (payload), contiene información desde una petición tipo POST o PUT. Los desarrolladores quienes implementamos servidores, requerimos frecuentemente acceso a la información del cuerpo de dicha petición.

   El módulo npm body-parser permite realizar esta tarea. No es necesario programarla. Solo se requiere instalar body-parser y habilitar json() así como url-encode como middlewares para convertir datos a JSON.
 
 
11.- Instalamos ahora **express-validator** con el siguiente comando: <br><br>
   ``
 npm install --save express-validator
 ``
 <br><br>Esta dependencia, nos ayudará al momento de hacer las validaciones en los end-points<br><br>
12.- Vamos a instalar **CORS** el cual nos servirá para poder consumir nuestra API posteriormente desde nuestro Front-end en un navegador. Si no instalamos esta dependencia, si accedemos a la url de nuestro api por ejemplo [https://personasapilocal1.azurewebsites.net/personas](https://personasapilocal1.azurewebsites.net/personas), el navegador SÍ me va mostrar los resultados, pero al momento de hacer un fetch()  dentro de  alguna función que invoque por ejemplo un botón, nos aparecerá el error de CORS es por eso que vamos a instalar de una vez la dependencia<br><br>

 ``
 npm i cors --save
 ``

<br><br>
13.- Por último vamos a crear nuestro archivo de **"index.js"** dentro de la carpeta de nuestro proyecto. Para esto vamos a hacer clic derecho sobre la carpeta de nuestro proyecto y vamos a dar clic en " New File" y le pondremos por nombre *index.js*<br><br>
![image](https://user-images.githubusercontent.com/99369122/171236180-98155f54-9617-4ecd-92a4-dcb2ba783cf7.png)<br><br>



## Montaje del servidor local

1.- Lo primero que haremos es montar un pequeño servidor en nuestra computadora, para poder estar ejecutando nuestro REST-API, para esto vamos a poner el siguiente código en nuestro archivo de *index.js*

```js
const express = require('express'); // Utilizo el módulo de node de express
const path = require('path'); // Utilizo el módulo de node de path
const bodyParser = require('body-parser') // Utilizo el modulo de body parser
const app = express(); // Genero mi aplicación de express simplemente llamando al constructor express()


const port = process.env.port || 8080; // constante para nuestro puerto, es un OR para el caso de  desarrollo en algún servicio o desarrollo local 
app.listen(port, () =>console.log(`Escuchando en el puerto ${port}`))

```
<br><br>
2.- Dentro de nuestro archivo de  *package.json*. Vamos a localizar la línea donde diga "script".<br><br>
![image](https://user-images.githubusercontent.com/99369122/171258320-f75f8848-3aa9-4bb0-bb08-0b70d013c5f1.png)<br><br>
 Y dentro en  "serve" vamos a modificar la parte de:<br><br>
``
"serve": "echo \"Error: no test specified\" && exit 1"
``
<br> <br>
Por: <br> <br>
``
"serve": "nodemon index.js"
``
<br><br>Esto nos va a servir para que nodemon reinicie el servidor cada que realicemos un cambio.

3.- Escribimos ahora en la terminal, el comando<br> <br>
``
npm run serve
``
<br><br> Y ahora sí, si todo salió bien, tendríamos nuestro pequeño servidor local funcionando. En la consola debió aparecer un mensaje como este:<br> <br>
![image](https://user-images.githubusercontent.com/99369122/171257860-eaab73cf-37bd-4d07-81d9-147d1b8baa43.png)

4.- Una vez teniendo nuestro servidor local funcionando, vamos a crear un primer END-POINT muy sencillo antes de pasar a crear los END POINTS de nuestra definición.
Para ello vamos a agregar unas líneas a nuestro código anterior, quedando de la siguiente forma:<br><br>
```js
const express = require('express'); // Utilizo el módulo de node de express
const path = require('path'); // Utilizo el módulo de node de path
const bodyParser = require('body-parser') // Utilizo el modulo de body parser
const app = express(); // Genero mi aplicación de express simplemente llamando al constructor express()

// *****Lineas añadidas***
//Route
app.get('/', (req, res)=>{// Petición de tipo GET para nuestra API
    res.send("Bienvenido a mi API");
})
//*************
 
const port = process.env.port || 8080; // constante para nuestro puerto, es un OR para el caso de  desarrollo en algún servicio o desarrollo local 
app.listen(port, () =>console.log(`Escuchando en el puerto ${port}`))

```
<br><br>Ahora sí, guardamos lo cambios y si todo estuvo bien. Podemos ir a nuestro navegador favorito y visitar [http://localhost:8080/](http://localhost:8080/), que fue el puerto en donde configuramos nuestro servidor. Que como ya sabemos, nuestro navegador por defecto siempre hace peticiones GET <br><br>
![image](https://user-images.githubusercontent.com/99369122/171259737-7bf6e6b8-7b7b-484f-a3f0-245c28febf87.png)<br><br>
¡Felicidades! Ya tenemos nuestra primer API funcionando, aunque no sigue para nada la definición que ya tenemos, a continuación, voy a crear de forma correcta el API que se nos solicita:


## Programación REST API

1.- Lo primero que tenemos que hacer es crear dos carpetas dentro de la carpeta de nuestro proyecto, vamos a crear una carpeta llamada **app** y dentro de esta vamos a crear 4 carpetas, una de nombre **controllers** , otro de nombre **routers**, y otra de nombre **validators** y a su vez dentro de cada  una de estas carpetas, debemos crear un archivo de nombre **personas.js**. La cuarta carpeta tendrá por nombre **herlpers** y dentro, crearemos un archivo llamado **validateHelper.js**.
Quedando de la siguiente manera:<br><br>
![image](https://user-images.githubusercontent.com/99369122/171909932-d6dcfd17-3c06-4ae2-82d4-d30bc47644db.png)<br><br>
Todo esto lo hacemos para tener un código desacoplado y por lo tanto sea más entendible y mantenible.

2.- Dentro de la carpeta **routers** agregar  dentro del archivo **personas.js**, el siguiente código . El código agregado viene con sus respectivos comentarios para mejor entendimiento del mismo.<br><br>

```js
/*HOJA DE RUTAS, en esta hoja vamos a tener el control de todas las rutas de nuestra app*/
const { request } = require('express');
const res = require('express/lib/response');
const { links, json } = require('express/lib/response');
// importo el modulo de express específicamente coon el constructor que tiene express de .Router()
const endPoints = require('express').Router(); 
//importo las funciones desde la ruta /controllers/personas.js
const {obtenerPersonas, obtenerPersona,añadirPersona,actualizarPersona,eliminarPersona }= require('../controllers/personas')
const {validarDatos}= require('../validators/personas')

/* ENDPOINTS */
/*Todas las funciones como por ejemplo obtenerPersonas, realizan toda su funcionalidad
en la hoja ../controllers/personas') se hace de esta forma para tener mas control en nuestro código */


//Obtener todos los datos de todas las personas de la lista
endPoints.get('/',obtenerPersonas)

//Obtener los datos una persona de acuerdo a su Id
endPoints.get('/:id', obtenerPersona)

/* Agregar una nueva persona al arreglo, pero antes de añadir valido los datos, con ayuda de ValidaDatos
en este caso Validar datos es un Middleware que intercepta el mensaje, sino obtuvo ningún error deja a pasar
 hacia añadirPersona con el next() que tiene internamente , si obtuvo alguno arroja el error*/
endPoints.post('/', validarDatos,añadirPersona)

/*Modificar los datos de una persona,pero antes de añadir valido los datos, con ayuda de ValidaDatos
en este caso ValidarDatos es un Middleware que intercepta el mensaje, deja a pasar hacia añadirPersona
con el next() que tiene internamente */
endPoints.put('/:id',validarDatos, actualizarPersona)

//Eliminar a una persona
endPoints.delete('/:id', eliminarPersona )

// Exporto todos mis endPoints para que los "reconozca" en index.html
module.exports = endPoints;



```

<br><br>

3.- Dentro de la carpeta **controllers**  agregar el siguiente código en el archivo **personas.js**. El código agregado viene con sus respectivos comentarios para mejor entendimiento del mismo.<br><br>
```js
const { response } = require('express');
const { request } = require('express');

/* personas es el objeto en donde tenemos nuestra "base de datos local"
Todos los cambios de post,put,delete, solo funcionan mientras el servidor está funcionando,
en caso de reiniciar el servidor regresara a los valores actuales*/

let personas = [
    {
        "id": 1,
        "Nombre": "Roberto",
        "Apellido": "Peredo",
        "Edad": 25,
        "Mail": "roberto@correo.com",
        "Celular": 2222222222
      },
      {
        "id": 2,
        "Nombre": "Maite",
        "Apellido": "Cruz",
        "Edad": 25,
        "Mail": "maite@correo.com",
        "Celular": 5555555555
      },
      {
        "id": 3,
        "Nombre": "Juan",
        "Apellido": "Perez",
        "Edad": 25,
        "Mail": "Juan@correo.com",
        "Celular": 6666666666
      }
];

//Obtener todas las personas de la lista

const obtenerPersonas = [(request, response)=>{

    //Validamos si el array está vacío
    if(personas.length===0){
        //En caso de estar vacío, mandamos el sig mensaje
        response.status(415).json({error: "No existe  ninguna persona registrada"});
     }
    else {
        //Sino está vació desplegamos la lista de todas las personas
    response.json(personas)}

}]



//Obtener una  personas de la lista de acuerdo a su ID
const obtenerPersona =[(request,response)=>{
    /*recupero el id de la persona haciendo un de-structur. La idea es crear una variable llamada id, 
    que está contenida con el mismo nombre id dentro de parms*/
    const {id} = request.params 
    
    //Hago la validación para ver si algún objeto de mi arreglo personas tiene el id igual al requerido(devuelve un bool)
    if(personas.some( persona => persona.id === parseInt(id) )){  

        /*Si existe ese id en mi array, entonces: 
        Encuentro el id que corresponda al  requerido y lo devuelvo en la response de mi api
        Como mi variable id viene en string con parseInt convertimos a entero id, porque el id 
        dentro del array personas es int*/        
       response.json(personas.find( persona => persona.id === parseInt(id) ));                                                                  } 
    else{
        //Sino existe imprimimos el mensaje
        response.status(410).json({error: "Este id no existe"});
    }
}]



//Añadir una nueva persona a la lista
const añadirPersona = [(request,response)=>{ 
/*Todo esto se ejecuta solo si los datos fueron validados. Es decir, validarDatos dentro de
/validator/personas.js continuó con  next()*/


    //Crea una variable tipo objeto, llamada nuevaPersona con los datos mandados en el body
    const nuevaPersona = {
        id: request.body.id,
        Nombre: request.body.Nombre,
        Apellido: request.body.Apellido,
        Edad: request.body.Edad,
        Mail: request.body.Mail,
        Celular: request.body.Celular
    }
    //Verifico si el id mandado desde la url ya existe dentro de mi arreglo de personas
    if(personas.some( persona => persona.id === parseInt(nuevaPersona.id) )){
        //Si existe, mando el mensaje
        response.status(411).json({error: "Este id ya existe"});
    }
    else{
        //Sino existe,lo agrego con push al arreglo de personas y mando en la respuesta el obj añadido
        personas.push(nuevaPersona);
        response.json(nuevaPersona);       
    }

}]

  
//Actualizar una nueva persona de la lista
const actualizarPersona = [  

    /*Todo esto se ejecuta solo si los datos fueron validados. Es decir, validarDatos dentro de
/validator/personas.js continuó con  next() */

    (request,response)=>{

    //Si no encontró ningún error en la validación entonces:
    /*recupero el id de la persona haciendo un de-structur. La idea es crear una variable llamada id, 
    que está contenida con el mismo nombre id dentro de parms*/
    const {id} = request.params

    //Verifico si el id mandado existe dentro de mi arreglo alguna persona dentro de mi array de personas
    if(personas.some( persona => persona.id === parseInt(id) )){ 
    
    /* Si la persona sí existe, entonces almaceno en una variable llamada nuevaPersona, de tipo object,
    todos los valores que provienen del body  */
    const nuevaPersona = {
        id: request.body.id,
        Nombre: request.body.Nombre,
        Apellido: request.body.Apellido,
        Edad: request.body.Edad,
        Mail: request.body.Mail,
        Celular: request.body.Celular
    }    

    //Asigno a personaAModificar todo el objeto que hace match con el id
    personaAModificar= personas.find( persona => persona.id === parseInt(id))
   // Modifico la persona con los nuevos datos
    personaAModificar.id =nuevaPersona.id
    personaAModificar.Nombre =nuevaPersona.Nombre
    personaAModificar.Apellido =nuevaPersona.Apellido
    personaAModificar.Edad =nuevaPersona.Edad
    personaAModificar.Mail =nuevaPersona.Mail
    personaAModificar.Celular =nuevaPersona.Celular
    
    //Mando en la respuesta la persona con los datos modificados
    response.json(personaAModificar)
} 
     else{
         //Si el id no existe, mando el mensaje
         response.status(410).json({error: "Este id no existe"});
     }
    
}]

const eliminarPersona = [(request,response)=>{
    /*recupero el id de la persona haciendo un de-structur. La idea es crear una variable llamada id, 
    que está contenida con el mismo nombre id dentro de parms*/
    const {id} = request.params 

    //Verifico si el id mandado existe dentro de mi arreglo alguna persona dentro de mi array de personas
    if(personas.some( persona => persona.id === parseInt(id) )){
//Si existe, entonces 'filtro' mi array personas y solo dejo las personas que tengan un id diferente al introducido
      personas = personas.filter(persona => persona.id !== parseInt(id))      

      //Mando en mi respuesta el id de la persona eliminada
      response.json(id);
 }
     else {
         //Sino el id no existe, mando el mensaje
         response.status(410).json({error: "Este id no existe"});;
     }

    
}]

//exporto las funciones hacia mi ruta /routers/personas.js
module.exports = {obtenerPersonas, obtenerPersona,añadirPersona, actualizarPersona, eliminarPersona}


```



<br><br>Estos archivos, trabajan en conjunto para generar los ENDPOINT y las validaciones correspondientes para cada solicitud. Noten que como ya lo habíamos comentado, la "base de datos" es un arreglo dentro del mismo proyecto, por lo que, al reiniciar el servidor, todos los cambios se perderán y el arreglo regresará a su contenido original. Posteriormente en la [parte 4](./implementacion.md) de este tutorial, lo vamos a vincular con una base de datos en la nube de Azure. <br><br>

4.-Dentro de la carpeta **validators**  agregar el siguiente código en el archivo **personas.js**. El código agregado viene con sus respectivos comentarios para mejor entendimiento del mismo.<br><br>

```js

const { response } = require('express');
const { request } = require('express');
const res = require('express/lib/response');

/*Creamos una 'variable' body  que son de express-validator, las cuales nos ayudarán a realizar las validaciones */
const { body} = require('express-validator');

/* importo la función validateResult desde  helpers/validateHelperes un helper para seguir el proceso
o mandar un error*/
const {validateResult}= require('../helpers/validateHelper') 

const validarDatos = [
     /*Con ayuda de las variables body  y validationResult creadas con 'express-validator',
    validamos que los elementos que viene en el body existan, se llamen de la forma correcta y
    sean del tipo correcto. NOTEN que es necesario que vengan todos los datos para realizar la modificación*/
    body('id').exists().isNumeric(), // en la definción de nuestro RESTAPI no pedimos el id requerido, esto es porque en nuestra base de datos el id será auto incremental, pero como lo tenemos en un arreglo, nosotros debemos asignarle el id.Mas adelante cuando nos conectamos a la base de datos, este campo desaparecerá
    body('Nombre').exists().isLength({ min: 3 }),
    body('Apellido').exists().isLength({ min: 3 }),
    body('Edad').exists().isNumeric(), 
    body('Mail').exists().isEmail(), 
    body('Celular').exists().isNumeric(), 

    (request,response, next)=>{    
        /* Desacoplamos esta función para tener mejor control, entonces la mandamos a llamar y le pasamos los parámetros.
         nos da un resultado si consigue todas las validaciones, si consigue un error  nos retorna el error  
        sino continua el flujo con next(). Asi que simplemente la mandamos a llamar desde helpers/validateHelper */ 
        validateResult(request,response, next)
    }
]

module.exports = {validarDatos}//exportamos la constante para hacer uso en /routers/personajes.js como un  Middleware
```
<br><br>
5.- Dentro de la carpeta **helpers**  agregar el siguiente código en el archivo **validateHelper.js**. El código agregado viene con sus respectivos comentarios para mejor entendimiento del mismo.<br><br>

```js
const { validationResult } = require('express-validator');

//Construimos una función con los parámetros que nos pasan desde /validators/personas.js

const validateResult = (request,response, next) =>{

    try{
        //si no obtuvimos ninguna error continuamos con el flujo next()
        validationResult(request).throw()
        return next()
    }catch(error){
        // si obtuvimos algún error lo regresamos en la respuesta
       response.status(400).json({ errors: error.array() });
    }
}

module.exports={validateResult}

```
<br><br>
6.- Finalmente en nuestro archivo principal **index.js** vamos a agregar el siguiente código, en donde vinculamos todos los códigos anteriores. <br><br>

```js
const express = require('express'); // Utilizo el módulo de express de Node
const path = require('path'); // Utilizo el módulo path de Node
const bodyParser = require('body-parser') // Utilizo el modulo de body parser
const app = express(); // Genero mi aplicación de express simplemente llamando al constructor express()
const endPoints = require('./app/routers/personas')/*Importo  el modulo(en este caso endPoint) que exporte
 desde la ruta ./app/routers/personas */
 const cors = require('cors')//Utilizo el módulo de cors


app.use(cors());//le damos acceso a nuestro API desde cualquier 'origen'

//Route "Pagina principal" al momento de conectarse al API, con un método GET que el navegador hace por default
app.get('/', (req, res)=>{
    res.send("Bienvenido a mi API");
})

//Middleware
//Body Parser (Para pasar a json los endpoint tipo post), se ejecuta antes de llegar al siguiente Middleware
app.use(bodyParser.urlencoded({extended: true}));
app.use(bodyParser.json());


 //Middleware  (registra una ruta) y ejecuta lo que viene dentro de endPoints
app.use('/personas', endPoints)
/*Si tuvieramos otra ruta en nuestra api como por ejemplo '/objetos', debemos crear las respectivas hojas
de las carpetas controllers y routers con el mismo nombre 'objetos'*/


/* constante para nuestro puerto, es un una condición OR para el caso de  desarrollo en algún servicio
 o desarrollo local (nuestro caso) */
const port = process.env.port || 8080; 
app.listen(port, () =>console.log(`Escuchando en el puerto ${port}`))

```
<br><br>Y listo, finalmente tenemos nuestro REST-API construido con Node.js y Express con base a la definición dada en Swagger. Ahora lo siguiente sería realizar pruebas para cada endpoint, para esto nos ayudaremos de POSTMAN.

## Pruebas de funcionamiento de los ENDPOINT utilizando POSTMAN

Para realizar las pruebas de funcionamiento, lo primero que debemos hacer es tener corriendo nuestro proyecto, para esto como ya sabemos debemos escribir en la terminal el comando<br><br>

``
npm run serve
``
 <br><br>Una vez teniendo nuestro servidor listo, vamos a realizar las pruebas en el programa de POSTMAN, para esto te voy a dejar aquí el archivo, para que tú mismo puedas realizar las pruebas. Basta con descargar el archivo e importarlo en POSTMAN. ¡No olvides hacer las solicitudes con base a la definición de nuestra API! Te dejo [AQUÍ](https://app.swaggerhub.com/apis-docs/RobertoPeredo/personas-api/1.0.0) la definición de nuestro REST-API para que tú mismo puedas realizar las pruebas.
 
 
  [ARCHIVO PARA PRUEBAS EN POSTMAN](https://github.com/RobertoPeredo/REST-API/tree/main/2.%20Desarrollo%20del%20API%20en%20Node.js%20(%20Con%20base%20de%20datos%20local)/POSTMAN)
 
 1. Prueba de la página principal del API<br><br>
 ![image](https://user-images.githubusercontent.com/99369122/171510656-1b04312f-82fb-45df-8628-e7d53a585746.png)<br><br>
2. Prueba del método GET que nos devuelve todas las personas<br><br>
![image](https://user-images.githubusercontent.com/99369122/171510872-33c37db2-bf86-43b6-9371-d21550138abc.png)<br><br>
3. Prueba del método GET que nos devuelve una persona por su ID<br><br>
 ![image](https://user-images.githubusercontent.com/99369122/171510960-4911bbc5-9723-48a5-a37d-14b9a5e0a407.png)<br><br>
 ERROR sino existe una persona con ese ID<br><br>
 ![image](https://user-images.githubusercontent.com/99369122/171511023-fef403f8-8191-4e60-8d25-3da9e3624859.png)<br><br>
4. Prueba del método POST que agrega una persona a la lista<br><br>
![image](https://user-images.githubusercontent.com/99369122/171511270-c9987861-c1eb-4a68-948a-57b71ece0783.png)<br><br>
Si queremos agregar un ID que ya existe<br><br>
![image](https://user-images.githubusercontent.com/99369122/171511354-7aadb60b-4b73-4fd8-a4fe-534dd6705425.png)<br><br>
Si hace falta agregar en el body algún dato de la persona<br><br>
![image](https://user-images.githubusercontent.com/99369122/171511448-0a61a581-1874-457e-bb97-f6c0ca63f3c2.png)<br><br>
5. Prueba del método PUT que modifica los datos de una persona<br><br>
![image](https://user-images.githubusercontent.com/99369122/171511565-66d5c9e4-540d-4f11-b650-76eae505f286.png)<br><br>
Si queremos modificar una id que no exista<br><br>
![image](https://user-images.githubusercontent.com/99369122/171511656-873f88c4-ec9d-4d60-9f87-bdf5e3d4a4ff.png)<br><br>
Si queremos modificar, pero hace falta un dato en el body<br><br>
![image](https://user-images.githubusercontent.com/99369122/171511748-621dbf1b-1348-43f2-853d-45900026bb3d.png)<br><br>
6. Y Por último si queremos eliminar a una persona de la lista<br><br>
![image](https://user-images.githubusercontent.com/99369122/171511824-7629afe5-0b62-42d8-80c0-d09ea3b1e158.png)<br><br>
Si queremos eliminar una persona, pero no existe el id<br><br>
![image](https://user-images.githubusercontent.com/99369122/171511906-ee79b690-9d00-481a-9f18-e247aea04366.png)<br><br>

Y listo, tenemos todas las validaciones realizadas y por consiguiente un REST API funcionando a la perfección.

El enlace de repositorio completo, que incluye todo el código es el siguiente:
-------->>>>>>>>>> [LINK DEL REPOSITORIO](https://github.com/RobertoPeredo/PersonasAPILocal)


Ahora, la siguiente parte del tutorial, consiste en montar este API en un App Service de Azure para poder acceder a éste desde cualquier lugar.



 
 
 
 


 
 




