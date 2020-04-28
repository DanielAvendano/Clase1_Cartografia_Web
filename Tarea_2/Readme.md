## 1. Definicion del problema

* El problema a solucionar es encontrar las manzanas en la localidad de San Cristobal las cuales se encuentran a mas de 200 metros de un paradero del SITP, y con esto garantizar que todas las manzanas tengan un paradero a por lo menos 200 metros lo que le tomaria a una persona promedio llegar caminando al paradero entre 2 y 3 minutos teniendo en cuenta que la velocidad de una persona adulta al caminar son 83 metros por minuto.
* Los datos geográficos ayudan a resolverlo, ya que brindan el componente espacial lo cual nos permite vincular varias capas y asi poder obtener una solución a nuestro problema
* Se propone:
- Extraer los datos de la capa localidades para tener solamente la localidad de San Cristobal
- Extraer los paraderos del sitp que se encuentran en la localidad de San Cristobal
- Realizar un Intersect para determinar las manzanas que se encuentran en la localidad de San Cristobal
- Realizar un Buffer a los paraderos del Sitp, para calcular su area de cobertura.
- Realizar una consulta por localizacion para determinar cuales manzanas no tienen cobertura de los paraderos del SITP en San Cristobal

## 2. Fuente de datos
* Capa de Localidades
    - Base de datos: GDR_V12.19.gdb
    - Dataset: Entidad_Territorial
    - Feature Class: Loca
    - Atributos que se tuvieron en cuenta: LocNombre, LocCodigo
    - Link de descarga: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

* * Manzanas
    - Base de datos: GDR_V12.19.gdb
    - Dataset: Area Catastral
    - Feature Class: Manz
    - Atributos que se tuvieron en cuenta: mancodigo, seccodigo
    - Link de descarga: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

* * Paraderos del SITP
    - Base de datos: GDR_V12.19.gdb
    - Dataset: Transporte_terrestre
    - Feature Class: Psitp
    - Atributos que se tuvieron en cuenta: localidad
    - Link de descarga: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

## 3. Procesamiento de datos

Para procesar los datos se va a usar la herramienta postgres, como el ejercicio que voy a trabajar solo necesita datos de una localidad entonces se procedio a realizar una base de datos diferente para trabajar los datos, y despues si cargarlos a la destinada para la clase.

* Primero se debe crear la base de datos

![imagen001](Imagenes/imagen001.PNG "imagen001")
* se verifica y la extension de postgis no esta activa

![imagen002](Imagenes/imagen002.PNG "imagen002")
* se procede a activar la extension de postgis

![imagen003](Imagenes/imagen003.PNG "imagen003")
* para cargar los datos a la base de datos debemos hacer uso de la herramienta QGIS, primero se debe hacer la conexion a la base de datos, en la ventana "Browser" damos click derecho a la opcion "PosGIS" y se despliega una herramienta que dice "New Connection..." esto despliega una ventana que nos permitira conectar a la base de datos anteriormente creada y se llena de la siguiente manera

![imagen004](Imagenes/imagen004.PNG "imagen004")
* posteriormente cargamos las capas que vamos a utilizar en el ejercicio seleccionamos la pestaña "Database" y la opcion "DB Manager..." y se tiene la siguiente ventana, ahi nos aseguramos de conectarnos a la base de datos de interes

![imagen005](Imagenes/imagen005.PNG "imagen005")
* en la ventana de "DB Manager" se selecciona el boton "Import/Layer File..." y se importan las tres capas de la siguiente manera

![imagen006](Imagenes/imagen006.PNG "imagen006")

![imagen007](Imagenes/imagen007.PNG "imagen007")

![imagen008](Imagenes/imagen008.PNG "imagen008")
* ya se puede trabajar desde la base de datos creada anteriormente
* como se requiere hacer solo el analisis de la localidad de San Cristobal, se procede a extraer esa localidad y que nos cree una nueva tabla con solo esa localidad.

![imagen009](Imagenes/imagen009.PNG "imagen009")

![imagen009](Imagenes/imagen009a.PNG "imagen009a")
* para los paraderos del sitp tambien extraemos los datos que se encuentran unicamente en la localidad de San Cristobal, y se crea una nueva tabla con estos paraderos.

![imagen010](Imagenes/imagen010.PNG "imagen010")

![imagen010a](Imagenes/imagen010a.PNG "imagen010a")
* para las manzanas tambien extraemos unicamente las que se encuentran en la localidad de San Cristobal, como la capa de manzanas no cuenta con el atributo localidad se hace uso de la funcion intersects y se crea una nueva tabla con esas manzanas

![imagen011](Imagenes/imagen011.PNG "imagen011")

![imagen011a](Imagenes/imagen011a.PNG "imagen011a")
* Se realizo un buffer de 200 metros a cada paradero de sitp en la localidad de San Cristobal, y tambien se realizo una union para que solo se tuviera un poligono resultante, y se le calculo el area de la siguiente manera.

![imagen012](Imagenes/imagen012.PNG "imagen012")
* se obtiene que los paraderos del sitp de la localidad de San Cristobal, tienen una area de influencia de 14455512,617306 metros cuadrados 

![imagen013](Imagenes/imagen013.PNG "imagen013")
* se procedio a calcular cuales manzanas se encontraban fuera de la cobertura del area de influencia.

![imagen014](Imagenes/imagen014.PNG "imagen014")
* y se muestran a continuacion en color rojo

![imagen014a](Imagenes/imagen014a.PNG "imagen014a")
* tambien se calculo cuales manzanas no se suplia totalmente la cobertura del area de influencia de 200 metros.

![imagen015](Imagenes/imagen015.PNG "imagen015")
* y se muestran a continuacion en color amarillo

![imagen015a](Imagenes/imagen015a.PNG "imagen015a")


#### Cargar capas a GEOSERVER

* se selecciona la pestaña "Database" y la opcion "DB Manager..." y se tiene la siguiente ventana, ahi nos aseguramos de conectarnos a la base de datos del curso

![imagen016](Imagenes/imagen016.PNG "imagen016")
* en la ventana de "DB Manager" se selecciona el boton "Import/Layer File..." y se importan las capas de la siguiente manera:
- capa da_paraderos_sitp_san_cristobal

![imagen017](Imagenes/imagen017.PNG "imagen017")
- capa da_manzanas_sin_cobertura_completa

![imagen018](Imagenes/imagen018.PNG "imagen018")
- capa da_manzanas_sin_cobertura

![imagen019](Imagenes/imagen019.PNG "imagen019")
- capa da_buffer_200_paraderos

![imagen020](Imagenes/imagen020.PNG "imagen020")
- capa da_manzanas_san_cristobal

![imagen021](Imagenes/imagen021.PNG "imagen021")
- capa da_localidad_san_cristobal

![imagen022](Imagenes/imagen022.PNG "imagen022")
* en la ruta del geoserver se da click en el boton "Capas" ubicado en Datos y se le da la opcion de agragar nuevo recurso.

![imagen023](Imagenes/imagen023.PNG "imagen023")

![imagen024](Imagenes/imagen024.PNG "imagen024")
* se selecciona la base de datos 

![imagen025](Imagenes/imagen025.PNG "imagen025")
* y se escoje la capa que se va a publicar y se le ajustan los datos de la siguiente manera

![imagen026](Imagenes/imagen026.PNG "imagen026")
* ese proceso se realiza con todas las capas que se requieren publicar
* se hace la verificacion de que las capas esten publicadas

![imagen027](Imagenes/imagen027.PNG "imagen027")


## 4. Capa simbología SLD

#### Crear Simbologia
* Para crear la simbologia en formato SLD se debe tener la capa desplegada en QGIS, y se le da click derecho y la opcion "Properties..."
* se ajusta la simbologia de la manera adecuada

![imagen028](Imagenes/imagen028.PNG "imagen028")
* se presiona el boton "Style" y se despliega una barra de opciones se debe seleccionar "Save Style..." 

![imagen029](Imagenes/imagen029.PNG "imagen029")
* para cargar el estilo al Geoserver, se da click en el boton estilos, y en el boton agregar un nuevo estilo
* se introducen los datos de las siguiente manera

![imagen030](Imagenes/imagen030.PNG "imagen030")
* se realizo para la capa "da_localidad_san_cristobal"
#### codigo 
~~~
  <NamedLayer>
    <se:Name>da_localidad_san_cristobal</se:Name>
    <UserStyle>
      <se:Name>da_localidad_san_cristobal</se:Name>
      <se:FeatureTypeStyle>
        <se:Rule>
          <se:Name>Localidad San Cristobal</se:Name>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#91522d</se:SvgParameter>
              <se:SvgParameter name="fill-opacity">0</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">3</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
        <se:Rule>
          <se:TextSymbolizer>
            <se:Label>
              <ogc:PropertyName>locnombre</ogc:PropertyName>
            </se:Label>
            <se:Font>
              <se:SvgParameter name="font-family">MS Shell Dlg 2</se:SvgParameter>
              <se:SvgParameter name="font-size">13</se:SvgParameter>
            </se:Font>
            <se:LabelPlacement>
              <se:PointPlacement>
                <se:AnchorPoint>
                  <se:AnchorPointX>0</se:AnchorPointX>
                  <se:AnchorPointY>0.5</se:AnchorPointY>
                </se:AnchorPoint>
              </se:PointPlacement>
            </se:LabelPlacement>
            <se:Fill>
              <se:SvgParameter name="fill">#000000</se:SvgParameter>
            </se:Fill>
            <se:VendorOption name="maxDisplacement">1</se:VendorOption>
          </se:TextSymbolizer>
        </se:Rule>
      </se:FeatureTypeStyle>
    </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
~~~
* previsualizacion de la leyenda

![imagen031](Imagenes/imagen031.PNG "imagen031")
* previsualizacion de la capa

![imagen031a](Imagenes/imagen031a.PNG "imagen031a")


* se realizo para la capa "da_paraderos_sitp_san_cristobal"
#### codigo
~~~
<?xml version="1.0" encoding="UTF-8"?>
<StyledLayerDescriptor xmlns="http://www.opengis.net/sld" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="1.1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.1.0/StyledLayerDescriptor.xsd" xmlns:ogc="http://www.opengis.net/ogc" xmlns:se="http://www.opengis.net/se">
  <NamedLayer>
    <se:Name>da_paraderos_sitp_san_cristobal</se:Name>
    <UserStyle>
      <se:Name>Paraderos SITP</se:Name>
      <se:FeatureTypeStyle>
        <se:Rule>
          <se:Name>Paraderos SITP</se:Name>
          <se:PointSymbolizer>
            <se:Graphic>
              <se:Mark>
                <se:WellKnownName>circle</se:WellKnownName>
                <se:Fill>
                  <se:SvgParameter name="fill">#000000</se:SvgParameter>
                </se:Fill>
                <se:Stroke>
                  <se:SvgParameter name="stroke">#232323</se:SvgParameter>
                  <se:SvgParameter name="stroke-width">0.5</se:SvgParameter>
                </se:Stroke>
              </se:Mark>
              <se:Size>4</se:Size>
            </se:Graphic>
          </se:PointSymbolizer>
        </se:Rule>
      </se:FeatureTypeStyle>
    </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
~~~
* previsualizacion de la leyenda

![imagen032](Imagenes/imagen032.PNG "imagen032")
* previsualizacion de la capa

![imagen032a](Imagenes/imagen032a.PNG "imagen032a")

* se realizo para la capa "da_buffer_200_paraderos"
#### codigo 
~~~
<?xml version="1.0" encoding="UTF-8"?>
<StyledLayerDescriptor xmlns="http://www.opengis.net/sld" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="1.1.0" xmlns:xlink="http://www.w3.org/1999/xlink" xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.1.0/StyledLayerDescriptor.xsd" xmlns:ogc="http://www.opengis.net/ogc" xmlns:se="http://www.opengis.net/se">
  <NamedLayer>
    <se:Name>da_buffer_200_paraderos</se:Name>
    <UserStyle>
      <se:Name>da_buffer_200_paraderos</se:Name>
      <se:FeatureTypeStyle>
        <se:Rule>
          <se:Name>Area de Influencia</se:Name>
          <se:PolygonSymbolizer>
            <se:Fill>
              <se:SvgParameter name="fill">#a47158</se:SvgParameter>
              <se:SvgParameter name="fill-opacity">0</se:SvgParameter>
            </se:Fill>
            <se:Stroke>
              <se:SvgParameter name="stroke">#232323</se:SvgParameter>
              <se:SvgParameter name="stroke-width">1</se:SvgParameter>
              <se:SvgParameter name="stroke-linejoin">bevel</se:SvgParameter>
              <se:SvgParameter name="stroke-dasharray">1 2</se:SvgParameter>
            </se:Stroke>
          </se:PolygonSymbolizer>
        </se:Rule>
      </se:FeatureTypeStyle>
    </UserStyle>
  </NamedLayer>
</StyledLayerDescriptor>
~~~
* previsualizacion de la leyenda

![imagen033](Imagenes/imagen033.PNG "imagen033")
* previsualizacion de la capa

![imagen033a](Imagenes/imagen033a.PNG "imagen033a")

## 5. Capa simbología CSS

* Para crear la simbologia en CSS debemos acceder a la pagina de geoserver y en la pestaña estilos agregar uno nuevo, se llenan los campos como acontinuacion y se escoje el formato "CSS" y en "Style Content" se selecciona polygon y generate para que genere el codigo
* se realizo para la capa "da_manzanas_san_cristobal"

![imagen034](Imagenes/imagen034.PNG "imagen034")
#### codigo
~~~
/* @title Manzanas San Cristobal */
* {
    stroke: #000000;
    stroke-width: 0.26;
    fill: null;
}

~~~
* previsualizacion de la leyenda

![imagen036](Imagenes/imagen036.PNG "imagen036")
* previsualizacion de la capa

![imagen036a](Imagenes/imagen036a.PNG "imagen036a")

## 6. Capa simbologia YSLD

#### crear Simbologia
* Para crear la simbologia en YSLD debemos acceder a la pagina de geoserver y en la pestaña estilos agregar uno nuevo, se llenan los campos como acontinuacion y se escoje el formato "YSLD" y en "Style Content" se selecciona polygon y generate para que genere el codigo
* Se realizo para la capa da_manzanas_sin_cobertura_completa

![imagen037](Imagenes/imagen037.PNG "imagen037")


#### codigo
~~~
title: Manzanas sin cobertura completa
name: Manzanas sin cobertura completa
symbolizers:
- polygon:
    stroke-width: 0.5
    stroke-color: '#000000'
    fill-color: '#ffff00'
    fill-opacity: 0.5
~~~
* previsualizacion de la leyenda

![imagen038](Imagenes/imagen038.PNG "imagen038")
* previsualizacion de la capa

![imagen038a](Imagenes/imagen038a.PNG "imagen038a")

* Se realizo para la capa da_manzanas_sin_cobertura

![imagen039](Imagenes/imagen039.PNG "imagen039")

#### codigo
~~~
title: Manzanas sin cobertura
name: Manzanas sin cobertura
symbolizers:
- polygon:
    stroke-width: 0.26
    stroke-color: '#000000'
    fill-color: '#ff1300'
    fill-opacity: 0.5
~~~

* previsualizacion de la leyenda

![imagen040](Imagenes/imagen040.PNG "imagen040")
* previsualizacion de la capa

![imagen040a](Imagenes/imagen040a.PNG "imagen040a")


## 7. grupo de capas 

#### Layer group
* Para crear el grupo de capas con el boton "Grupos de Capas" y se llenan los datos de la siguiente manera

![imagen041](Imagenes/imagen041.PNG "imagen041")
* se cargan las capas de la siguiente manera y se asigna la simbologia por defecto. 

![imagen042](Imagenes/imagen042.PNG "imagen042")

#### Previsualización

* A continuacion se muestra una previsualizacion 

![imagen043](Imagenes/imagen043.PNG "imagen043")

* y el link para acceder al mapa

http://34.83.176.208:18080/geoserver/clase_2020_01/wms?service=WMS&version=1.1.0&request=GetMap&layers=clase_2020_01%3Ada_zona_de_influencia_paraderos_sitp&bbox=996471.4130562533%2C990282.0057598756%2C1005432.3568950287%2C999399.4895897815&width=754&height=768&srs=EPSG%3A3116&format=application/openlayers

##### Publicacion en GITHUB pages desde QGIS

* Para generar los mapas se debe contar con el Plugin de "Qgis2web"
        ![imagen044](Imagenes/imagen044.PNG "imagen044")
* Posteriormente se despliega la pestaña "Web" , se escoge la opcion "qgis2web" y la herramienta "Create web map"
      ![imagen045](Imagenes/imagen045.PNG "imagen045")
* Se despliega una ventana donde se deben confgurar las propiedades del mapa web
      ![imagen046](Imagenes/imagen046.PNG "imagen046")
* Cuando ya se han ajustado todas las propiedades, se da click en el boton "Exportar", y debe salir una ventana con el proceso Exitoso
      ![imagen047](Imagenes/imagen043.PNG "imagen047")

* Url 
https://danielavendano.github.io/Clase1_Cartografia_Web/Tarea_2/Mapa/Mapa/index.html
    

## 8. Conclusiones

* Video Loom