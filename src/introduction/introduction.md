# 📖Introducción

Este proyecto se ha desarrollado con el objetivo de crear un sistema de análisis interactivo utilizando Power BI para visualizar y gestionar datos provenientes de una base de datos PostgreSQL. Los informes creados proporcionan a los usuarios una visión clara y detallada de los *actos documentados* y los *recibos*, así como de las *ayudas* otorgadas, permitiendo una mejor toma de decisiones a partir de la información presentada.

## Objetivos

El proyecto tiene varios objetivos clave:

1. **Conectar Power BI a una base de datos PostgreSQL**: Establecer una conexión fluida entre Power BI y la base de datos, permitiendo la carga y manipulación de grandes volúmenes de datos de forma eficiente.
   
2. **Crear informes interactivos**: Generar informes que presenten datos relevantes de manera dinámica, permitiendo la interacción del usuario a través de filtros y segmentaciones.

3. **Facilitar el análisis de datos**: Proporcionar a los usuarios una herramienta que les permita visualizar y analizar fácilmente la información sobre actos documentados, recibos, y ayudas.

## Estructura del proyecto

El proyecto consta de dos informes principales:

- **Informe de Actos Documentados y Recibos**: Este informe muestra la relación entre actos documentados y los recibos asociados. Se pueden aplicar filtros por fecha de recibo y estado de vigencia del acto documentado.

- **Informe de Ayudas**: Presenta un análisis visual de las ayudas otorgadas, permitiendo filtrar por Decreto y Provincia. Incluye gráficos que ayudan a interpretar los datos de manera más intuitiva.

## Herramientas utilizadas

Para la realización de este proyecto, se han utilizado las siguientes herramientas y tecnologías:

- **Power BI Desktop**: Para el desarrollo de los informes interactivos.
- **PostgreSQL**: Como base de datos relacional para almacenar y gestionar los datos.
- **Consulta SQL**: Para optimizar la carga de datos en ciertos informes y filtrar la información de manera eficiente.

## Flujo de trabajo

1. **Conexión a la base de datos**: Se estableció una conexión directa a la base de datos PostgreSQL.
2. **Carga de datos**: En algunos informes se optó por una carga completa de las tablas, mientras que en otros se utilizó una consulta SQL personalizada para optimizar el rendimiento.
3. **Diseño de los informes**: Se diseñaron los informes en Power BI, incluyendo tablas y gráficos, así como la implementación de filtros y slicers para una interacción dinámica.