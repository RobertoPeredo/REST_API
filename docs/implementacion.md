# Implementación de un API en un App Services de Azure

## Subir nuestro proyecto a un repositorio de GitHub

### Creando un nuevo repositorio

1. Lo primero que tenemos que hacer es crear un repositorio nuevo en GitHub. Para esto vamos a ir a la página de GitHub y damos clic en el botón "+" que aparece en la parte superior derecha, y vamos a seleccionar " New repository".<br><br>
![image](https://user-images.githubusercontent.com/99369122/171529266-132065c6-154f-483c-b1ab-564e4e91d844.png)<br><br>
2. Vamos a colocar un nombre y una descripción a nuestro repositorio, en esta ocasión, yo nombré mi repositorio como "PersonasAPILocal, posteriormente vamos llenar los demás datos y haremos clic en "Create repository"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171529489-ee081386-0961-40b3-b088-43298a4a4393.png)<br><br>
### Subiendo nuestro repositorio a GitHub
1. Nos aparecerá un código como el siguiente, el cual vamos a copiar.

![image](https://user-images.githubusercontent.com/99369122/171529813-ac620540-c518-4bd8-a189-d7641f1e0448.png)
2. Vamos a abrir en Visual Studio la carpeta de nuestro proyecto, y vamos a pegar en la terminal el código que copiamos. Para esto, ya debes tener vinculado tu VScode con tu cuenta de GitHub

![image](https://user-images.githubusercontent.com/99369122/171530206-53264d2f-6852-4ac2-a69a-2b9fbcf91043.png)
3. Vamos a presionar "enter", vamos a agregar un comentario para el commit y automáticamente se comenzarán a subir todos los archivos de nuestro proyecto a nuestro repositorio de GitHub. Presionamos en Sync Changes, y listo. Ahora sí, tenemos nuestro Repositorio listo con todos los archivos.
![image](https://user-images.githubusercontent.com/99369122/171530585-217b6f64-52c4-4315-a285-f18cc0388a7e.png)

### Link del repositorio

Aquí te dejo el link del repositorio, para que simplemente lo descargues y hagas uso de el 
[PersonasAPILocal](https://github.com/RobertoPeredo/PersonasAPILocal)

## Subiendo nuestra API en Azure
Lo primero que tenemos que hacer es tener una cuenta en [portal.azure.com](https://portal.azure.com). Yo, por ejemplo, creé mi cuenta con mi correo estudiantil, el cual me otorga $100 dólares para poder ocupar en los servicios de Azure.

Una vez con nuestra cuenta logueada, procedemos a dar clic en "crear un recurso"
![image](https://user-images.githubusercontent.com/99369122/171550598-dea30113-ce68-4bcb-84a3-05643b1710b5.png)
Posteriormente elegimos la opción “crear" en Aplicación Web
![image](https://user-images.githubusercontent.com/99369122/171550721-ecbc8696-6d09-420b-9543-e4423ca80a83.png)
Ahora vamos a ir llenando poco a poco los datos que se nos solicita.

#### Detalles del proyecto
En *Suscripción*, dejaré la que viene de forma predeterminada qué es "Azure for Students", como les comenté esta suscripción viene con mi cuenta creada a partir del correo de estudiante. En el apartado de *Grupo de recursos* voy a hacer clic en donde dice "Crear nuevo"
![image](https://user-images.githubusercontent.com/99369122/171552423-4347422d-31c1-449e-82af-5c643f2896f3.png)
<br><br>Le pondré por nombre **"DemoWeb"* y haré clic en aceptar.<br><br>
![image](https://user-images.githubusercontent.com/99369122/171552544-0d76bfe9-414b-42c3-82e1-8e402ecf2ebf.png)
#### Detalles de instancia
En el apartado de *Nombre*, colocaré el nombre de nuestro proyecto hasta ahora, el cual es "PersonasAPILocal". Los demás datos deben ser preferentemente llenados como se muestran en la imagen. Es importante que en el aparto *Publicar* seleccionemos la opción **"Código"**
![image](https://user-images.githubusercontent.com/99369122/171552878-b58f46b5-dfdc-4e29-bbbc-0d80c7056624.png)

#### Plan de App Service
En el apartado de *Plan de Linux* lo voy a dejar por defecto, pero en *SKU y tamaño* voy a hacer clic en "Cambiar tamaño"
![image](https://user-images.githubusercontent.com/99369122/171553310-3cde044d-42fc-461a-8839-44e38158ebf9.png)<br><br>
Y en el menú del lado derecho, voy a seleccionar el "plan de tarifa gratuito" y a dar clic en "Aceptar"<br><br>
![image](https://user-images.githubusercontent.com/99369122/171553441-ecc600f3-996c-428a-94c7-dc3109038e5a.png)
Por último, simplemente voy a dar clic en "Revisar y crear"
![image](https://user-images.githubusercontent.com/99369122/171553598-2634838a-f26e-49d0-b437-f2f788313747.png)
Nos aparecerá esta pantalla y haremos clic en "Crear
![image](https://user-images.githubusercontent.com/99369122/171553780-1f50398f-c0ef-4557-8eeb-0493efa02908.png)
#### Implementación
Nos aparecerá una pantalla como esta, y debemos dejar que se termine de realizar la implementación
![image](https://user-images.githubusercontent.com/99369122/171553938-3e8a1097-192e-4c51-99e2-824fdd4a55ff.png)
Una vez terminada la implementación, nos aparecerá la siguiente pantalla y a continuación daremos clic en "Ir al recurso"
![image](https://user-images.githubusercontent.com/99369122/171554124-15bcf015-abf0-4891-bee9-96bc70a62e1e.png)
<br><br>Iremos a la barra lateral izquierda y buscaremos la opción de **" Centro de implementación"** y haremos clic sobre ésta.<br><br>
![image](https://user-images.githubusercontent.com/99369122/171554956-0d1e4687-d7c9-45e4-9ba2-097c7e987e01.png)

### Centro de implementación

#### Origen

Nos aparecerá la siguiente ventana, y seleccionaremos GitHub como Origen de nuestro proyecto
![image](https://user-images.githubusercontent.com/99369122/171555151-0c42968b-4bd2-4654-b3bd-d74d44061d55.png)

#### Github
Debemos loguearnos con nuestro perfil de GitHub y seleccionar la organización, repositorio y rama de nuestro proyecto. 
![image](https://user-images.githubusercontent.com/99369122/171555406-ebcde95b-2689-4543-9255-06981b3edc87.png)

Y finalmente, en la parte superior, debemos hacer clic en "Guardar"
![image](https://user-images.githubusercontent.com/99369122/171555483-5f766418-e34b-41f5-8f9e-18e24f6f6e8d.png)

#### Actions en Github.
Una vez hecho clic en "Guardar", automáticamente en nuestro repositorio de GitHub comienza a ejecutarse un Action de parte de Azure, en cuanto termine de construirse y desplegarse, tendremos acceso a nuestra API 
![image](https://user-images.githubusercontent.com/99369122/171555717-f6a6813d-ba09-42d6-9ac9-1f44ab12b753.png)

Una vez terminada el Action por parte de GitHub veremos algo así<br><br>
![image](https://user-images.githubusercontent.com/99369122/171981482-260a1969-c90c-475b-adbf-5664b1ebc26e.png)

#### URL de nuestro REST-API
Regresamos a Azure y hacemos clic en "Introducción"<br>
![image](https://user-images.githubusercontent.com/99369122/171555933-447979ef-f361-443a-b1df-02b697d81f77.png)

¡¡¡¡¡¡Y con este link, tendremos acceso a nuestra API corriendo en AZURE!!!!!!
![image](https://user-images.githubusercontent.com/99369122/171556249-3820655c-b333-4113-bb76-eb29e9ce05c3.png)

¡¡¡Este es el LINK!!! --->>>> [https://personasapilocal1.azurewebsites.net](https://personasapilocal1.azurewebsites.net)

Se los comparto, para que ustedes mismos realicen pruebas del RESTA API funcionando.

Probaremos nuestra API nuevamente con la plataforma de POSTMAN. Les dejó aquí el archivo para que tú mismo puedas realizar las pruebas. Basta con descargar el archivo e importarlo en POSTMAN. ¡No olvides hacer las solicitudes con base a la definición de nuestra API! Te dejo [AQUI](https://app.swaggerhub.com/apis-docs/RobertoPeredo/personas-api/1.0.0) la definición de nuestro REST API para que tú mismo o puedas realizar las pruebas.

[ARCHIVO PARA PRUEBAS EN POSTMAN](https://github.com/RobertoPeredo/REST-API/tree/main/3.%20Implemetaci%C3%B3n%20del%20API%20en%20un%20App%20Service%20de%20Azure/POSTMAN)
<br><br>En esta ocasión solo realizaremos la prueba de un END-POINT para que observen que todo trabaja a la perfección


El resto de las pruebas las omito, porque es las mismas que ya realizamos en la parte anterior del tutorial, te dejo [AQUÍ](https://robertoperedo.github.io/REST_API/desarrollo/#pruebas-de-funcionamiento-de-los-endpoint-utilizando-postman) la liga de las pruebas por si quieres revisar cómo se hacen.















