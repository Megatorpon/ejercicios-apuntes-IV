# Ejercicios: Virtualización ligera usando contenedores
## Ejercicio 1
### Instalar docker y/o otro gestor de contenedores como Podman/Buildah.
#### Instalar Docker
En primer lugar eliminamos en caso de que existan, versiones antiguas de Docker:

![img1]()

Actualizamos el índice de paquetes con:
`sudo apt-get update`
Instalamos los paquetes necesarios para permitir a apt usar un repositorio sobre HTTPS:

![img2]()

Añadimos la clave GPG de Docker:

![img3]()

Verificamos que tenemos la clave con la figerprint 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88:

![img4]()

Establecemos el repositorio estable:

![img5]()

Instalamos la última versión de Docker:

![img6]()

Probamos si está instalado y funciona correctamente:

![img7]()



## Ejercicio 2
### Instalar a partir de docker una imagen alternativa de Ubuntu y alguna adicional, por ejemplo de CentOS.

### Buscar e instalar una imagen que incluya MongoDB.

## Ejercicio 3
### Crear un usuario propio e instalar alguna aplicación tal como nginx en el contenedor creado de esta forma, usando las órdenes propias del sistema operativo con el que se haya inicializado el contenedor.

## Ejercicio 4
### Crear a partir del contenedor anterior una imagen persistente con commit.

## Ejercicio 5
### Crear un Dockerfile para el servicio web que testee la clase que se ha venido desarrollando hasta ahora.

## Ejercicio 6
### Desplegar un contenedor en alguno de estos servicios, de prueba gratuita o gratuitos.
