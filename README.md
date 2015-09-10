# Sistema control de tráfico urbano
# Consulta de videos on-line y grabaciones.
Prototipo para el sistema de control de tráfico urbano

URL API: http://private-c9e3b-consultavideo.apiary-mock.com <br/>
Github: https://github.com/druizr/sistemacontroltrafico

## API Blueprint

+ [Documentación API](http://docs.consultavideo.apiary.io/)
# Videos [/videos/{?id}]

+ Parámetros
    + id (int) ID Video
    + inicio_transmision_video (datetime)

## Lista de videos [GET /videos/]

+ Response 200 (application/json)

        {
            "videos": [
                {
                    "id": 1,
                    "inicio_transmision_video": "31-08-2015 00:01",
                    "fin_transmision_video": "02-09-2015 23:59",
                    "tamano_video": "2 GB",
                    "descargar_video": "http://consultavideo/download/video_1"
                }
            ]
        }

## Buscar video [GET /videos/{id}]
Buscar video por su identificador único (ID)

+ Parameters
    + id (int) ID Video

+ Response 200 (application/json)

        {
            "id": 1,
            "inicio_transmision_video": "31-08-2015 00:01",
            "fin_transmision_video": "02-09-2015 23:59",
            "tamano_video": "2 GB",
            "descargar_video": "http://consultavideo/download/video_1"
        }

## Eliminar video [DELETE /videos/{id}]
+ Parameters
    + id (int) ID Video

+ Response 200 (application/json)

        {
            "result": True,
            "message": "El video ha sido eliminado con éxito"
        }

## Reproducir video [GET /videos/{id}/reproducir]

+ Parameters
    + id (int) ID Video

+ Response 200 (application/json)

        {
            "id": 1,
            "inicio_transmision_video": "31-08-2015 00:01",
            "fin_transmision_video": "02-09-2015 23:59",
            "tamano_video": "2 GB",
            "descargar_video": "http://consultavideo/download/video_1"
            "source_video":"http//consultavideo/replay/1"
        }
        
# Camaras [/camaras/{?id}]

+ Parámetros
    + id (int) ID Cámara
    + periodo
    + marca
    + brillo
    + calidad
    + color
    + contraste
    + ip
    + coodenadas

## Lista de cámaras [GET /camaras/]

+ Response 200 (application/json)

        {
            "Listado de camaras": [
                {
                    "id": 1,
                    "marca":"Samsung UltraHD Pro",
                    "fecha_agregada":"30-08-2015",
                    "ip":"192.168.1.200",
                    "latitud":"-43.000101",
                    "longitud":"-87.01212",
                    "configuración":{
                        "brillo": 20,
                        "calidad": "1024p",
                        "color":"rgba(0,0,0)",
                        "contraste":"25"
                    }
                }
            }
            ]
        }

## Buscar Cámara [GET /camaras/{id}]

+ Response 200 (application/json)

        {
            "id": 1,
            "marca":"Samsung UltraHD Pro",
            "fecha_agregada":"30-08-2015",
            "ip":"192.168.1.200",
            "latitud":"-43.000101",
            "longitud":"-87.01212",
            "configuración":{
                "brillo": 20,
                "calidad": "1024p",
                "color":"rgba(0,0,0)",
                "contraste":25
            }
        }
+ Response 404 (application/json)

        { 
            "error": "Camara no se encuentra disponible" 
        }

### Editar Cámara [PATCH /camaras/{id}]

+ Request (application/json)

        {
            "brillo": 20,
            "contraste": 25,
        }

+ Response 200

        {
            "id": 1,
            "marca":"Samsung UltraHD Pro",
            "fecha_agregada":"05-09-2015",
            "ip":"192.168.1.200",
            "latitud":"-43.000101",
            "longitud":"-87.01212",
            "configuración":{
                "brillo": 20,
                "calidad": "1024p",
                "color":"rgba(0,0,0)",
                "contraste":25
            }
        }

+ Response 404

        { 
            "error": "Recurso no disponible"
        }

+ Response 400

        { 
            "error": "Fallo al modificar el Recurso"
        }
        
## Eliminar Cámara [DELETE /camaras/{id}]

+ Response 200

        { 
            "result": True,
            "message": "Cámara eliminada con éxito"
        }

## Añadir Cámara [POST /camaras]

+ Request (application/json)

        {
            "marca":"Samsung UltraHD 4K Pro",
            "fecha_add":"30-08-2015",
            "brillo": 10,
            "calidad": "1024p",
            "color":"rgba(0,0,0)",
            "contraste":25
            
        }
        
+ Response 201

        {
            "id": 2,
            "marca":"Samsung UltraHD 4K Pro",
            "fecha_add":"30-08-2015",
            "ip":"192.168.1.201",
            "latitud":"-43.000101",
            "longitud":"-87.01212",
            "configuración":{
                "brillo": 10,
                "calidad": "1024p",
                "color":"rgba(0,0,0)",
                "contraste":30
            }
        }
        
# Transmitir video [GET /camaras/{id}/transmitir]

+ Response 200

        {
            "id": 1,
            "marca":"Samsung UltraHD Pro",
            "fecha_add":"31-08-2015",
            "ip":"192.168.1.200",
            "latitud":"-43.000101",
            "longitud":"-87.01212",
            "configuración":{
                "brillo": 10,
                "calidad": "1024p",
                "color":"rgba(0,0,0)",
                "contraste":"25"
            },
            "Video":{
                "id": 1,
                "descargar_video": "http://consultavideo/download/video_1"
            },
            "broadcast":{
                "id": 1,
                "inicio_broadcast":"31-08-2015 12:00",
                "descripción": "Transmision de video tiempo real",
                "source":"http://consultavideo/broadcast/1/play",
                "fps":30
            }
        }


## Buscar video - CD [GET /grabar-video/{id}]

+ Response 200 (application/json)

        {
            "id": 1,
            "inicio_grabación":"30-08-2015 00:00",
            "tasa_vehiculo": "-",
            "tipo_fichero":"avi",
            "compresion":"format-x",
            "secuencias_grabadas":250,
            "total_secuencias":6581,
            "video":{
                "id": 2,
                "inicio_transmision": "31-08-2015 00:01",
                "fin_transmision": "01-09-2015 23:59",
                "tamano_video": "2 GB",
            }

        }
    
+ Response 404 (application/json)

        { 
            "error": "Recurso no se encuentra" 
        }

# Broadcast [/broadcast/{id}]

+ Parámetros
    + id (int) ID Broadcast
    + descripcion
