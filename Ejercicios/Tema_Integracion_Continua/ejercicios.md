# Ejercicios: Integración continua
## Ejercicio 9
### Darse de alta en algún sistema de integración continua y posteriormente activar el repositorio en el que se vaya a aplicar la integración continua.
#### Darnos de alta en Travis CI 
En primer lugar para empezar a trabajar con Travis CI debemos dirigirnos a su página oficial, la cual encontramos en el [siguiente enlace](https://travis-ci.org/).

Una vez dentro de la página web nos registramos haciendo click en "Sign Up": 

![img1](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Integracion_Continua/images/9.1.png)

Una vez habiéndole dado a "Sign Up" se nos redirige a lo siguiente, debemos darle a "autorize travis-ci":

![img2](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Integracion_Continua/images/9.2.png)

Una vez hecho esto se nos pide introducir la contraseña de GitHub, la introducimos y con esto ya estaríamos registrados.

![img3](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Integracion_Continua/images/9.3.png)

#### Activar el repositorio en el que se vaya a aplicar la integración continua

A la izquieda en la misma página de bienvenida podemos encontar un símbolo "+" para añadir travis-ci a nuestro repositorio:

![img4](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Integracion_Continua/images/9.4.png)

Ahora en la nueva página a la que hemos sido redirigidos, añadimos travis-ci a nuestro repositorio de la siguiente forma:

![img5](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Integracion_Continua/images/9.5.png)

Lo que hemos conseguido con esto es añadir un webhook de GitHub en nuestro repositorio de forma automática:

![img6](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Integracion_Continua/images/9.6.png)

## Ejercicio 10
### Configurar integración continua para nuestra aplicación usando Travis o algún otro sitio.
Se ha configurado la integración continua sobre el repositorio [WhenToClass](https://github.com/antoniocuadros/WhenToClass), puede que sea modificado para ejecutar los tests haciendo uso del contenedor creado en el hito 3.

```
language: ruby
cache: bundler
rvm:
  - 2.7.2
before_install:
  - gem install bundler
install: bundle install
script: rake test
```

Podemos observar que funciona correctamente con la siguiente imagen:

![img7](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Integracion_Continua/images/10.1.png)