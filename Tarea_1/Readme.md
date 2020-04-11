
##  1. Cuál es el problema a tratar?

 El problema a tratar es, calcular cual localidad cuenta con mas parques que tengan canchas sinteticas, y la cercania de ciclorutas a estos parques

## 2. Por qué los datos geográficos ayudan a resolverlo?

Los datos geográficos ayudan a resolverlo, ya que brindan el componente espacial lo cual nos permite vincular varias capas y asi poder obtener una solución a nuestro problema
   
## 3. Descripción de la solución propuesta.

La solucion propuesta es:

* Cargar las capas de localidades, canchas, y ciclorutas.

* Realizar un Intersect para poder determinar que una cancha esta solo en una localidad la cual se llamara "Int_Loc_Canchas".

* Crear un buffer de 100 metros a las canchas de esa localidad, el cual se llamara "Buff_100_Parques".

* Hacer un Intersect entre el buffer de las canchas (Buff_100_Parques) y la capa de ciclorutas, para determinar si existen ciclorutas a menos de 100 mentros de las canchas, esta capa se llamara "Int_Ciclo_Parques".
    
## 4. Listado detallado de las fuentes de datos seleccionadas.

* Capa de Localidades
    - Base de datos: GDR_V12.19.gdb
    - Dataset: Entidad_Territorial
    - Feature Class: Loca
    - Atributos que se tuvieron en cuenta: Nombre Localidad
    - Link de descarga: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

* Capa de ciclorutas 
    - Base de datos: GDR_V12.19.gdb
    - Dataset: Transporte_Terrestre
    - Feature Class: RBic
    - Atributos que se tuvieron en cuenta:
    - Link de descarga: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

* Capa de Canchas Sinteticas 
    - Atributos que se tuvieron en cuenta:
    - Link de descarga: http://datosabiertos.bogota.gov.co/dataset/canchas-sinteticas

## 5. Descripción detallada del procesamiento realizado a los datos 
    
## 6. Descripción detallada de la metodología utilizada para generar los mapas 
    
## 7. Descripción detallada del procedimiento técnico utilizado para generar los mapas.

## 8. Adicionar al repositorio github los archivos generados

## 9. Urls de los mapas publicados en la web
    
## 10. Conclusiones Ventajas / desventajas / dificultades encontradas durante el desarrollo del ejercicio
