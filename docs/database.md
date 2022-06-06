# Creación de una base de datos en Azure, modificación del API para trabar con DB y vinculación con el API


## Creación de un Servidor en Azure

Para hacer la creación de un servidor de Azure, lo primero que tenemos que hacer es tener una cuenta en [portal.azure.com.](https://portal.azure.com.) Yo por ejemplo, creé mi cuenta con mi correo estudiantil, el cual me otorga $100 dólares para poder ocupar en los servicios de Azure.

Una vez con nuestra cuenta logueada, vamos a poner en el buscador "Servidores de Azure Database for MySQL" y haremos clic en este que aparece en la imagen<br><br>
![image](https://user-images.githubusercontent.com/99369122/171561181-f5807408-3624-445c-9c81-db1ede34a8d3.png)<br><br>
Nos aparecerá la siguiente venta y haremos clic en "Crear Azure Database para el servidor MySQL"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171561599-9e7c9aec-ee57-4cb4-8366-4495efd87db4.png)
Nos aparecerá una ventana como la siguiente y vamos a seleccionar en el apartado  *Tipo de recurso* la opción de  "Servidor flexible" y vamos a dar clic en "crear"
![image](https://user-images.githubusercontent.com/99369122/171700473-f52a4ec2-e758-470c-a249-55c8513d4d5a.png)

## Configuración del servidor
Se nos abrirá una ventana en donde realizaremos las siguientes configuraciones.

#### Detalles del proyecto
En este apartado seleccionaremos "Azure for Students" en el apartado de *Suscripción* y en *Grupo de recursos* seleccionaremos "DemoWeb", el cual ya habíamos creado con anterioridad en la [sección 4](implementacion.md) de este tutorial.<br><br>
![image](https://user-images.githubusercontent.com/99369122/171706258-1216f11f-495e-4206-a39f-2775d46a4669.png)

#### Detalles del servidor

Asignaremos el *Nombre del servidor*, en este caso yo le pondré por nombre "rest-api-server", las demás configuraciones las colocaremos como se muestra en la imagen, y haremos clic en **"Configurar servidor"**<br><br>
![image](https://user-images.githubusercontent.com/99369122/171708597-46763149-c360-4255-a283-673b34434595.png)<br><br>
Se nos abrirá otra ventana<br><br>
**NOTA IMPORTANTE: CREAR UN SERVIDOR DE ESTE TIPO TIENE UN COSTO MENSUAL, NOSOTROS LO VAMOS A CONFIGURAR TRATANDO DE HACERLO LO MAS ECONÓMICO POSIBLE, COMO SOLO ES UN PROYECTO CON FINES DE APRENDIZAJE, NO NECESITAMOS MUCHOS RECURSOS. AUN ASÍ, TE VOY A COMPARTIR ESTE PROYECTO FUNCIONANDO PARA QUE TU PUEDAS REALIZAR TUS PROPIAS PRUEBAS, SI LO REVISAS DESPUES DE UN AÑO A PARTIR DE QUE SE REALIZÓ ESTE PROYECTO (02/06/2022) ES PROBABLE QUE LOS CREDITOS QUE NOS PROPORCIONÓ AZURE YA ESTÉN VENCIDOS Y POR LO TANTO EL SERVIDOR YA NO ESTÉ ACTIVO**

#### Proceso

En este apartado solo modificaremos el *Tamaño de proceso* y seleccionaremos la opción "Standard_B1s(1 núcleo virtual, 1 memoria GiB, 400 IPOS máxima)"
![image](https://user-images.githubusercontent.com/99369122/171717784-ff55a3e4-dab9-4869-82a5-037a2f892d37.png)

#### Almacenamiento
En *Storage size (in GiB)* Seleccionaremos "20" y en *IOPS* pondremos "360"
Y listo, las demás configuraciones las dejaremos por defecto. Y haremos clic en "Guardar"
![image](https://user-images.githubusercontent.com/99369122/171719612-f73af1e9-67e0-4076-b953-3b231bec6a49.png)

¡Podemos observar que conseguimos hacer un poco más barato el costo del servidor!<br><br>
![image](https://user-images.githubusercontent.com/99369122/171719776-361c76ce-6ff3-464d-8faa-e8a56570e11c.png)

#### Cuenta de administrador

Por último, vamos a configurar el usuario de nuestro servidor para poder acceder a éste.

En *Nombre de usuario de administrador* vamos a colocar un nombre para nuestro administrador, en este caso voy a colocar "root1" y vamos a crear una contraseña. Y haremos clic en " Siguiente".<br>
 **Es importante guardas estos datos porque los vamos a estar utilizando más adelante para poder conectarnos a nuestro servidor**
![image](https://user-images.githubusercontent.com/99369122/171720464-13b2f73c-0cce-4507-86da-424fe451f8a3.png)

### Redes 

En esta ventana bajaremos hasta el apartado "Reglas de firewall"

#### Reglas de firewall
Vamos seleccionar la opción "Permitir” acceso público a este servidor desde cualquier servicio de Azure dentro de Azure" y hacer clic en  "+ Agregar dirección IP del cliente actual"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171721159-7ad85885-265d-4c74-8912-4528729fdace.png)<br><br>
Nos aseguramos de que se haya agregado en la tabla de abajo<br><br>
![image](https://user-images.githubusercontent.com/99369122/171721505-cccb88fc-8b7e-4846-9ee4-c8c22d120da3.png)<br><br>
Las demás configuraciones las dejaremos por defecto y haremos clic en "Revisar y crear"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171721880-6b9baf31-f0dc-4c17-bfd9-630f2b4d3e03.png)<br><br>
Nos aparecerá una venta como esta y haremos con en "crear"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171722475-7f29e0d1-4d4f-4714-af23-03173b24e7e5.png)
Posteriormente la implementación de nuestro servidor comenzará, aquí debemos esperar unos minutos a que termine la implementación
![image](https://user-images.githubusercontent.com/99369122/171723033-d5401b40-23c0-4c9c-8c0c-e67b614abe82.png)
Una vez terminada la implementación, nos aparecerá una ventana como la siguiente, y haremos clic sobre " Ir al recurso"
![image](https://user-images.githubusercontent.com/99369122/171725000-612f670e-7ada-44fa-a90d-e02d181d2a9c.png)



#### Des habilitación de la aplicación de SSL

La siguiente información fue sacada directamente de la  documentación de Microsoft

*"El servidor flexible de Azure Database for MySQL admite la conexión de las aplicaciones cliente al servidor MySQL mediante el cifrado de la Capa de sockets seguros (SSL) con la Seguridad de la capa de transporte (TLS). TLS es un protocolo estándar del sector que garantiza conexiones de red cifradas entre el servidor de bases de datos y las aplicaciones cliente, lo que le permite ajustarse a los requisitos de cumplimiento.

Si la aplicación cliente no admite conexiones cifradas, tendrá que deshabilitar la obligatoriedad de conexiones cifradas en el servidor flexible. Para deshabilitar la obligatoriedad de conexiones cifradas, debe establecer el parámetro de servidor require_secure_transport en OFF"*

Para más información acerca de SSL, te invito a pasar a la página de Microsoft para que te informes mas [LINK](https://docs.microsoft.com/es-es/azure/mysql/flexible-server/how-to-connect-tls-ssl#disable-ssl-enforcement-on-your-flexible-server)

Como ya lo leyeron arriba, nuestra aplicación cliente no va a admitir conexiones cifradas, por lo tanto tenemos que deshabilitarlas, para esto dentro del recurso de nuestro servidor vamos a ir a la barra del lado izquierdo y buscaremos la opción *Parámetros del servidor* y haremos clic sobre éste<br><br>
![image](https://user-images.githubusercontent.com/99369122/171725276-ba058356-5eb0-4a40-bdce-ef3b768630c6.png)<br><br>
Se nos abrirá una ventana y en el buscador colocaremos "require_secure_transport", cambiaremos la opción a "OFF" y daremos clic en "Guardar"
![image](https://user-images.githubusercontent.com/99369122/171725682-8e2a4901-bf13-45d0-b927-f9f8c0c866e8.png)
Esperemos nuevamente que termine la implementación y una vez terminada, vamos a ir a la opción de la barra de lado izquierdo que dice "Información general" vamos a dar clic y se nos abrirá una ventana como esta: De aquí vamos a copiar el *Nombre del servidor* que es el que vamos a estar utilizando para poder conectarnos a nuestro servidor.
![image](https://user-images.githubusercontent.com/99369122/171734251-fb00fc5c-b421-482c-9179-a2b7454f69c5.png)
En este caso el enlace para el servidor que montamos es: [rest-api-server.mysql.database.azure.com](rest-api-server.mysql.database.azure.com)
estamos listo para crear nuestra base de datos!!!


## Creación de base de datos y tabla


Una vez implementados nuestros cambios, vamos a hacer clic en  " Ir al recurso" y una vez aquí, vamos a acceder a la terminal dentro de nuestro portal de Azure, para esto haremos clic sobre este icono ubicado en la parte superior de nuestra ventana
![image](https://user-images.githubusercontent.com/99369122/171726907-630044dc-ee1e-4eaa-807d-86656b3841ed.png)
En la parte de abajo nos aparecerá una ventana  como esta y haremos clic sobre " Crear almacenamiento"
![image](https://user-images.githubusercontent.com/99369122/171727800-feab8c8d-9bef-4a16-9b16-a873448f3ff0.png)
Esperamos a que termine de cargar y finalmente nos aparecerá una ventana como esta:
![image](https://user-images.githubusercontent.com/99369122/171727961-565c8a67-c36c-4270-95f2-12f583c807a5.png)
¡Muy bien! Ahora sí estamos listos para crear nuestra base de datos. 

Para crear nuestra base de datos tenemos dos opciones, usar la terminal que nos ofrece el propio portal de Azure, o hacer uso de [MySQL Workbench](https://www.mysql.com/products/workbench/). Nosotros en esta ocasión vamos a utilizar la terminal de Azure, pero si tu decides hacerla haciendo uso de MySQL Workbench, aquí te dejo la [DOCUMENTACIÓN](https://docs.microsoft.com/es-es/azure/mysql/flexible-server/connect-workbench) necesaria de parte de Microsoft para realizar la conexión

Para crear nuestra base de datos primero realizaremos la conexión al servidor con MySQL, para esto vamos a ingresar la siguiente línea de código en nuestra terminal, en donde *host* es el  nombre del servidor (que copiamos anteriormente) y *user* el nombre del administrador que configuramos cuando creamos el servidor

```sql
mysql --host=rest-api-server.mysql.database.azure.com --user=root1 -p
```



![image](https://user-images.githubusercontent.com/99369122/171735318-21fa11cb-45ac-41e7-9b29-8060b4b1dfde.png)


Después nos va a pedir nuestra contraseña, aquí es muy importante notar, que vamos a escribir nuestra contraseña pero no se va a ver que estamos escribiendo, es decir el curso seguirá igual, pero en realidad sí estamos escribiendo. Una vez insertada nuestra contraseña correctamente vamos a presionar "enter" y nos aparecerá algo así
![image](https://user-images.githubusercontent.com/99369122/171735426-e116ff1b-b93c-48c2-9444-e2257115a966.png)

Para crear nuestra base de datos insertaremos el siguiente comando, donde "baseDeDatosDemoWeb" es el nombre que decidí para mi base datos, pueden sustituirlo por el nombre de su preferencia
```sql
create database baseDeDatosDemoWeb;
```
Vamos a recibir esta respuesta<br><br>
![image](https://user-images.githubusercontent.com/99369122/171742905-e2c23fa6-0b05-48dd-9423-6ba4148e69f2.png)

Ahora debemos hacer uso de nuestra base de datos, para esto vamos a insertar el siguiente comando, en donde baseDeDatosDemoWeb, es el nombre de la base de datos que queremos utilizar:
```sql

USE baseDeDatosDemoWeb;
```
Vamos a recibir la siguiente respuesta<br><br>
![image](https://user-images.githubusercontent.com/99369122/171744844-1286a883-2668-4968-a7b8-efcb411515fa.png)


Una vez dentro de nuestra base de datos, vamos a crear dentro una tabla, para esto vamos a insertar el siguiente código. Aquí es muy importante que el nombre de los campo coincidan con los nombres que asignamos en el Schema de nuestra [definición](https://app.swaggerhub.com/apis-docs/RobertoPeredo/personas-api/1.0.0#/Persona). Por otro lado *"persona"* es el nombre que decidí para la tabla, ustedes pueden poner el nombre de su preferencia.

```sql
CREATE TABLE personas (
    id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    Nombre VARCHAR(20),
    Apellido VARCHAR(20),
    Edad INT UNSIGNED,
    Mail VARCHAR(40),
    Celular BIGINT UNSIGNED   
);

```
Vamos a recibir la siguiente respuesta:<br><br>
![image](https://user-images.githubusercontent.com/99369122/171744991-3099101e-1da8-46ce-b52c-33ae0c81fb7a.png)<br><br>
Y ahora vamos a insertar unos datos de forma manual, para tener algo con que comenzar, posteriormente todo lo haremos directamente desde nuestro REST-API.<br><br>
Para insertar los datos vamos a escribir el siguiente código en nuestro terminal

```sql
INSERT INTO personas (Nombre, Apellido, Edad, Mail,Celular) VALUES 
 ('Roberto', 'Carlos', 25, 'roberto@correo.com', 2222222222), 
 ('Carlos', 'Guzman', 24, 'carlos@correo.com',6666666666), 
 ('Maite', 'Cruz', 23, 'maite@correo.com', 1111111111); 
```
Recibiremos una respuesta como esta<br><br>
![image](https://user-images.githubusercontent.com/99369122/171746758-62905e28-04c1-48b3-9eca-3338bb878d34.png)<br><br>
 Por último, verificamos los datos que introducimos, para esto utilizamos  el comando<br><br>
```sql
SELECT * from personas;
```
Recibiremos esta respuesta<br><br>
![image](https://user-images.githubusercontent.com/99369122/171746943-3d408ee2-a818-41eb-8e66-be70cb1b1e27.png)

¡¡Y ahora sí!! Tenemos nuestro servidor, nuestra base de datos y nuestra tabla trabajando perfectamente.
Ahora lo que sigue es modificar nuestro código del API, para que pueda tener acceso a nuestro servidor


## Cambios en el código de nuestro REST-API

### Añadir dependencias

Como bien sabemos, anteriormente teníamos nuestra "base de datos" en un arreglo dentro de nuestra aplicación, pero como ahora sí tenemos una base de datos, a la cual conectar nuestro REST API, tenemos que hacer unos cambios en nuestro código para poder conectarnos e interactuar con ésta.


Antes de comenzar, debemos instalar en nuestro proyecto de VScode la dependencia de MySQL, lo cual vamos a hacer poniendo el siguiente comando en la terminal dentro de nuestro proyecto:

  
```sql
npm i mysql -s
```

Instalamos **doteev** que es una dependencia de node  que carga las variables de entorno desde un archivo .env en process.env

```sql
npm i dotenv -s
```

### Código

Vamos a partir de nuestro proyecto creado anteriormente, y simplemente haremos algunas modificaciones. Si no tiene el proyecto, aquí te dejo el repositorio para que vayas a descargarlo [LINK](https://github.com/RobertoPeredo/PersonasAPILocal)

Abrimos nuestro proyecto en VSCode

En nuestro proyecto, en el mismo nivel que la carpeta *app*, vamos a crear un archivo nuevo y lo vamos a nombrar ".env" . También, nuevamente en el mismo nivel que la carpeta *app* vamos a crear una nueva carpeta, la cual nombraremos "config" y dentro de esta carpeta vamos a crear un archivo llamado  "mysql.js" esto haciendo referencia a que nos servirá para la conexión con la base de datos de MySQL. Quedando al final de la siguiente forma, los archivos remarcados en color verde son los que acabamos de agregar:
![image](https://user-images.githubusercontent.com/99369122/171771817-b4133af5-7325-4be3-9585-e697935cf65c.png)

Abrimos ahora el archivo .env, en este archivo van a ir todos los datos necesario para conectarnos a nuestra base de datos
El archivo .env  permite personalizar las variables de entorno de trabajo individuales. Puesto que el archivo .env está oculto
El uso de variables de entorno, o environment, en las aplicaciones web es importante para la separación del código por responsabilidades, no debemos mezclar el código de la aplicación con los valores de configuración.

Las variables de configuración cambiarán generalmente según el entorno de ejecución, es decir, cuando una aplicación está siendo ejecutada en distintos servidores.

Lo que es importante es que estos archivos no se encuentren al alcance de los usuarios, por lo que nunca deberían estar dentro de la carpeta de publicación, sino en algún directorio por encima en el servidor. Es decir, se colocará en la raíz del proyecto, pero nunca dentro de la carpeta raíz de publicación, pues si estuvieran allí los usuarios podrían acceder a esos valores componiendo la ruta como "example.com/.env". Obviamente, los valores de configuración deseamos que estén seguros, por lo que no deben ser accesibles por el público en general.

En este archivo ".env" vamos a agregar las siguientes líneas 
```
DB_CONN=rest-api-server.mysql.database.azure.com
DB_USER=root1
DB_PASSWORD=rest-api246
DB_DATABASE=basededatosdemoweb
DB_PORT=3306
```
Se estarán preguntando de donde obtuve esos datos, para obtener los datos de la conexión a nuestra base de datos. Tenemos que ir al servidor que creamos anteriormente dentro Azure. Par eso tenemos que visitar [portal.azure.com](htpps://portal.azure.com),  ahí vamos a buscar nuestro servidor creado y daremos clic en éste
![image](https://user-images.githubusercontent.com/99369122/171772782-1849bf16-94f3-425b-b8ef-01e9d206931d.png)

Nos desplegará una ventana y buscaremos en la barra lateral derecha el apartado de "Cadenas de conexión"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171772873-4648c996-6f05-4f24-89a4-4edd56b36715.png)

Aquí nosotros copiaremos por ejemplo la de Node.js
![image](https://user-images.githubusercontent.com/99369122/171773021-d24f116c-ecac-4c9d-af80-25b84903f261.png)
 La cual nos dará algo como esto:

```js
var conn=mysql.createConnection({
 host:"rest-api-server.mysql.database.azure.com",
 user:"root1",
 password:"{your_password}",
 database:"{your_database}",
 port:3306, 
 ssl:{ca:fs.readFileSync("{ca-cert filename}")}}); 
 

```
 
 Como nosotros no vamos a hacer la conexión directa, sino que vamos a hacer por medio de variables de entorno, entonces de aquí vamos a ir copiando los valores uno a uno e írselos asignado a las constantes que pusimos en el archivo ".env". Ahora recordemos que nosotros eliminamos la autenticación por SSL por lo que no es necesario agregar esa variable. Los campos *password*  lo obtuvimos al momento de crear nuestro servidor, y *database*  es el nombre de la base de datos que nosotros creamos.
 
 Posterior a esto, en el archivo  "mysql.js" que creamos  vamos a pegar el siguiente código, este nos servirá para realizar la conexión con la BD

```js
 const mysql = require('mysql');//Utilizo el módulo de mysql p


//Creo una función para realizar la conexión de la base de datos
const dbConnect = () =>{

    /*creo un objeto con los parámetros necesarios para realizar la conexión a la db, noten
    que lo realizo con los valores que añadimos en el archivo .env*/
    conn= mysql.createConnection({
        host:process.env.DB_CONN,
        user:process.env.DB_USER,
        password:process.env.DB_PASSWORD, 
        database:process.env.DB_DATABASE,
        port:process.env.DB_PORT      
  })

  //con los datos del objeto, intentamos hacer la conexión a la base de datos
    conn.connect(error=>{
        // si hay error en la conexión
    if(error) throw {error: "**** ERROR DE CONEXION ****"}
       //si la conexión fue correcta    
    console.log("**** CONEXION CORRECTA ****");
})
}

//exportamos nuestra función para llamarla en el index
module.exports={dbConnect}
 
```
Y finalmente en el archivo index.js vamos a agregar en las cabeceras las siguientes líneas

```js
 
  require('dotenv').config()
 const {dbConnect}=require('./config/mysql')// importamos la función dbConnect del archivo mysql.js
```

Y en la parte de hasta abajo, antes de realizar el app.listen al puerto vamos a agregar
```js
 //llamamos a la función que realiza la conexión con la DB
dbConnect()
 
```
Y así es, solo con tres líneas en nuestro índex, creamos la conexión a nuestra base de datos. De todas formas, el código completo en el archivo de index.js es el siguiente: 
```js
 const express = require('express'); // Utilizo el módulo de express de Node
const path = require('path'); // Utilizo el módulo path de Node
const bodyParser = require('body-parser') // Utilizo el modulo de body parser
const app = express(); // Genero mi aplicación de express simplemente llamando al constructor express()
const endPoints = require('./app/routers/personas')/*Importo  el modulo(en este caso endPoint) que exporte
 desde la ruta ./app/routers/personas */
 const cors = require('cors')//Utilizo el módulo de cors
 require('dotenv').config()
 const {dbConnect}=require('./config/mysql')// importamos la funcion dbConnect del archivo mysql.js

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

//llamamos a la función que realiza la conexión con la DB
dbConnect()


/* constante para nuestro puerto, es un una condición OR para el caso de  desarrollo en algún servicio
 o desarrollo local (nuestro caso) */
const port = process.env.port || 8080; 
app.listen(port, () =>console.log(`Escuchando en el puerto ${port}`))
 
```
  
  Guardamos los cambios y corremos nuestra aplicación, ya saben para esto en la terminal escribimos el comando  
```
  npm run serve
```
  
  Y si todo sale bien, nos aparecerá en consola un mensaje como este, lo cual indica que **hicimos una conexión correcta a nuestra base de datos**
  ![image](https://user-images.githubusercontent.com/99369122/171775505-2910c415-d00c-4191-9d45-5e7320285b15.png)
  
  Ahora simplemente en nuestro archivo **personas.j** dentro de la carpeta de *controllers*, vamos a realizar algunas modificaciones, porque, recordemos que ya no vamos a  hacer las solicitudes simplemente con un array interno, sino que las haremos directamente en la base de datos. En este archivo, cambiaremos el contenido de cada función, porque antes insertábamos datos en un array, ahora tenemos que cambiar esto por comandos y validaciones de SQL. El código que vamos a insertar es el siguiente. El código viene con sus respectivos comentarios para mayor entendimiento del mismo

```js
  const { response } = require('express');
const { request } = require('express');


//Obtener todas las personas de la lista

const obtenerPersonas = [(request, response)=>{

    //creo el comando para seleccionar todas los elementos mi tabla personas y lo guardo en sql
    const sql = 'SELECT * FROM personas';
     //Hago la conexión con mi base de datos
    conn.query(sql, (error, results) => {
      //Si se genera un error con la bd lo lanzamos
        if (error) throw error;
         // Sino se genera error, verificamos que venga algo en la respuesta, es decir que el haya al menos una persona registrada
        if (results.length > 0) {
          /*Si existen personas,Mandamos todas las persona registradas en la respuesta, 
          aquí ya se realizó la sentencia de sql*/
          response.json(results);
        } else {
          //Sino existe ninguna persona registrada imprimimos el mensaje:
            response.status(415).json({error: "No existe  ninguna persona registrada"});
        }
      }); 
}]


//Obtener una  personas de la lista de acuerdo a su ID
const obtenerPersona =[(request,response)=>{
    /*recupero el id de la persona haciendo un de-structur. La idea es crear una variable llamada id, 
    que está contenida con el mismo nombre id dentro de parms*/
    const {id} = request.params 
    //creo el comando para seleccionar la persona con el id de mi tabla personas y lo guardo en sql 
    const sql = `SELECT * FROM personas WHERE id = ${id}`;
     //Hago la conexión con mi base de datos
    conn.query(sql, (error, results) => {
      //Si se genera un error con la bd lo lanzamos
        if (error) throw error;
         // Sino se genera error, verificamos que venga algo en la respuesta, es decir que el id exista
        if (results.length > 0) {
      // Si el id existe, mandamos en la respuesta los datos de la persona, aquí ya se realizó la sentencia de sql
          response.json(results);
        } else {
          //Sino existe el id imprimimos el mensaje:
        response.status(410).json({error: "Este id no existe"});
        }
      }); 
    
    
}]



//Añadir una nueva persona a la lista
const añadirPersona = [(request,response)=>{ 
/*Todo esto se ejecuta solo si los datos fueron validados. Es decir, validarDatos dentro de
/validator/personas.js continuó con  next()*/

//creo el comando para seleccionar para añadir una persona en  mi tabla personas y lo guardo en sql 
const sql = `INSERT INTO personas SET ?`
 //Crea una variable de tipo objeto, llamada nuevaPersona, con los datos mandados en el body dentro de request
    const nuevaPersona = {        
        Nombre: request.body.Nombre,
        Apellido: request.body.Apellido,
        Edad: request.body.Edad,
        Mail: request.body.Mail,
        Celular: request.body.Celular
    }
  //Hago la conexión con mi base de datos
    conn.query(sql,nuevaPersona, (error) => {
      //Si se genera un error con la bd lo lanzamos
        if (error) throw error;
        /* Sino se genera error, mando en mi respuesta los de la persona creada, aquí ya se realizó la 
        sentencia de sql,pero para mandar los datos de la persona creada primero solicito el id que le asignó
        con el siguiente comando*/                         
        sqlId ='SELECT @@identity AS id'
        //Hago la conexión con mi base de datos
        conn.query(sqlId,(error,results)=>{
        //Si se genera un error con la bd lo lanzamos
          if (error) throw error;
          // Sino se genera error accedo al id que viene que viene en la posición cero de resultados
        neWId=results[0].id
        //a mi objeto nuevo persona le agrego el id
        nuevaPersona.id=neWId
        // Ahora sí mando como respuesta los datos de la persona que se agregó
        response.json(nuevaPersona) 
          
        })        
        
      }); 
}]

  
//Actualizar una nueva persona de la lista
const actualizarPersona = [ (request,response)=>{  
    /*Todo esto se ejecuta solo si los datos fueron validados. Es decir, validarDatos dentro de
/validator/personas.js continuó con  next() */
   

 /*recupero el id de la persona haciendo un de-structur. La idea es crear una variable llamada id, 
    que está contenida con el mismo nombre id dentro de parms*/    
    const {id} = request.params
    
   //creo el comando para seleccionar la persona con el id de mi tabla personas y lo guardo en sql 
    const sql = `SELECT * FROM personas WHERE id = ${id}`;
    //Hago la conexión con mi base de datos
    conn.query(sql, (error, results) => {
      //Si se genera un error con la bd lo lanzamos
        if (error) throw error;
        // Sino se genera error, verificamos que venga algo en la respuesta, es decir que el id exista
        if (results.length > 0) {
           /*Si el id existe, almaceno en variables  todos los valores que provienen del body (desestructuro)  */
           const {Nombre,Apellido,Edad,Mail,Celular} = request.body;
          /* Si el id existe, podemos modificar los datos de la persona, entonces guardamos el comando
           para modificar en sqlUpdate*/
          const sqlUpdate = `UPDATE personas SET  Nombre = '${Nombre}', Apellido = '${Apellido}',
          Edad = '${Edad}', Mail = '${Mail}', Celular = '${Celular}' WHERE id = ${id}; `          
          //Hago la conexión con mi base de datos       
          conn.query(sqlUpdate,error => {
            //Si se genera un error con la bd lo lanzamos
            if (error) throw error;
            /* Sino se genera error, mando en mi respuesta los de la persona modificados, 
              aquí ya se realizó la sentencia de sql */
            response.json({id,Nombre,Apellido,Edad,Mail,Celular});
      }); 
    }  
        else {
          //Sino existe el id imprimimos el mensaje:
        response.status(410).json({error: "Este id no existe"});
        }
      });
  
}]

const eliminarPersona = [(request,response)=>{
   /*recupero el id de la persona haciendo un de-structur. La idea es crear una variable llamada id, 
    que está contenida con el mismo nombre id dentro de parms*/
    const {id} = request.params 

    //creo el comando para seleccionar la persona con el id de mi tabla personas y lo guardo en sql 
    const sql = `SELECT * FROM personas WHERE id = ${id}`;
          //Hago la conexión con mi base de datos
        conn.query(sql, (error, results) => {
           //Si se genera un error con la bd lo lanzamos
        if (error) throw error;
        // Sino se genera error, verificamos que venga algo en la respuesta, es decir que el id exista
        if (results.length > 0) {
          // Si el id existe, lo podemos eliminar., entonces guardamos el comando para eliminar en: sqlDelete
            const sqlDelete = `DELETE FROM personas WHERE  id = ${id};`
            //Hago la conexión con mi base de datos
            conn.query(sqlDelete,error => {
              //Si se genera un error con la bd lo lanzamos
                if (error) throw error;
                /* Sino se genera error, mando en mi respuesta el id de la persona eliminada, 
                aquí ya se realizó la sentencia de sqlDelete */
              response.json(id);
              }); 
        } else {
          //Sino existe el id imprimimos el mensaje
        response.status(410).json({error: "Este id no existe"});
        }
      }); 

    
}]

//exporto las funciones hacia mi ruta /routers/personas.js
module.exports = {obtenerPersonas, obtenerPersona,añadirPersona, actualizarPersona, eliminarPersona}
```
   
   Y listo!! ¡¡¡Tenemos nuestro REST-API terminado y conectado a una base de datos en la nube de Azure!!! **¡Fenomenal!**.
   
   ¡¡¡¡Aquí te voy a dejar el repositorio con el código completo y listo para ser ejecutado!!!!<br><br>
   ------>>>> LINK DEL REPOSITORIO COMPLETO  [LINK](https://github.com/RobertoPeredo/PersonasAPI-DB)

## Validación de los END-POINTS utilizando POSTMAN
   Lo siguiente es realizar nuestras pruebas, para verificar que todo esté funcionando correctamente.
   Para esto te voy a dejar nuevamente un archivo tipo JSON  para que podamos realizar las validaciones  en POSTMAN
   [VALIDACIONES](https://github.com/RobertoPeredo/REST_API/tree/main/POSTMAN/localhost-DB)
   


   Ingresaremos a POSTMAN, pero antes, verifiquemos el estado actual de la Tabla personas dentro de nuestra base de datos que creamos con anterioridad. Para esto vamos a ir al portal de Azure, abriremos la terminal y nos conectaremos a nuestro servidor. Una vez dentro de nuestro servidor, utilizaremos el comando
   
```sql
 USE basededatosdemoweb
```
  Posteriormente utilizaremos
```sql
  SELECT * FROM personas
```
  

      
 Y obtendremos esta respuesta, este es el estado actual de nuestra tabla personas, que sería más o menos así.
 ![image](https://user-images.githubusercontent.com/99369122/171963961-3faf74fe-f2ba-4733-ab37-905d023fe9ef.png)

Ahora sí, iremos a postman y con el método GET tendría que devolvernos los mismos datos que nuestra base de datos


1.- Prueba del método GET que nos devuelve todas las personas
![image](https://user-images.githubusercontent.com/99369122/171964425-ccdd972a-28f9-43ef-8478-45a0f7cc2005.png)
¡¡Como pueden observar, efectivamente nos devuelve los mismos datos que nuestro base de datos!! Estamos haciéndolo de forma correcta<br><br>
2.- Prueba del método GET que nos devuelve una persona por su ID, si ponemos, por ejemplo, el id No 2. Según nuestra base de datos, tendría que devolvernos el API todos los datos de Carlos Guzmán. Hacemos la petición en POSTMAN
![image](https://user-images.githubusercontent.com/99369122/171964549-577e079c-ad64-4a31-afab-1edd34166a6e.png)
Efectivamente, nos devolvió los resultados esperados.<br><br>
3.- Probemos ahora con el método POST. Agregamos los datos en el body según nuestra [definicón](https://app.swaggerhub.com/apis-docs/RobertoPeredo/personas-api/1.0.0)
y en postman obtenemos la siguiente respuesta
![image](https://user-images.githubusercontent.com/99369122/171964681-7c1ce28d-a199-44a1-8f03-03c0408b896a.png)
Ahora verificamos en nuestra base de datos, que se haya añadido correctamente la persona, para esto nuevamente en la terminal de Azure escribiremos

```sql
  SELECT * FROM personas
```
  ![image](https://user-images.githubusercontent.com/99369122/171964779-e46bfbfd-3111-416e-8a31-75cbc81e2b0b.png)

  ¡¡¡¡Y podemos observar como en el registro con id=5 añadió los datos que le mandamos desde el API!!!!
  Hasta ahora todo funciona muy bien. 
  Intentemos añadir una persona, con un dato faltante en el body
  ![image](https://user-images.githubusercontent.com/99369122/171964987-5ea85926-5f4b-4545-95e8-1a4e3ed8a760.png)
Como lo esperábamos nos arroja un error, por lo tanto, nuestras validaciones están funcionando correctamente<br><br>
4.- Probemos ahora con el método PUT para cambiar los datos de una persona, intentaremos cambiar los datos del registro 5, que intencionalmente los puse repetidos para que podamos probar nuestro método PUT. Ponemos los datos en el body de acuerdo con nuestra [definicón](https://app.swaggerhub.com/apis-docs/RobertoPeredo/personas-api/1.0.0) y obtenemos la siguiente respuesta
![image](https://user-images.githubusercontent.com/99369122/171965166-0845e950-1acf-4ecf-9f62-8be9683720ff.png)
Verificamos nuevamente en nuestra base de datos, con el comando
 ```sql
  SELECT * FROM personas
  ```
  Y en efecto, nos modificó correctamente los datos<br><br>
  ![image](https://user-images.githubusercontent.com/99369122/171965254-e951cb9d-29c9-4840-b952-3cae29a826f2.png)<br><br>
5.- Finalmente probaremos el eliminar una persona, para esto, eliminaremos a la persona con el id=5. Esta es la respuesta obtenida de postman
 ![image](https://user-images.githubusercontent.com/99369122/171965350-e067c32a-40c2-4445-b2ae-730225e284b9.png)
 Por último, verificamos nuevamente en nuestra base de datos<br><br>
![image](https://user-images.githubusercontent.com/99369122/171965395-be620027-1ff3-4089-a785-3ebf90b687e7.png)<br><br>
Y efectivamente borró los datos de esta persona<br><br>


## Siguientes pasos

¿Qué sigue ahora?<br><br>
Vamos a subir nuestro nuevo REST-API en un App Service de Azure, para que podamos acceder a nuestro API desde cualquier lado, pero ya no lo haremos paso a paso, puesto que esto ya lo hicimos anteriormente, sino viste esa parte del tutorial o ya olvidaste los pasos, aquí te dejo el [ENLACE](./implementacion.md) para que puedas implementar este REST-API en la nube de Azure.


Yo ya implementé esto en la nube de AZURE, este es el enlace obtenido.

¡Te dejo por aquí el link para que puedas probarlo tu mismo!<br><br>
 LINK ----------------------->>>>>>>>>>>>>> [https://personasapi-db.azurewebsites.net](https://personasapi-db.azurewebsites.net)



Ahora, te invito a seguir con la siguiente parte del tutorial, en donde añadiremos un API-KEY a nuestro REST-API para que podamos tener un mejor control de ésta








