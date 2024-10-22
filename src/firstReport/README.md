# Informe 1: Actos documentados y Recibos

## Objetivo del informe

Este informe tiene como objetivo mostrar los *actos documentados* y sus recibos asociados, permitiendo el filtrado por mes, año, y estado de vigencia del acto documentado.

## Elementos del informe

- **Tabla de Actos Documentados**: Muestra los actos registrados en la base de datos. Al seleccionar un acto, se filtran automáticamente los recibos relacionados.
- **Tabla de Recibos**: Muestra los pagos asociados a los actos documentados seleccionados.
- **Filtros de Recibos**:
  - Filtro por *Año*.
  - Filtro por *Mes*.
  - Filtro por estado de vigencia del acto documentado (*Vigente* o *No vigente*).

## Configuración de los filtros

- **Filtro de año y mes**: Se han implementado slicers para permitir el filtrado dinámico de los recibos, de modo que los usuarios puedan ver tanto los recibos pagados en una fecha específica como los acumulados hasta esa fecha.
- **Filtro de Vigencia**: Este filtro permite al usuario visualizar únicamente los actos documentados vigentes o no vigentes.

## Carga de datos

Para cargar los datos, se realizó una conexión directa a la base de datos PostgreSQL. En este caso, se utilizó la opción de "Importar datos" en Power BI para cargar todas las tablas necesarias.