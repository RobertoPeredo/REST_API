# Asignación de API-KEY a nuestro REST-API

Todas las API deben protegerse mediante una autenticación y una supervisión adecuadas. Las dos maneras principales de proteger las API de REST son las siguientes:

1. Tokens de autenticación <br>
Se utilizan para autorizar a los usuarios a hacer la llamada a la API. Los tokens de autenticación comprueban que los usuarios son quienes dicen ser y que tienen los derechos de acceso para esa llamada concreta a la API. Por ejemplo, cuando inicia sesión en el servidor de correo electrónico, el cliente de correo electrónico utiliza tokens de autenticación para un acceso seguro.<br><br>
2. Claves de API <br>
Las claves de API verifican el programa o la aplicación que hace la llamada a la API. Identifican la aplicación y se aseguran de que tiene los derechos de acceso necesarios para hacer la llamada a la API en cuestión. Las claves de API no son tan seguras como los tokens, pero permiten supervisar la API para recopilar datos sobre su uso. Es posible que haya notado una larga cadena de caracteres y números en la URL de su navegador cuando visita diferentes sitios web. Esta cadena es una clave de la API que el sitio web utiliza para hacer llamadas internas a la API.<br><br>


Llegó el momento de darle, un poco más de seguridad a nuestro API, es decir, de darle acceso solo a aquellas clientes que nosotros queramos. Para esto, podríamos configurar los CORS de nuestro REST-API y limitarlo solo al 'origen' que nosotros deseemos. Pero hay casos en el que debemos habilitar los CORS para que cualquier origen pueda acceder. ¿Entonces que podemos hacer?
Una de las soluciones es solicitar un API-KEY que venga en los headers de la solicitud. Validamos que sea correcto, y si es correcto podemos continuar con nuestra petición. ¿Te imaginas cómo?

## Reto
Este es el reto de nuestro proyecto. Ya te di todas las bases acerca de cómo crear el API-REST y de cómo funciona todo nuestro código, es tu turno de poner en práctica lo visto anteriormente para que le asignes la validación por API-KEY a nuestro proyecto

PISTA: ¡¡¡¡USA LOS MIDDLEWARE!!!! 


¡¡Cuando tengas todo listo, utiliza POSTMAN para realizar las pruebas!! ¡No olvides poner en los headers el api-key que configuraste!
¡¡Cualquier problema que se te presente, no dudes en escribirme!!
