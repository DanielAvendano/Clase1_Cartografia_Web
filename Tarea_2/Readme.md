## 1. Definicion del problema

* El problema a solucionar es encontrar las manzanas en la localidad de San Cristobal las cuales se encuentran a mas de 200 metros de un paradero del SITP, y con esto garantizar que todas las manzanas tengan un paradero a por lo menos 200 metros lo que le tomaria a una persona promedio llegar caminando al paradero entre 2 y 3 minutos teniendo en cuenta que la velocidad de una persona adulta al caminar son 83 metros por minuto.

* Se propone:
- Extraer los datos de la capa localidades para tener solamente la localidad de San Cristobal
- Extraer los paraderos del sitp que se encuentran en la localidad de San Cristobal
- Realizar un Intersect para determinar las manzanas que se encuentran en la localidad de San Cristobal
- Realizar un Buffer a los paraderos del Sitp, para calcular su area de cobertura.
- Realizar una consulta por localizacion para determinar cuales manzanas no tienen cobertura de los paraderos del SITP en San Cristobal

## 2. Fuente de datos

* Localidades

* Manzanas

* Paraderos del SITP

## 3. Procesamiento de datos

Para procesar los datos se va a usar la herramienta postgres, como el ejercicio que voy a trabajar solo necesita datos de una localidad entonces se procedio a realizar una base de datos diferente para trabajar los datos, y despues si cargarlos a la destinada para la clase.

* Primero se debe crear la base de datos
imagen001
* se verifica y la extension de postgis no esta activa
imagen002
* se procede a activar la extension de postgis
imagen003
* para cargar los datos a la base de datos debemos hacer uso de la herramienta QGIS, primero se debe hacer la conexion a la base de datos, en la ventana "Browser" damos click derecho a la opcion "PosGIS" y se despliega una herramienta que dice "New Connection..." esto despliega una ventana que nos permitira conectar a la base de datos anteriormente creada y se llena de la siguiente manera
imagen004
* posteriormente cargamos las capas que vamos a utilizar en el ejercicio seleccionamos la pestaña "Database" y la opcion "DB Manager..." y se tiene la siguiente ventana, ahi nos aseguramos de conectarnos a la base de datos de interes
imagen005
* en la ventana de "DB Manager" se selecciona el boton "Import/Layer File..." y se importan las tres capas de la siguiente manera
imagen006, imagen007, imagen008
* ya se puede trabajar desde la base de datos creada anteriormente
* como se requiere hacer solo el analisis de la localidad de San Cristobal, se procede a extraer esa localidad y que nos cree una nueva tabla con solo esa localidad.
imagen009, imagen009a
* para los paraderos del sitp tambien extraemos los datos que se encuentran unicamente en la localidad de San Cristobal, y se crea una nueva tabla con estos paraderos.
imagen010, imagen010a
* para las manzanas tambien extraemos unicamente las que se encuentran en la localidad de San Cristobal, como la capa de manzanas no cuenta con el atributo localidad se hace uso de la funcion intersects y se crea una nueva tabla con esas manzanas
imagen011, imagen011a
* Se realizo un buffer de 200 metros a cada paradero de sitp en la localidad de San Cristobal, y tambien se realizo una union para que solo se tuviera un poligono resultante, y se le calculo el area de la siguiente manera.
imagen012
* se obtiene que los paraderos del sitp de la localidad de San Cristobal, tienen una area de influencia de 14455512,617306 metros cuadrados 
imagen013
* se procedio a calcular cuales manzanas se encontraban fuera de la cobertura del area de influencia.
imagen014
* y se muestran a continuacion en color rojo
imagen014a
* tambien se calculo cuales manzanas no se suplia totalmente la cobertura del area de influencia de 200 metros.
imagen015
* y se muestran a continuacion en color amarillo
imagen015a

#### Cargar capas a GEOSERVER

* se selecciona la pestaña "Database" y la opcion "DB Manager..." y se tiene la siguiente ventana, ahi nos aseguramos de conectarnos a la base de datos del curso
imagen016
* en la ventana de "DB Manager" se selecciona el boton "Import/Layer File..." y se importan las capas de la siguiente manera:
- capa da_paraderos_sitp_san_cristobal
imagen017
- capa da_manzanas_sin_cobertura_completa
imagen018
- capa da_manzanas_sin_cobertura
imagen019
- capa da_buffer_200_paraderos
imagen020
- capa da_manzanas_san_cristobal
imagen021
- capa da_localidad_san_cristobal
imagen022
* en la ruta del geoserver se da click en el boton "Capas" ubicado en Datos y se le da la opcion de agragar nuevo recurso.
imagen023, imagen024
* se selecciona la base de datos 
imagen025
* y se escoje la capa que se va a publicar y se le ajustan los datos de la siguiente manera
imagen026
* ese proceso se realiza con todas las capas que se requieren publicar
* se hace la verificacion de que las capas esten publicadas
imagen027


## 4. Capa simbología SLD

* Para crear la simbologia en formato SLD se debe tener la capa desplegada en QGIS, y se le da click derecho y la opcion "Properties..."
* se ajusta la simbologia de la manera adecuada
imagen028
* se presiona el boton "Style" y se despliega una barra de opciones se debe seleccionar "Save Style..." 
imagen029
* para cargar el estilo al Geoserver, se da click en el boton estilos, y en el boton agregar un nuevo estilo
* se introducen los datos de las siguiente manera
imagen030
* se realizo para la capa "da_localidad_san_cristobal"
* se introduce el codigo 
-- codigo sld
* previsualizacion de la leyenda
imagen031
* previsualizacion de la capa
iamgen031a
* se realizo para la capa "da_paraderos_sitp_san_cristobal"
* codigo
-- codigo sld
* previsualizacion de la leyenda
imagen032
* previsualizacion de la capa
iamgen032a
* se realizo para la capa "da_buffer_200_paraderos"
* se introduce el codigo 
-- codigo sld
* previsualizacion de la leyenda
imagen033
* previsualizacion de la capa
iamgen033a

## 5. Capa simbología CSS

* Para crear la simbologia en CSS debemos acceder a la pagina de geoserver y en la pestaña estilos agregar uno nuevo, se llenan los campos como acontinuacion y se escoje el formato "CSS" y en "Style Content" se selecciona polygon y generate para que genere el codigo
imagen034
* se modifica el codigo para que quede de la siguiente manera
image035
* previsualizacion de la leyenda
imagen036
* previsualizacion de la capa
iamgen036a


## 6. Capa simbologia YSLD

## 7. grupo de capas 

#### Layer group
* Para crear el grupo de capas con el boton "Grupos de Capas" y se llenan los datos de la siguiente manera

* se cargan las capas de la siguiente manera y por el momento se les asigna la simbologia por defecto.

#### Previsualización

## 8. Concluciones

* Video Loom