# 🔍Definición y creación de los filtros

Para mejorar la interactividad y la personalización del informe, se han implementado tres filtros fundamentales en Power BI: **Año**, **Mes** y **Último Acto**. A continuación, se detalla cómo crear y configurar cada uno de estos filtros utilizando los campos correspondientes de los datos.

![Filtros](../assets/FiltrosActosdocumentadosYRecibos.png)

## 1. Filtro por Año

El primer filtro permite seleccionar el año para filtrar la información mostrada en el informe. Para crear este filtro, sigue estos pasos:

1. En el panel **Visualizaciones**, selecciona el icono de **Segmentación de datos** (Slicer).
2. Arrastra el campo **Año** desde la tabla **reciboinformacion** hacia el área de visualización del Slicer.
3. Ajusta el diseño del Slicer según tus preferencias, ya sea como lista desplegable o como una serie de botones.

Este filtro se basará en el campo **Año** que forma parte de la columna **fecha** de la tabla **reciboinformacion**, permitiendo a los usuarios seleccionar el año específico para visualizar los datos correspondientes.

## 2. Filtro por Mes

El segundo filtro permite a los usuarios seleccionar el mes en el que desean enfocarse. Para configurarlo, sigue estos pasos:

1. Al igual que antes, selecciona un nuevo **Segmentador de datos** en el panel **Visualizaciones**.
2. Arrastra el campo **Mes** desde la tabla **reciboinformacion** hacia el área del nuevo Slicer.
3. Personaliza la apariencia del Slicer según sea necesario.

Este filtro se basa en el campo **Mes** de la columna **fecha** de la tabla **reciboinformacion**, y permite a los usuarios seleccionar un mes específico para filtrar los datos del informe.

## 3. Filtro por Último Acto

El tercer filtro está diseñado para permitir a los usuarios filtrar los resultados en función del estado de vigencia de los actos documentados. Para crear este filtro, sigue estos pasos:

1. Selecciona otro **Segmentador de datos** desde el panel **Visualizaciones**.
2. Arrastra el campo **Vigente**, previamente creado con la siguiente consulta DAX en la tabla **actodocumentado**:

   ```dax
   Vigente = IF('safir actodocumentado'[baja] = TRUE(), "No", "Sí")
   ```
3. Personaliza el Slicer para que los usuarios puedan seleccionar entre "Sí" y "No", indicando si los actos documentados están vigentes o no.

Este filtro proporcionará una forma efectiva de filtrar los datos mostrados en el informe según el estado de vigencia de los actos documentados.

## Interactividad entre Recibos y Actos Documentados

Además, gracias a la interactividad de Power BI, si un usuario selecciona un recibo, podrá ver los actos documentados vinculados a la cuenta de ese recibo. Del mismo modo, al seleccionar un acto documentado, se podrá acceder a la información de los recibos asociados a la cuenta de dicho acto documentado. Esta funcionalidad enriquece aún más la experiencia del usuario, permitiendo un análisis más profundo de la relación entre recibos y actos documentados.

## Conclusión

Con la implementación de estos filtros, los usuarios podrán interactuar de manera más efectiva con el informe, permitiendo una visualización más clara y específica de los datos según sus necesidades. La capacidad de filtrar por **Año**, **Mes** y **Último Acto** proporcionará una herramienta valiosa para el análisis de información, facilitando una toma de decisiones más informada.