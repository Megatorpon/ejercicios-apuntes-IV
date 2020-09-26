## Tema 1: Introducción a la infraestructura virtual: concepto y soporte físico
###### Antonio Cuadros Lapresta
##### Ejercicio 1: Consultar en el catálogo de alguna tienda de informática el precio de un ordenador tipo servidor y calcular su coste de amortización a cuatro y siete años. Consultar [este artículo en Infoautónomos sobre el tema](https://www.infoautonomos.com/consultas-a-la-comunidad/988/)
Para la realización de este ejercicio en primer lugar he tenido que buscar información acerca de la amortización, más concretamente aquella relacionada con productos informáticos, para ello en consultado [la siguiente página](https://www.infoautonomos.com/contabilidad/tablas-de-amortizacion-para-los-bienes-de-una-empresa/)
Según la información de la misma los productos que se enmarcan como "Equipos para tratamiendo de la información y sistemas y programas informáticos" tienen un coeficiente lineal máximo del 26% y un periodo máximo de 10 años.
Si nosotros por ejemplo queremos amortizar [el siguiente producto](https://www.pccomponentes.com/asustor-lockerstor-8-as6508t-servidor-nas), un servidor Asustor LOCKERSTOR 8 AS6508T Servidor NAS con un precio de 1092,42€.
De esta forma atendiendo a los ejemplos que se presentan en la página citada en el ejercicio, si este servidor tiene un coste de 1092,42€, si le quitamos el IVA, para calcular la amortización, en este caso un 21%, el precio del producto es de 863,0118€ y el 26% de este precio es 224,383068€ de esta forma la amortización de este producto comprado mediados del año 2020  será a lo largo de 4 años (Último y primer año deben ser proporcionales al mes de compra, mediados de año, mitad de la amortización basada en el 26%):
2020: 112,191534€
2021:224,383068€
2022:224,383068€
2023:112,191534€

##### Ejercicio 2: Usando las tablas de precios de servicios de alojamiento en Internet “clásicos”, es decir, que ofrezcan Virtual Private Servers o servidores físicos, y de proveedores de servicios en la nube, comparar el coste durante un año de un ordenador con un procesador estándar (escogerlo de forma que sea el mismo tipo de procesador en los dos vendedores) y con el resto de las características similares (tamaño de disco duro equivalente a transferencia de disco duro) en el caso de que la infraestructura comprada se usa solo el 1% o el 10% del tiempo.
Como Virtual Private Server he elegido el [siguiente](https://www.arsys.es/servidores/vps). Como configuración del mismo he decidido elegir una opción intermedia entre la más cara y la más barata y nos presenta las siguientes características:
- Procesador 2 vCPUs Intel Xeon.
- Memoria RAM 4 GB.
- 60 GB SSD.
- Transferencia ilimitada.
- 1 IP y firewall.
- Sistema operativo Linux
Todo esto tiene un coste de 7,50€ al mes.


Por otra parte tenemos la opción de contratar un proveedor de servicio en la nube, en este caso he elegido el [siguiente](https://www.digitalocean.com/pricing/#general-purpose-droplets) que presenta las siguientes características:
- Procesador 2vCPUs.
- 4 GB RAM.
- 80 GB SSD.
Todo esto tiene un coste de 0.030$ y al mes de 20$.

Teniendo todo esto en cuenta y si suponemos que se va a utilizar unicamente el 10% del tiempo y pagamos por horas, el 10% de un día (24 horas) son 2,4 horas que ajustamos a 3 horas. Cómo unicamente vamos a utilizar el servicio 3 horas al día pagaríamos 0.09$ al día que sería un total de 2,7$ (2,32€) al mes para poder comparar con el VPS que costaba 7,50€ al mes.


Como conclusion podemos ver que nos viene mucho mejor el segundo caso ya que se ajusta mejor a nuestro uso y en consecuencia conseguimos ahorrar más dinero e incluso tenemos mejores características como el tamaño del disco duro.

##### Ejercicio 3: En general, cualquier ordenador con menos de 5 o 6 años tendrá estos flags. ¿Qué modelo de procesador es? ¿Qué aparece como salida de esa orden? Si usas una máquina virtual, ¿qué resultado da? ¿Y en una Raspberry Pi o, si tienes acceso, el procesador del móvil?

El procesador que posee mi ordenador es un intel core i7 8700k, todos los detalles se pueden consultar [aquí](https://www.intel.es/content/www/es/es/products/processors/core/core-vpro/i7-8700k.html).
Si leemos el archivo /proc/cpuinfo obtenemos la siguiente información:
![Imagen](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema%201%20Introduccion/Im%C3%A1genes/Ejercicio_3_1.PNG)

Si además ejecutamos el comando egrep '^flags.*(vmx|svm)' /proc/cpuinfo citado en la parte de teoría obtenemos lo siguiente:
![Imagen2](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema%201%20Introduccion/Im%C3%A1genes/Ejercicio_3_2.PNG)

Además podemos probarlo con lscpu y obtenemos lo siguiente:
![Imagen3](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema%201%20Introduccion/Im%C3%A1genes/Ejercicio_3_4.PNG)

Si además probamos esto en una máquina virtual, obtenemos lo siguiente:
![Imagen4](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema%201%20Introduccion/Im%C3%A1genes/Ejercicio_3_3.PNG)

En cuanto al último aspecto comentado a probar, no dispongo de una Raspberry Pi ni de un móvil con Android.

##### Ejercicio 4: Instalar un hipervisor para gestionar máquinas virtuales, que más adelante se podrá usar en pruebas y ejercicios. Usar siempre que sea posible un hipervisor que sea software libre.
Como hipervisor para gestionar máquinas virtuales y que además sea software libre he elegido [Virtual Box](https://www.virtualbox.org/)
Se muestra una captura de Virtual Box ejecutándose tras su instalación:
![Imagen5](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema%201%20Introduccion/Im%C3%A1genes/Ejercicio_3_5.PNG)

##### Ejercicio 5: Darse de alta en una web que permita hacer pruebas con alguno de los sistemas de gestión de nube libres como los mencionados en los párrafos anteriores, aunque sea temporalmente. Si la prueba es menos de un mes, simplemente anotarlo y dejarlo para el mes de diciembre, más o menos.

Para este ejercicio me he dado de alta en Microsoft Azure que posee una prueba gratuita de 12 meses, aún así no he adquirido aún la prueba hasta que la necesite. Se adjunta captura de pantalla una vez dado de alta:
![Imagen6](https://github.com/antoniocuadros/ejercicios-apuntes-IV/blob/master/Ejercicios/Tema%201%20Introduccion/Im%C3%A1genes/Ejercicio_5_1.PNG)