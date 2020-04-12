
##  1. Cuál es el problema a tratar?

 El problema a tratar es, calcular cual localidad cuenta con mas parques que tengan canchas sinteticas, y la cercania de ciclorutas a estos parques

## 2. Por qué los datos geográficos ayudan a resolverlo?

Los datos geográficos ayudan a resolverlo, ya que brindan el componente espacial lo cual nos permite vincular varias capas y asi poder obtener una solución a nuestro problema
   
## 3. Descripción de la solución propuesta.

La solucion propuesta es:

* Cargar las capas de localidades, canchas, y ciclorutas.

* Realizar un Join para poder determinar que el parque y el nombre de la localidad la cual se llamara "Join_Loc_Parques".

* Crear un buffer de 100 metros a las parques de esa localidad, el cual se llamara "Buff_100_Parques".

* Hacer un Intersect entre el buffer de las canchas (Buff_100_Parques) y la capa de ciclorutas, para determinar si existen ciclorutas a menos de 100 mentros de las canchas, esta capa se llamara "Int_Ciclo_Parques".
    
## 4. Listado detallado de las fuentes de datos seleccionadas.

* Capa de Localidades
    - Base de datos: GDR_V12.19.gdb
    - Dataset: Entidad_Territorial
    - Feature Class: Loca
    - Atributos que se tuvieron en cuenta: LocNombre, LocCodigo
    - Link de descarga: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

* Capa de ciclorutas 
    - Base de datos: GDR_V12.19.gdb
    - Dataset: Transporte_Terrestre
    - Feature Class: RBic
    - Atributos que se tuvieron en cuenta:
    - Link de descarga: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

* Capa de Canchas Sinteticas 
    - Atributos que se tuvieron en cuenta: Parque, Localidad
    - Link de descarga: http://datosabiertos.bogota.gov.co/dataset/canchas-sinteticas

## 5. Descripción detallada del procesamiento realizado a los datos 

* Lo primero que debemos hacer es garantizar que todas las capas esten en el mismo sistema de coordenadas
    - ![Imagen001](Imagenes/Imagen001.png), Imagen002, Imagen003
* Como las capas estan en otro sistema de coordenadas debemos cambiarlo a Colombia Bogota Zone para trabajar todas en el mismo sistema y que podamos trabajar las medidas en metros
* Se hace el siguiente procedimiento para las tres capas
    - Imagen004
* Y debemos tener todas las capas de la siguiente manera
    - Imagen005a, Imagen005b, Imagen005c
* Teniendo ya las tres capas en el mismo sistema de referencia se procede a hacer el Join
    - Imagen006
* Y se obtiene el siguiente resultado
    - Imagen007
* Para poder agrupar los datos debemos abrir la tabla de atributos y la herramienta Field Calculator, y se escribe la siguiente sentencia
    - Imagen008
* Y de ahi obtenemos que la localidad con mas parques es suba con 9 parques
    - Imagen009
* Se procede a seleccionar los parques de Suba
    - Imagen010
* Y posteriormente el Buffer a los parques, Para esto necesitamos ir a la pestaña "Vector", la opcion "Geoprocessing Tools" y la herramienta "Buffer", se despliega una ventana y llenamos los campos de la manera
    - Imagen011
* Y obtenemos el siguiente resultado
    - Imagen012
* Como la capa de RBic tiene dominios debemos agregar esos dominios en qgis, de la siguiente manera
    - Imagen013, Imagen014
* Ahora realizamos el intersect para ver que parques tienen una cicloruta a menos de 100 metros, para el intersect debemos ir a la pestaña "Vector", la opcion "Geoprocessing Tools" y la herramienta "Intersection...", se despliega una ventana y llenamos los campos de la siguiente manera
    - Imagen015
* Y obtenemos el siguiente resultado
    - Imagen016

## 6. Descripción detallada de la metodología utilizada para generar los mapas 

* La metodologia utilizada para generar los mapas fue:
* A la capa localidades un color solido con transparencia y mostrar los nombres de las localidades
    - Imagen017, Imagen018
* La capa quedo de la siguiente manera
    - Imagen019
* A la capa parques se le puso un color solido sin transparencia y tambien se muestran todos los nombres
    - Imagen020, Imagen021
* La capa quedo de la siguiente manera
    - Imagen022
* Para la capa RBic, se le asigno una simbologia categorizada ya que habian varias clases, y se le asigno una rampa en color gris
    - Imagen023
* La capa resulto como se muestra a continuacion 
    - Imagen024
* Para la Capa de Buffer se le asigno una simbologia de poligono sin relleno y linea punteada al rededor
    - Imagen025
* se muestra el resultado en la siguiente imagen
    - Imagen026
* Para la capa Intersect, se le asigno una simbologia categorizada ya que habian dos clases, y se le asignaron colores que destacaran
    - Imagen027
* Se muestra el resultado a continuacion
    - Imagen028



## 7. Descripción detallada del procedimiento técnico utilizado para generar los mapas.

## 8. Adicionar al repositorio github los archivos generados

## 9. Urls de los mapas publicados en la web
    
## 10. Conclusiones Ventajas / desventajas / dificultades encontradas durante el desarrollo del ejercicio
