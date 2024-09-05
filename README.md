## Documentación Práctica 1 MyS1
### Variables:
Las variables declaradas para implementar en el modelo son:
- **CompraBomba1 - CompraBomba6**: Monitorean las compras realizadas en cada bomba de gasolina.
- **TotalBomba1 - TotalBomba6**: Registra el total de ventas realizadas en cada estación.
- **TotalBombas**: Acumula el total de ventas de todas las bombas combinadas.
- **TiempoB1 - TiempoB6**: Mide el tiempo de operación de cada bomba.
- **Contador1**: Cuenta el número total de vehículos atendidos.

### Procesos
- **BombaN3 - BombaN6**: Son los procesos que se utilizan en las bombas de Autoservicio.<br>
* En la primera asignación se usa la función Random.Discrete
```
Random.Discrete( TablaAbastecimiento.Diesel, 0.25, TablaAbastecimiento.Regular , 0.61, TablaAbastecimiento.Super, 1)
```
Dicha función asigna un valor aleatorio basado en las probabilidades de uso de los tipos de combustible.
* En la segunda asignación se acumula el valor de "CompraBomba" en la variable "TotalBomba", lo cual representa el total acumulado de combustible
  vendido.
