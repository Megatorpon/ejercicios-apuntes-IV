# Ejercicios: Serverless
## Ejercicio 1
### Darse de alta en Vercel y Firebase, y descargarse los SDKs para poder trabajar con ellos localmente.
#### Vercel

En primer lugar nos dirigimos a su página [web](https://vercel.com/) y le damos a registrarnos.

Nos registramos haciendo uso de la cuenta de GitHub, en este caso he usado otra cuenta diferente a mi cuenta principal por si me da problemas los límites de Vercel.

![img1](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Serverless/images/1.png)

En segundo lugar nos pide que vinculemos un repositorio:

![img2](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Serverless/images/2.png)

Vinculamos un repositorio que hemos creado concretamente para esta prueba:

![img3](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Serverless/images/3.png)

Cuando terminemos ya tendremos el deploy hecho:

![img5](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Serverless/images/5.png)

##### Descargar el SDK

Tal y como indica en su página web oficial, nos lo descargamos de la siguiente forma:

![img8](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Serverless/images/8.png)

#### Firebase

Como Firebase es de Google no hace falta crearse una cuenta, simplemente teniendo una cuenta en google ya funciona, de esta manera se ha usado el correo .go.ugr de la facultad:

![img7](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Serverless/images/7.png)

##### Descargar el SDK

Tal y como indica en su página web oficial, nos lo descargamos de la siguiente forma:

![img11](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Serverless/images/11.png)

## Ejercicio 2
### Tomar alguna de las funciones de prueba de Vercel, y hacer despliegues de prueba con el mismo.

Se ha tomado como prueba el ejemplo que viene hecho con ruby debido a que es el lenguaje que estoy utilizando en el proyecto, este ejemplo se puede consultar [aquí](https://vercel.com/docs/serverless-functions/supported-languages#ruby).

Se ha creado la carpeta api y dentro el fichero date.rb que contiene lo siguiente:

```
#Ejemplo obtenido de: https://vercel.com/docs/serverless-functions/supported-languages#ruby
Handler = Proc.new do |req, res|
  res.status = 200
  res['Content-Type'] = 'text/text; charset=utf-8'
  res.body = "Dia y hora actual: #{Time.now}"
end
```

Podemos ver el correcto despliegue en la siguiente foto:

![img9](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema_Serverless/images/9.png)


Y que funciona correctamente [aquí](https://pruebas-vercel.vercel.app/api/date):

