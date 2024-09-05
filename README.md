## Documentación Práctica 1 MyS1
## Variables:
Las variables declaradas para implementar en el modelo son:
- **CompraBomba1 - CompraBomba6**: Monitorean las compras realizadas en cada bomba de gasolina.
- **TotalBomba1 - TotalBomba6**: Registra el total de ventas realizadas en cada estación.
- **TotalBombas**: Acumula el total de ventas de todas las bombas combinadas.
- **TiempoB1 - TiempoB6**: Mide el tiempo de operación de cada bomba.
- **Contador1**: Cuenta el número total de vehículos atendidos.

## Procesos
### <span style="color:green"> **BombaN3 - BombaN6**: Son los procesos que se utilizan en las bombas de Autoservicio.</span>
**Flujo del proceso**:
* En la primera asignación se usa la función Random.Discrete
```
Random.Discrete( TablaAbastecimiento.Diesel, 0.25, TablaAbastecimiento.Regular , 0.61, TablaAbastecimiento.Super, 1)
```
Dicha función asigna un valor aleatorio basado en las probabilidades de uso de los tipos de combustible.
* En la segunda asignación se acumula el valor de "CompraBomba" en la variable "TotalBomba", lo cual representa el total acumulado de combustible
  vendido.

- **BombaSerCom1 - BombaSerCom2**: Son los procesos que se utilizan en las bombas de Servicio Completo.
**Flujo del proceso**:
* En la primera asignación se usa la función Random.Discrete
```
Random.Discrete( TablaAbastecimiento.Diesel, 0.25, TablaAbastecimiento.Regular , 0.61, TablaAbastecimiento.Super, 1)
```
Dicha función asigna un valor aleatorio basado en las probabilidades de uso de los tipos de combustible.
* En la segunda asignación se acumula el valor de "CompraBomba" en la variable "TotalBomba", lo cual representa el total acumulado de combustible
  vendido.

- **TiempoBom1 - TiempoBom6**: Son los procesos que se utilizan para el tiempo de servicio de cada bomba.
**Flujo del proceso**:
* En SetRow se selecciona una fila aleatoria de la "Tabla Abastecimiento" de acuerdo a la columna de probabilidad
```
TablaAbastecimiento.Probabilidad.RandomRow
```
Esto permite que cada fila tiene una probabilidad diferente de ser seleccionada haciendo la simulación más realista.
* Se hace una asignación a la variable "TiempoB" que almacena el tiempo que tomará el servicio de abastecimiento para esa bomba,<b>
  basándose en la fila seleccionada aleatoriamente. Esto permitirá la simulación de múltiples escenarios.
