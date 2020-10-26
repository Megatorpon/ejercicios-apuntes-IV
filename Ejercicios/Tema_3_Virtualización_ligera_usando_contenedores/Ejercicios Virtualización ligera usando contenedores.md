# Ejercicios: Virtualización ligera usando contenedores
## Ejercicio 1
### Instalar docker y/o otro gestor de contenedores como Podman/Buildah.
#### Instalar Docker
En primer lugar eliminamos en caso de que existan, versiones antiguas de Docker:

![img1](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/1.1.PNG)

Actualizamos el índice de paquetes con:
`sudo apt-get update`
Instalamos los paquetes necesarios para permitir a apt usar un repositorio sobre HTTPS:

![img2](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/1.2.PNG)

Añadimos la clave GPG de Docker:

![img3](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/1.3.PNG)

Verificamos que tenemos la clave con la figerprint 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88:

![img4](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/1.4.PNG)

Establecemos el repositorio estable:

![img5](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/1.5.PNG)

Instalamos la última versión de Docker:

![img6](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/1.6.PNG)

Probamos si está instalado y funciona correctamente:

![img7](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/1.7.PNG)



## Ejercicio 2
### Instalar a partir de docker una imagen alternativa de Ubuntu y alguna adicional, por ejemplo de CentOS.

Todas las imágenes mostradas se han encontrado en [Docker Hub](https://hub.docker.com/):

Nos bajamos Alpine por ejemplo:

![img1](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/2.1.png)

Nos bajamos CentOS:

![img2](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/2.2.png)

### Buscar e instalar una imagen que incluya MongoDB.

![img3](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/2.3.png)

## Ejercicio 3
### Crear un usuario propio e instalar alguna aplicación tal como nginx en el contenedor creado de esta forma, usando las órdenes propias del sistema operativo con el que se haya inicializado el contenedor.

Ejecutamos la imagen de CentOS en modo interactivo:

![img1](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/3.1.png)

Creamos un nuevo usuario:

![img2](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/3.2.png)


Ahora instalamos Nginx y comprobamos que funciona:


![img2](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/3.3.png)

## Ejercicio 4
### Crear a partir del contenedor anterior una imagen persistente con commit.

![img1](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_3_Virtualizaci%C3%B3n_ligera_usando_contenedores/images/4.1.png)

## Ejercicio 5
### Crear un Dockerfile para el servicio web que testee la clase que se ha venido desarrollando hasta ahora.

Este ejercicio lo hemos realizado ya en el hito 3. Se puede consultar el Dockerfile en el [siguiente enlace](https://github.com/antoniocuadros/WhenToClass/blob/master/Dockerfile).

## Ejercicio 6
### Desplegar un contenedor en alguno de estos servicios, de prueba gratuita o gratuitos.

Se ha desplegado en [Docker Hub](https://hub.docker.com/r/antoniocuadros/whentoclass) y en [GitHub Container Registry](https://github.com/users/antoniocuadros/packages/container/package/whentoclasstests).