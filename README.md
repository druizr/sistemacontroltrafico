# Sistema control de tráfico urbano
# Consulta de videos on-line y grabaciones.
Prototipo para el sistema de control de tráfico urbano

URL API: http://private-c9e3b-consultavideo.apiary-mock.com <br/>
Github: https://github.com/druizr/sistemacontroltrafico

## API Blue print

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
        
## Alarma
Grupo del recurso Alarmas.

## Alarma [/Alarmas/{IdAlarma}]
Opciones para el recurso de las Alarmas.

+ Parameters

    + IdAlarma: 1 (number) - Identificador unico de Camara.
    
### Crear una Alarma [POST]

+ Request Plain Text Message

    + Headers

            Accept: text/plain

+ Response 200 (text/plain)

    + Headers

            X-My-Message-Header: 50

    + Body

            Grabación encontrada

+ Request JSON Message

    + Headers

            Accept: application/json
    + Body

            {
              "IdAlarma"     :1,
              "IdCamara"     :"1"
              "TipoAlarma"   :"Error"
            }

+ Response 200 (application/json)

    + Headers

            X-My-Message-Header: 50

### Devuelve una Alarma [GET]

+ Request Plain Text Message

    + Headers

            Accept: text/plain

+ Response 200 (text/plain)

    + Headers

            X-My-Message-Header: 50

    + Body

            Camara encontrada

+ Request JSON Message

    + Headers

            Accept: application/json

+ Response 200 (application/json)

    + Headers

            X-My-Message-Header: 50

    + Body

            {
              "IdCamara"          :1,
              "NroCamara"         :"1",
              "IP"                :"192.168.1.200",
              "LocalizacionGPS"   :"-43.000101, -87.01212"
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

# Imagen
Recurso Imagen.

## Imagen [/Imagenes/{IdImagen}]
Recurso donde se encuentran las opciones para el recurso de las Imagenes.

+ Parameters

    + IdImagen: 1 (number) - Identificador unico de una Imagen.

### Crear una Imagen [POST]

+ Request Plain Text Message

    + Headers

            Accept: text/plain

+ Response 200 (text/plain)

    + Headers

            X-My-Message-Header: 50

    + Body

            Imagen encontrada

+ Request JSON Message

    + Headers

            Accept: application/json
    + Body

            {
              "NroFotograma" :1,
              "TiempoMs"     :"1000",
              "NroCamara"    :"1"
            }

+ Response 200 (application/json)

    + Headers

            X-My-Message-Header: 50

### Devuelve una Imagen [GET]

+ Request Plain Text Message

    + Headers

            Accept: text/plain

+ Response 200 (text/plain)

    + Headers

            X-My-Message-Header: 50

    + Body

            Imagen encontrada

+ Request JSON Message

    + Headers

            Accept: application/json

+ Response 200 (application/json)

    + Headers

            X-My-Message-Header: 50

    + Body

            {
              "IdImagen"     :1,
              "NroFotograma" :1,
              "TiempoMs"     :"1000",
              "NroCamara"    :"1"
            }

## Todas las Imagenes [/imagen{?limit}]
Lista todas las imagenes que forman un video de el sistema de vigilancia de trafico.

### Devuelve todas las Imagenes [GET]

+ Parameters

    + limit (number, optional) - El maximo numero de imagenes mostradas en pantalla.
        + Default: `20`

+ Response 200 (application/json)

        [
          {
              "IdImagen" :1,
              "NroFotograma" :1,
              "TiempoMs"     :"1000",
              "NroCamara"    :"1"
          },
          {
              "IdImagen"    :2,
              "NroFotograma" :2,
              "TiempoMs"     :"1000",
              "NroCamara"    :"1"
          },
          {
              "IdImagen"    :3,
              "NroFotograma" :3,
              "TiempoMs"     :"1000",
              "NroCamara"    :"1"
          }
        ]            
            
# Group SobreImpresion
Grupo del recurso Sobreimpresion.

## SobreImpresion [/Sobreimpresiones/{IdSobreImpresion}]
Recurso donde se encuentran las opciones para el recurso de las sobreimpresiones de informacion que van insertos dentro de los videos.

+ Parameters

    + IdSobreImpresion: 1 (number) - Identificador unico de Disco.

### Crear una Sobre Impresión [POST]

+ Request Plain Text Message

    + Headers

            Accept: text/plain

+ Response 200 (text/plain)

    + Headers

            X-My-Message-Header: 50

    + Body

            Sobreimpresion Creada!

+ Request JSON Message

    + Headers

            Accept: application/json
    + Body

            {
              "NroCamara"                 :"1",
              "AmbitoOrden"               :"",
              "NroBloquesSobreimpresion"  :"35",
              "CoordSobreImpresion"       :"42/45",
              "AtribSobreImpresion"       :"Hora",
              "TipoInformacion"           :"Hora",
              "Tamano"                    :"10",
              "TipoCaracteres"            :"ASCII"
            }

+ Response 200 (application/json)

    + Headers

            X-My-Message-Header: 50

### Devuelve una sobreimpresion [GET]

+ Request Plain Text Message

    + Headers

            Accept: text/plain

+ Response 200 (text/plain)

    + Headers

            X-My-Message-Header: 50

    + Body

            Sobreimpresion encontrada

+ Request JSON Message

    + Headers

            Accept: application/json

+ Response 200 (application/json)

    + Headers

            X-My-Message-Header: 50

    + Body

            {
              "IdSobreImpresion"          :1,
              "NroCamara"                 :"1",
              "AmbitoOrden"               :"",
              "NroBloquesSobreimpresion"  :"35",
              "CoordSobreImpresion"       :"42/45",
              "AtribSobreImpresion"       :"Hora",
              "TipoInformacion"           :"Hora",
              "Tamano"                    :"10",
              "TipoCaracteres"            :"ASCII"
            }

### Edita un Sobreimpresion [PUT]

+ Request Update Plain Text Message (text/plain)

        Actualizado correctamente!

+ Request Update JSON Message (application/json)

        { "message": "Actualizado correctamente!" }

+ Response 204

## Elimina Sobreimpresion [DELETE /sobreimpresion/{IdSobreImpresion}]

+ Parameters
    + IdSobreImpresion (int)

+ Response 204

## Todos las SobreImpresiones [/Sobreimpresion{?limit}]
Lista todas las sobreimpresiones de los videos del sistema de vigilancia de trafico.

### Devuelve todos los Sobreimpresiones [GET]

+ Parameters

    + limit (number, optional) - El maximo numero de Sobreimpresiones mostrados en pantalla.
        + Default: `20`

+ Response 200 (application/json)

        [
          {
              "IdSobreImpresion"          :1,
              "NroCamara"                 :"1",
              "AmbitoOrden"               :"",
              "NroBloquesSobreimpresion"  :"35",
              "CoordSobreImpresion"       :"42/45",
              "AtribSobreImpresion"       :"Hora",
              "TipoInformacion"           :"Hora",
              "Tamano"                    :"10",
              "TipoCaracteres"            :"ASCII"
          },
          {
              "IdSobreImpresion"          :2,
              "NroCamara"                 :"2",
              "AmbitoOrden"               :"",
              "NroBloquesSobreimpresion"  :"35",
              "CoordSobreImpresion"       :"42/45",
              "AtribSobreImpresion"       :"Hora",
              "TipoInformacion"           :"Hora",
              "Tamano"                    :"10",
              "TipoCaracteres"            :"ASCII"
          },
          {
              "IdSobreImpresion"          :3,
              "NroCamara"                 :"3",
              "AmbitoOrden"               :"",
              "NroBloquesSobreimpresion"  :"35",
              "CoordSobreImpresion"       :"42/45",
              "AtribSobreImpresion"       :"Hora",
              "TipoInformacion"           :"Hora",
              "Tamano"                    :"10",
              "TipoCaracteres"            :"ASCII"
          }
        ]

