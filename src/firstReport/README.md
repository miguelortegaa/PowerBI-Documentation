# Informe 1: Actos documentados y Recibos

## Objetivo del informe

Este informe tiene como objetivo mostrar los *actos documentados* y sus recibos asociados, permitiendo el filtrado por mes, año, y estado de vigencia del acto documentado.

![Informe Actos documentados y Recibos](../assets/InformeActosdocumentados.png)

## Elementos del informe

- **Tabla de Actos Documentados**: Muestra los actos registrados en la base de datos. Al seleccionar un acto, se filtran automáticamente los recibos relacionados.
- **Tabla de Recibos**: Muestra los pagos asociados a los actos documentados seleccionados.
- **Filtros de Recibos**:
  - Filtro por *Año*.
  - Filtro por *Mes*.
  - Filtro por *Último acto*.

## Configuración de los filtros

- **Filtro de año y mes**: Se han implementado *slicers* para permitir el filtrado dinámico de los recibos, de modo que los usuarios puedan ver tanto los recibos pagados en una fecha específica como los acumulados hasta esa fecha.
- **Filtro de Último Acto**: Este filtro permite al usuario visualizar únicamente los actos documentados que son el último acto registrado o aquellos que ya no lo son.
![Filtros Actos documentados y Recibos](../assets/FiltrosActosdocumentadosYRecibos.png)

## Carga de datos

Para cargar los datos, se estableció una conexión directa con la base de datos PostgreSQL. En esta ocasión, se optó por la opción de 'Importar datos' en Power BI para cargar todas las tablas. Este enfoque se eligió porque, al proponer el informe, se planteó como un proyecto que sería actualizado de forma continua, con mejoras progresivas y la incorporación de nuevos datos y métricas a mostrar.