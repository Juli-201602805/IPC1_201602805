## Documentación Práctica 1 MyS1 - *Grupo No. 14*
### Integrantes:
* Walter Manolo Martinez Mateo    - 201213212
* Luis Alfredo Vejo Mendoza       - 201212527
* Gabriel Orlando Ajsivinac Xicay - 201213010
* María Julissa García Morán      - 201602805
* Diego Abraham Robles Meza       - 201901429

# **MODELO 1**
El *Modelo 1* nos muestra un sistema de 6 estaciones de combustible, 2 de Servicio Completo representadas con el nombre de *BombaSC* y 4 de AutoServicio con el nombre<b>
*Bomba* numeradas de la 3 a la 6, cada una de las bombas distribuye tres tipos de combustible: Diesel, Regular y Super. La distribución de clientes se basa en estudios que indican que el 25% de los vehículos utilizan Diesel, el 48% utilizan Regular, y el 52% Super. Los vehículos pasan por una serie de nodos, cada uno asignado a un función específica, como carga de combustible o mantenimiento. Se inicia con las estaciones de combustible, luego aparecen otras estaciones como *Lavado*, *Secado*, *Inspección*, *Encerado* y *Ventanillas de pago*, las cuales proporcionan servicios adicionales a los usuarios. Cuando un cliente llega a la estación, tiene un 75% de probabilidad de comprar combustible y un 25% de utilizar el servicio de limpieza. De los que abastecen combustible, un 40% pasa también al servicio de limpieza, mientras que el 33% de los que inician con limpieza luego compran combustible.<b>
El modelo también incluye métricas relacionadas con las bombas, como costos e ingresos generados. Estas métricas son esenciales para evaluar la eficiencia del sistema.
* **Llegada de vehículos:** La llegada de vehículos está distribuida exponencialmente con una media de 10 minutos, la *distribución* utilizada es:
```
Random.Exponential(10)
```
Genera un valor aleatoriamente a partir de una *distribución exponencial* con una media de 10 minutos. Es utilizada comúnmente para modelar el tiempo entre eventos en un proceso de Poisson, en este caso la llegada de vehículos a una estación de servicio, ya que los eventos ocurren de manera aleatoria e independiente unos de otros.
* **Estación de Lavado:** Para el lavado de vehículos la *distribución* utilizada es:
```
Random.Normal( 8, 1.5)
```
Esta *distribución* es utilizada para modelar tiempos de operación, se utilizó en el lavado de autos ya que el tiempo de operación puede variar debido a factores como el tamaño del vehículo, la suciedad del mismo, entre otros. El valor 8 significa el tiempo promedio que toma lavar un auto y el valor 1.5 significa la desviación estándar, indicando que el proceso de lavado puede variar manteniendo un rango de 6.5 a 9.5 minutos.
* **Estación de Secado:** Para la operación de secado de vehículo se utiliza la *distribución*:
```
Random.Triangular( 3 , 4 , 6 )
```
Se utiliza esta *distribución* ya que conocemos el valor mínimo = 3 minutos, el valor más probable = 4 minutos y el valor máximo = 6 minutos. Ya que el sistema casi siempre completa el secado en 4 minutos, pero con la posibilidad de que en algunas ocasiones el tiempo sea menos como 3 minutos o más como 6 minutos.
* **Estación de Inspección:** Para la operación de inspección de vehículo se utiliza la *distribución*:
```
Random.Discrete( 3, 0.35, 4, 0.60,6,1 )
```
Esta distribución modela el tiempo que tarda el proceso de secado con los siguientes parámetros: *3 minutos con una probabilidad de 35%* , *4 minutos con una probabilidad de 25%.* y *6 minutos con una probabilidad de 40%*. Esta distribución se seleccionó para modelar el tiempo de la inspección del vehículo, porque refleja de manera precisa la variabilidad observada en el sistema. Dependiendo de las condiciones del vehículo y las expectativas del cliente, la inspección puede durar 3, 4 o 6 minutos, con una mayor probabilidad de que tome 6 minutos.
* **Estación de Encerado:** Para la operación de encerado de vehículo se utiliza la *distribución*:
```
Random.Uniform( 5 , 9 )
```
La distribución uniforme es adecuada para este tipo de operación porque no hay un valor más probable dentro del rango. Esto implica que el tiempo del proceso de encerado puede ser de cualquier duración entre los 5 y 9 minutos, sin que ninguno de esos tiempos sea más común que otro.
* **Estación de Pago:** Para la estación de pago, en cada ventanilla se utiliza la *distribución*:
```
Random.Poisson(6)
```
Esta distribución es comúnmente utilizada para modelar el número de eventos que ocurren en un intervalo de tiempo fijo. En este caso se utiliza para modelar el tiempo que tarda un empleado en procesar el pago de un cliente. Con una media de 6 minutos, se estima que, en promedio, cada cliente toma 6 minutos en ser atendido, lo que incluye entregar la ficha, realizar el pago y recibir el ticket de salida.

## Variables:
Las variables declaradas para implementar en el modelo son:
- **CompraBomba1 - CompraBomba6**: Monitorean las compras realizadas en cada bomba de gasolina.
- **TotalBomba1 - TotalBomba6**: Registra el total de ventas realizadas en cada estación.
- **TotalBombas**: Acumula el total de ventas de todas las bombas combinadas.
- **TiempoB1 - TiempoB6**: Mide el tiempo de operación de cada bomba.
- **Contador1**: Cuenta el número total de vehículos atendidos.

## Procesos
### *BombaN3 - BombaN6: Son los procesos que se utilizan en las bombas de Autoservicio.*
**Flujo del proceso**:
* En la primera asignación se usa la distribución *Random.Discrete*
```
Random.Discrete( TablaAbastecimiento.Diesel, 0.25, TablaAbastecimiento.Regular , 0.61, TablaAbastecimiento.Super, 1)
```
Dicha distribución asigna un valor aleatorio basado en las probabilidades de uso de los tipos de combustible, lo que significa que hay una probabilidad del 25% que se seleccione el valor asociado a *TablaAbastecimiento.Diesel*, una probabilidad de que el 61% seleccione el valor asociado a *TablaAbastecimiento.Regular* y el restante que es del 14% seleccione el valor asociado a *TablaAbastecimiento.Super*. La suma de las probabilidades debe ser igual a 1, ya que esto nos garantiza que siempre se seleccionará uno de los valores posibles.
* En la segunda asignación se acumula el valor de "CompraBomba" en la variable "TotalBomba", lo cual representa el total acumulado de combustible
  vendido.

### *BombaSerCom1 - BombaSerCom2: Son los procesos que se utilizan en las bombas de Servicio Completo.*
**Flujo del proceso**:
* En la primera asignación se usa la distribución *Random.Discrete*
```
Random.Discrete( TablaAbastecimiento.Diesel, 0.25, TablaAbastecimiento.Regular , 0.61, TablaAbastecimiento.Super, 1)
```
Dicha distribución asigna un valor aleatorio basado en las probabilidades de uso de los tipos de combustible, lo que significa que hay una probabilidad del 25% que se seleccione el valor asociado a *TablaAbastecimiento.Diesel*, una probabilidad de que el 61% seleccione el valor asociado a *TablaAbastecimiento.Regular* y el restante que es del 14% seleccione el valor asociado a *TablaAbastecimiento.Super*. La suma de las probabilidades debe ser igual a 1, ya que esto nos garantiza que siempre se seleccionará uno de los valores posibles.
* En la segunda asignación se acumula el valor de "CompraBomba" en la variable "TotalBomba", lo cual representa el total acumulado de combustible
  vendido.

### *TiempoBom1 - TiempoBom6: Son los procesos que se utilizan para el tiempo de servicio de cada bomba.*
**Flujo del proceso**:
* En SetRow se selecciona una fila aleatoria de la "Tabla Abastecimiento" de acuerdo a la columna de probabilidad
```
TablaAbastecimiento.Probabilidad.RandomRow
```
Esto permite que cada fila tiene una probabilidad diferente de ser seleccionada haciendo la simulación más realista.
* Se hace una asignación a la variable "TiempoB" que almacena el tiempo que tomará el servicio de abastecimiento para esa bomba,<b>
  basándose en la fila seleccionada aleatoriamente. Esto permitirá la simulación de múltiples escenarios.
