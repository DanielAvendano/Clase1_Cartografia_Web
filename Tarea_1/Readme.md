
##  1. Cuál es el problema a tratar?

 El problema a tratar es calcular cual localidad cuenta con mas canchas sinteticas, y la cercania de ciclorutas a estas canchas

## 2. Por qué los datos geográficos ayudan a resolverlo?

Los datos geográficos ayudan a resolverlo, ya que brindan el componente espacial lo cual nos permite vincular varias capas y asi poder obtener una solución a nuestro problema
   
## 3. Descripción de la solución propuesta.

La solucion propuesta es:

* Cargar las capas de localidades, canchas sinteticas, y ciclorutas.

* Realizar un filtro para determinar cual es la localidad con mas canchas sinteticas.

* Crear un buffer de 100 metros a las canchas de esa localidad.

* Hacer un Intersect para determinar si existen ciclorutas a menos de 100 mentros de las canchas.
    
## 4. Listado detallado de las fuentes de datos seleccionadas.

* Capa de Localidades: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

* Capa de ciclorutas: https://www.ideca.gov.co/recursos/mapas/mapa-de-referencia-para-bogota-dc

* Capa de Canchas Sinteticas: http://datosabiertos.bogota.gov.co/dataset/canchas-sinteticas

## 5. Descripción detallada del procesamiento no trivial realizado a los datos 
    
## 6. Descripción detallada de la metodología utilizada para generar los mapas 
    
## 7. Descripción detallada del procedimiento técnico utilizado para generar los mapas.

## 8. Adicionar al repositorio github los archivos generados

## 9. Urls de los mapas publicados en la web
    
## 10. Conclusiones Ventajas / desventajas / dificultades encontradas durante el desarrollo del ejercicio
