# Ejercicios: Microservicios
## Ejercicio 1
### Instalar etcd3, averiguar qué bibliotecas funcionan bien con el lenguaje que estemos escribiendo el proyecto (u otro lenguaje), y hacer un pequeño ejemplo de almacenamiento y recuperación de una clave; hacer el almacenamiento desde la línea de órdenes (con etcdctl) y la recuperación desde el mini-programa que hagáis.
En primer lugar tenemos que instalar localmente etcd, se puede hacer la siguiente forma:

```
apt-get install etcd
```

Para comprobar que lo tenemos instalado hacemos:

```
etcd3 --version
```

Y deberíamos obtener una respuesta similar a:

```
etcd Version: 3.2.26
```

A continuación nos bajamos la gema necesaria para trabajar con etcd en Ruby de la siguiente forma:

```
gem install etcdv3
```

O alternativamente en el Gemfile:

```
gem 'etcdv3'
```

Así nuestro sencillo programa es el siguiente:

```
require 'etcdv3'

conn = Etcdv3.new(endpoints: 'http://127.0.0.1:2379')

 # Get
 value = conn.get('miclave').kvs.first.value
 p value
```

Creamos desde la línea de órdenes una clave y un valor:

```
etcdctl put miclave clavedeprueba 
```

Si ejecutamos el programa obtenemos correctamente los datos:

Obtenemos la siguiente salida:
```
"clavedeprueba"
```



## Ejercicio 2
### Realizar una aplicación básica que use express para devolver alguna estructura de datos del modelo que se viene usando en el curso.

Se ha realizado una aplicación muy sencilla que devuelve un JSON y tiene tres rutas:
- Por defecto devuelve: `{ status: 200 } `
- /status: `{ status: 200 } `
- /date: Devuelve la hora actual.

```
#!/usr/bin/env node

var express=require('express');
var app = express();
var port = process.env.PORT || 8080;


//Petición por defecto
app.get('/', function (req, res) {
    res.send( { status: 200 } );
});

//Petición comprobación del estado
app.get('/status', function (req, res) {
    res.send( { status: 200 } );
});



//getDate
app.get('/date', function (req, res) {
    var d = new Date();
    res.send( { 'Date': d} );
});

//getHoraActual
app.get('/hour', function (req, res) {
    var d = new Date();
    var minutes = d.getMinutes();
    var hour = d.getHours();
    res.send( { 'Hour': hour,
                'Minutes': minutes
    } );
});

app.listen(port);
console.log('Server running at http://127.0.0.1:'+port+'/');
```

## Ejercicio 3
### Programar un microservicio en express (o el lenguaje y marco elegido) que incluya variables como en el caso anterior.

Se puede consultar el ejemplo realizado para la enrega:

```
require "roda"
require "json"
require_relative "../lib/FSDator.rb"
require_relative "../lib/gestorgrados.rb"
require_relative "../lib/parse.rb"
require_relative "middleware"

class App < Roda
    ####################
    #Plugins
    plugin :all_verbs #por defecto solo trae GET y POST, queremos más.
    plugin :response_request #nos permite personalizar más las respuestas
    use Rack::CustomLogger

    ####################
    #Rutas
    route do |r|
        @dator = FSDator.new("data")
        @gestor = GestorGrados.new(@dator)
        @parse = Parse.new
        #Directorio Raíz
        r.root do
            response.status = 200
            response['Content-Type'] = 'application/json'
            body = 
                {
                    "status"=>200
                }
            response.write(body.to_json)
        end

        # /grados
        r.on "grados" do
            # GET /grados
            # curl --request GET http://localhost:9292/grados
            r.get do
                #obtenemos todos los grados
                grados = Array.new
                grados = @gestor.todosGrados()
                gradosjson = Array.new
                #los pasamos a JSON
                for i in 0..grados.length()-1
                    gradosjson.push(@parse.gradoToJSON(grados[i]))
                end

                #preparamos la respuesta
                response.status = 200
                response['Content-Type'] = 'application/json'
                response.write(gradosjson.to_json)
            end
        end

        # /grado
        r.on "grado" do
            # /grado/$ID
            r.on String do |id|
                
                # Rama /grado/$ID/asignatura/$ID2
                r.on "asignatura" do
                    r.on String do |id2|
                        # /asignatura/$ID/horario
                        r.get "horario" do
                            begin
                                if r.params['grupo'] == nil
                                    response.status = 404
                                    response['Content-Type'] = 'application/json'
                                    res = {
                                        "error"=>"es necesario pasar la variable grupo"
                                    }
                                    response.write(res.to_json)   
                                else
                                    grupo = r.params['grupo']
                                    horario = @gestor.horarioAsignatura(id, id2, grupo)
                                    arrayHorario = Array.new
                                    for i in 0..horario.length()-1
                                        arrayHorario.push(@parse.horarioToJSON(horario[i]))
                                    end
                                    res = {
                                        "horario"=>arrayHorario
                                    }
                                    response.status = 200
                                    response['Content-Type'] = 'application/json'
                                    response.write(res.to_json)
                                end
                            rescue 
                                response.status = 404
                                    response['Content-Type'] = 'application/json'
                                    res = {
                                        "error"=>"No se ha encontrado el grado o asignatura"
                                    }
                                response.write(res.to_json)  
                            end
                        end

                        # grado/$ID1/asignatura/$ID2/enlace
                        r.get "enlace" do
                            begin
                                if r.params['grupo'] == nil
                                    response.status = 404
                                    response['Content-Type'] = 'application/json'
                                    res = {
                                        "error"=>"es necesario pasar la variable grupo"
                                    }
                                    response.write(res.to_json)   
                                else
                                    grupo = r.params['grupo']
                                    enlaces = @gestor.enlacesAsignatura(id, id2, grupo)

                                    res = {
                                        "enlace"=>enlaces
                                    }
                                    response.status = 200
                                    response['Content-Type'] = 'application/json'
                                    response.write(res.to_json)
                                end
                            rescue
                                response.status = 404
                                response['Content-Type'] = 'application/json'
                                res = {
                                    "error"=>"No se ha encontrado el grado o asignatura"
                                }
                                response.write(res.to_json)  
                            end
                        end

                        # grado/$ID1/asignatura/$ID/turnos
                        r.get "turno" do
                            begin
                                if r.params['turno'] == nil or r.params['mes'] == nil
                                    response.status = 404
                                    response['Content-Type'] = 'application/json'
                                    res = {
                                        "error"=>"es necesario pasar la variable turno y mes"
                                    }
                                    response.write(res.to_json)   
                                else
                                    turno = r.params['turno']
                                    mes = r.params['mes']
                                    turnos = @gestor.turnosAsignatura(id, id2, turno,mes)

                                    res = {
                                        "turnos"=>turnos
                                    }
                                    response.status = 200
                                    response['Content-Type'] = 'application/json'
                                    response.write(res.to_json)
                                end
                            rescue
                                response.status = 404
                                response['Content-Type'] = 'application/json'
                                res = {
                                    "error"=>"No se ha encontrado el grado o asignatura"
                                }
                                response.write(res.to_json)  
                            end
                        end
                            
                        # grado/$ID1/asignatura/$ID
                        # curl --request GET http://localhost:9292/grado/0e78a27a1e605334c0ba/asignatura/50bbd29ff87ba567f7bd
                        r.get do
                            begin
                                asignatura = @gestor.obtenerAsignatura(id, id2)
                                asigjson = @parse.asignaturaToJSON(asignatura)

                                #Preparamos la respuesta
                                response.status = 200
                                response['Content-Type'] = 'application/json'
                                response.write(asigjson.to_json)
                            rescue
                                response.status = 404
                                response['Content-Type'] = 'application/json'
                                res = {
                                    "error"=>"No existe el grado o la asignatura"
                                }
                                response.write(res.to_json)    
                            end
                            
                        end

                        r.delete do
                            begin
                                @gestor.eliminaAsignatura(id, id2)
                                res = {
                                    "eliminado"=>id2
                                }
                                response.status = 200
                                response['Content-Type'] = 'application/json'
                                response.write(res.to_json)
                            rescue
                                response.status = 404
                                response['Content-Type'] = 'application/json'
                                res = {
                                    "error"=>"No existe el grado o la asignatura"
                                }
                                response.write(res.to_json)
                            end
                        end
                    end

                    # post /grado/$ID/asignatura
                    # curl --header "Content-Type:application/json" --request POST --data '{"id":"50bbd29ff87ba567f7bd","siglas":"IV","nombre":"Infraestructura Virtual","horario_teoria":{"dia":"2-Martes","hora_inicio":"11:30","hora_fin":"13:30","grupo":"T"},"horario_practicas":[{"dia":"2-Martes","hora_inicio":"9:30","hora_fin":"11:30","grupo":"P1"},{"dia":"5-Viernes","hora_inicio":"9:30","hora_fin":"11:30","grupo":"P2"}],"turno_presencialidad":[["28sep - 2oct","12oct - 16oct","26oct - 30oct","9nov - 13nov","23nov - 27nov","7dec - 11dec","21dec - 22dec"],["5oct - 9oct","19oct - 23oct","2nov - 6nov","16nov - 20nov","30nov - 4dec","14dec - 18dec","8jan y 11jan - 14jan"]],"grupo":"A","enlaces_clase_online":["https://meet.jit.si/IV-ETSIIT-UGR-2020","https://meet.jit.si/IV-ETSIIT-UGR-2020","https://meet.jit.si/IV-ETSIIT-UGR-2020"],"curso":"4"}' http://localhost:9292/grado/0e78a27a1e605334c0ba/asignatura
                    r.post do
                        begin
                            asignatura = JSON.parse(r.body.read)
            
                            parsed = @parse.jsonToAsignatura(asignatura)
    
                            @gestor.añadeAsignatura(id ,parsed)
    
                            #Preparamos la respuesta
                            response.status = 200
                            response['Content-Type'] = 'application/json'
                            res = {
                                "añadido"=>parsed.id
                            }
                            response.write(res.to_json) 
                        rescue
                            response.status = 404
                            response['Content-Type'] = 'application/json'
                            res = {
                                "error"=>"No existe el grado o la asignatura"
                            }
                            response.write(res.to_json)
                        end
                    end
                end

                # /grado/$ID/asignaturas
                r.on "asignaturas" do
                    r.get do
                        begin
                            asignaturas = @gestor.todasAsignaturas(id)
                            asignaturasjson = Array.new
                            for i in 0..asignaturas.length()-1
                                asignaturasjson.push(@parse.asignaturaToJSON(asignaturas[i]))
                            end

                            #Preparamos la respuesta
                            response.status = 200
                            response['Content-Type'] = 'application/json'
                            response.write(asignaturasjson.to_json) 
                        rescue
                            response.status = 404
                            response['Content-Type'] = 'application/json'
                            res = {
                                "error"=>"No existe el grado o no contiene ninguna asignatura"
                            }
                            response.write(res.to_json)
                        end
                        
                    end
                end
                # get /grado/$ID
                r.get do
                    begin
                        grado = @gestor.obtenerGrado(id)
                        jsongrado = @parse.gradoToJSON(grado)
                        response.status = 200
                        response['Content-Type'] = 'application/json'
                        response.write(jsongrado.to_json) 
                    rescue
                        response.status = 404
                        response['Content-Type'] = 'application/json'
                        res = {
                            "error"=>"No existe el grado"
                        }
                        response.write(res.to_json)
                    end
                    
                end

                # delelete /grado/$ID
                r.delete do
                    begin
                        @gestor.eliminarGrado(id)
                        res = {
                            "eliminado"=>id
                        }
                        response.status = 200
                        response['Content-Type'] = 'application/json'
                        response.write(res.to_json) 
                    rescue
                        response.status = 404
                        response['Content-Type'] = 'application/json'
                        res = {
                            "error"=>"No existe el grado"
                        }
                        response.write(res.to_json)
                    end
                end

            end
            # post /grado
            r.post do
                begin
                    grado = JSON.parse(r.body.read)
                    parsed = @parse.jsonToGrado(grado)
                    id2 = @gestor.AnadirGrado(parsed)
                    res = {
                        "añadido"=>id2
                    }
                    response.status = 200
                    response['Content-Type'] = 'application/json'
                    response.write(res.to_json)      
                rescue
                    response.status = 404
                    response['Content-Type'] = 'application/json'
                    res = {
                        "error"=>"Error al añadir el grado"
                    }
                    response.write(res.to_json)
                end

            end
        end
    end
end
```

## Ejercicio 4
### Crear pruebas para las diferentes rutas de la aplicación.
Se pueden consultar en el siguiente [enlace](https://github.com/antoniocuadros/WhenToClass/blob/master/t/TestApi.rb)