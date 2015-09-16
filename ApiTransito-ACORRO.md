FORMAT: 1A
HOST: http://videotransito.acorro.apiblueprint.org/

# VideoTransito
Servicios para Sistema de control de transito vehicular

## Video [/video/{id_video}]
Grabaciones de Camaras de Control de Transito

Atributos:

- `id_video`        Unique
- `fecha`


+ Parameters
    + id_video (required, int) ... PK video

+ Model (application/hal+json)

    + Body

            {
                "id_video": 1,
                "fecha": "10-09-2015 11:00",
                "descargar_video": "http://controltransito/download/video_1"
            }
            
## Buscar Video [GET]

+ Response 200 (application/json)


+ Response 404 (application/json)

        { 
            "error": "Video no se encuentra" 
        }

+ Response 404

        { 
            "error": "Video no disponible"
        }


## Eliminar Video [DELETE]

+ Response 200

        { 
            "result": True,
            "message": "Video eliminado con éxito"
        }

    

# ListaVideos [/video]
Obtener todos los videos

+ Model (application/hal+json)

    + Body

            {
                "video": [
                    {
                        "id_video": 1,
                        "inicio_transmision": "10-09-2015 11:00",
                        "fin_transmision": "10-09-2015 12:00",
                        "descargar_video": "http://controltransito/download/video_1"
                    },
                    {
                        "id_video": 2,
                        "inicio_transmision": "10-09-2015 12:00",
                        "fin_transmision": "10-09-2015 13:00",
                        "descargar_video": "http://controltransito/download/video_2"
                    },{
                        "id_video": 3,
                        "inicio_transmision": "10-09-2015 13:00",
                        "fin_transmision": "10-09-2015 14:00",
                        "descargar_video": "http://controltransito/download/video_3"
                    }
                ]
            }


## Obtener lista de videos [GET]

+ Response 200

    [ListaVideos][]


# ReproducirVideo [/video/{id_video}/reproducir]
Reproducir video 

+ Model (application/hal+json)

    + Body

            {
                "id_video": 3,
                "status": "offline",
                "inicio_transmision": "10-09-2015 13:00",
                "fin_transmision":"10-09-2015 14:00"
            }


## Buscar y reproducir video [GET]

+ Response 200

    [ReproducirVideo][]


## Camara [/camara/{id_cam}]
Recurso Cámaras 

Atributos Obligatorios: 

- `id_cam`        Unique
- `detalle_cam`
- `dir_ip`
- `coord_gps`


+ Parameters
    + id_cam (required, int) ... PK Camara

+ Model (application/hal+json)

    + Body

            {
                "id_cam": 1,
                "detalle_cam":"Camara x HD Pro 1",
                "dir_ip":"129.200.1.100",
                "latitud":"-33.000101",
                "longitud":"-77.01212",
            }
            
## Buscar Camara [GET]

+ Response 200 (application/json)


+ Response 404 (application/json)

        { 
            "error": "Camara no encontrada" 
        }
    
## Eliminar Camara [DELETE]

+ Response 200

        { 
            "result": True,
            "message": "Camara eliminada del sistema"
        }

## Agregar Camara [POST]

+ Request (application/json)

        {
            "detalle_Cam":"Camara x HD Pro 2",
            "dir_ip":"129.200.1.151",
            "latitud":"-33.000505",
            "longitud":"-77.01616",
        }

+ Response 201


    
+ Response 400

        { 
            "error": "Error al agregar la camara"
        }

# ListaCamaras [/camara]
Obtener todas las cámaras registradas

+ Model (application/hal+json)

    + Body

            {
                "camara": [
                    {
                        "id_cam": 1,
                        "detalle_cam":"Camara x HD Pro 1",
                        "dir_ip":"129.200.1.100",
                        "latitud":"-33.000101",
                        "longitud":"-77.01212",
                    },{
                        "id_cam": 2,
                        "detalle_cam":"Camara x HD Pro 2",
                        "dir_ip":"129.200.1.151",
                        "latitud":"-33.000505",
                        "longitud":"-77.01616",
                    }
                ]
            }


## Obtener lista de cámaras [GET]

+ Response 200

    [ListaCamaras][]

# ReproductorLocal [/camara/{id_cam}/reproducir]
Reproducir Video Localmente

+ Model (application/hal+json)

    + Body

            {
                "id_cam": 1,
                "detalle_cam":"Camara x HD Pro 1",
                "dir_ip":"129.200.1.100",
                "latitud":"-33.000101",
                "longitud":"-77.01212",
                "Video":{
                    "id_video": 1,
                    "descargar_video": "http://controltransito/download/video_1"
                },
                "transmision":{
                    "id_trans": 1,
                    "descripción": "Descripción video tiempo real",
                    "source":"http://controltransito/streaming/1/play"
                }
            }


## Buscar y transmitir video [GET]

+ Response 200

    [ReproductorLocal][]


## GrabarDisco [/disco/{id_disco}]
Grabar video Disco Local

Atributos Obligatorios: 

- `id_disco`          Autoincrementable
- `detalles`


+ Parameters
    + id_disco (required, int) ... PK Video

+ Model (application/hal+json)

    + Body

            {
                "id_disco": 1,
                "inicio_grabación":"10-09-2015 18:00",
                "video":{
                    "id_video": 2,
                    "inicio_transmision": "10-09-2015 11:00",
                    "fin_transmision": "10-09-2015 12:00",
                }

            }
            
## Buscar video Disco [GET]

+ Response 200 (application/json)


    
+ Response 404 (application/json)

        { 
            "error": "Disco no se encuentra" 
        }

## Detener grabación Disco [DELETE]

+ Response 200

        { 
            "result": True,
            "message": "Detener grabación Disco"
        }

## Nueva grabación Disco [POST]

+ Request (application/json)

        {
            "id_video":1
        }

+ Response 201

    [GrabarDisco][]
    
+ Response 400

        { 
            "error": "Error al crear Disco Video"
        }




## TransmisionOn-Line [/transmision/{id_trans}]
Reproducir video en tiempo real

Atributos Obligatorios: 

- `id_trans`          Autoincrementable
- `caracteristicas` 


+ Parameters
    + id_trans (required, int) ... PK broadcast

+ Model (application/hal+json)

    + Body

            {
                "id_trans": 1,
                "descripción": "Video tiempo real Camara 1",
                "source":"http://controltransito/streaming/1/play",
                "camara":{
                    "id_cam": 1,
                    "detalle_cam":"Camara x HD Pro 1",
                    "dir_ip":"129.200.1.101",
                    "latitud":"-33.000101",
                    "longitud":"-77.01212",
                },
                "video":{
                    "id_video": 1,
                    "descargar_video": "http://controltransito/download/video_1"
                }
            }
            
## Buscar transmision [GET]

+ Response 200 (application/json)


    
+ Response 404 (application/json)

        { 
            "error": "Transmision no se encuentra" 
        }

## Editar Transmision [PATCH]

+ Request (application/json)

        {
            "descripción": "Cambio detalles Transmision"
        }

+ Response 200
    
        { 
            "result": True,
            "message": "Transmision editado con éxito"
        }

+ Response 404

        { 
            "error": "Transmision no disponible"
        }

+ Response 400

        { 
            "error": "Fallo al modificar el detalle de Transmision"
        }

## Detener Transmision [DELETE]

+ Response 200

        { 
            "result": True,
            "message": "Se detuvo la Transmision"
        }
