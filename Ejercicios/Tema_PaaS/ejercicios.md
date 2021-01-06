# Ejercicios: PaaS
## Ejercicio 1
### Darse de alta en algún servicio PaaS tal como Heroku o BlueMix o usar alguno de los PaaS de otros servicios cloud en los que ya se esté dado de alta.

En primer lugar para registrarnos en Heroku que ha sido la plataforma selccionada accedemos a su página oficial que se encuentra en el siguiente enlace: https://www.heroku.com/ más concretamente a https://signup.heroku.com/ donde se nos pedirán ciertos datos como el nombre, apellidos, correo y lenguaje a utilizar entre otros datos.

Una vez nos registremos nos encontraremos con una página como la siguiente:

![img1](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_PaaS/images/2.png)


## Ejercicio 2
### Crear una aplicación en OpenShift o en algún otro PaaS en el que se haya dado uno de alta. Realizar un despliegue de prueba usando alguno de los ejemplos incluidos con el PaaS.

En mi caso estoy trabajando con Heroku, para ello en primer lugar instalamos el CLI de Heroku en Linux mediante la siguiente orden:

`sudo snap install heroku --classic`

Hacemos seguidamente `Heroku login` y tras iniciar sesión nos saldrá si todo ha ido bien:

```
Logging in... done
Logged in as anculap99@gmail.com
```

Desde el cli hacemos `heroku create` en una carpeta donde tengamos la aplicación y obtenemos lo siguiente:

```
Creating app... done, ⬢ calm-spire-62126
https://calm-spire-62126.herokuapp.com/ | https://git.heroku.com/calm-spire-62126.git
```

Para desplegar nuestra aplicación en heroku:

```
git push heroku main
```

Y haremos uso de `heroku open` para abrir el sitio donde se ha desplegado la aplicación. Podemos ver como funciona correctamente:

![img2](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_PaaS/images/3.png)

Adicionalmente se puede configurar para que con cada push en nuestro repositorio de GitHub se despliegue automáticamente, puede observarse esto en la siguiente imagen:

![img3](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_PaaS/images/4.png)


## Ejercicio 3
### Instalar y echar a andar tu primera aplicación en Heroku.

Este ejercicio se ha realizado completamente en el ejercicio anterior donde incluso vemos un ejemplo.


## Ejercicio 4
### Usar como base la aplicación de ejemplo de heroku y combinarla con la aplicación en node que se ha creado anteriormente. Probarla de forma local con foreman. Al final de cada modificación, los tests tendrán que funcionar correctamente; cuando se pasen los tests, se puede volver a desplegar en heroku.

Como se puede leer en la documentación oficial de Heroku en el siguiente enlace https://devcenter.heroku.com/changelog-items/692, el comando `heroku local` ha reemplazado `foreman` haciendo uso de Forego que es según su repositorio oficial 'Foreman in Go'.


No obstante se puede seguir utilizando foreman haciendo `gem install foreman`.

Para ejecutarlo localmente ejecutamos `heroku local` y a continuación obtenemos un mensaje como el siguiente:

```
12:56:29 PM web.1 |  [2021-01-06 12:56:29] INFO  WEBrick 1.6.0
12:56:29 PM web.1 |  [2021-01-06 12:56:29] INFO  ruby 2.7.0 (2019-12-25) [x86_64-linux-gnu]
12:56:29 PM web.1 |  [2021-01-06 12:56:29] INFO  WEBrick::HTTPServer#start: pid=32843 port=9292
```

Viendo así que se ha iniciado correctamente en localhost:9292. 

Para hacer esto ha sido necesario un archivo Procfile que contiene lo siguiente:

```
web: rake start
```

Para hacer que se despliegue cuando se pasen los tests tendremos que habilitar en Heroku la opción `Wait for CI to pass before deploy`.


## Ejercicio 5
### Haz alguna modificación a tu aplicación en node.js para Heroku, sin olvidar añadir los tests para la nueva funcionalidad, y configura el despliegue automático a Heroku.

Antiguamente se podrían usar addons como por ejemplo Codeship.io o Wercker, no obstante Heroku ha añadido una nueva opción de configuración para realizar esto y es la comentada anteriormente `Wait for CI to pass before deploy`.


Todas las pruebas realizadas se encuentran en el siguiente repositorio de github: 