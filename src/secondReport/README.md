# Informe 2: Ayudas

## Introducción

El segundo informe tiene como objetivo presentar información relevante sobre las ayudas, utilizando una consulta SQL previamente elaborada para cargar únicamente los datos necesarios. Este enfoque garantiza eficiencia en el manejo de datos y mejora el rendimiento del informe.

![Informe Ayudas](../assets/InformeAyudas.png)

## Creación de la Tabla Visual

Una vez cargada la consulta SQL, se crea una tabla visual que muestra todos los campos de la consulta. Esta tabla incluye información detallada sobre los solicitantes de ayuda y sus respectivas solicitudes. Para mejorar la legibilidad de la tabla, se realizan los siguientes pasos:

1. **Cambio de Nombres de Columnas**: 
   - Para cambiar los nombres de las columnas, se selecciona la tabla visual y se accede al panel de propiedades. En la sección "Formato", se encuentra la opción "Títulos de columnas", donde se puede editar cada título para que sea más descriptivo.

2. **Reemplazo de Valores en Campos**:
   - Para mejorar la legibilidad de ciertos campos, como `tipoexpediente`, se utiliza la opción "Reemplazar valores" en Power BI. Para ello, se siguen los siguientes pasos:
     - Se accede a la pestaña **Transformar datos**.
     - Se selecciona la columna correspondiente (por ejemplo, `tipoexpediente`).
     - Se hace clic derecho sobre la columna y se selecciona "Reemplazar valores".
     - En el cuadro de diálogo que aparece, se introduce el valor a reemplazar (por ejemplo, "CON") y el nuevo valor que se desea mostrar (por ejemplo, "Concesión").
     - Se repiten estos pasos para otros valores que necesiten ser reemplazados, asegurando así que la información sea más legible para los usuarios.

## Creación de Gráficos

Se incorporan dos gráficos para ofrecer una visualización más clara de los datos:

1. **Gráfico Circular**: 
   - Este gráfico representa la distribución del campo `tipoexpediente`. Para crear el gráfico, se selecciona la visualización de gráfico circular y se configura para que utilice la columna `tipoexpediente` (ya transformada) como el eje de categoría.

   ![Gráfico Circular](../assets/GraficoCircular.png)

2. **Gráfico de Barras**:
   - Se añade un gráfico de barras que muestra el campo `Estado`. Este gráfico proporciona una rápida visualización del estado de las solicitudes de ayuda.

   ![Gráfico de Barras](../assets/GraficoBarras.png)

## Filtros

Se implementan dos filtros para facilitar la segmentación de datos:

1. **Filtro por Provincia**: 
   - Este filtro permite a los usuarios seleccionar la provincia correspondiente a las ayudas. Se basa en el campo `provincia` de la consulta SQL.

2. **Filtro por Decreto**:
   - Similarmente, se añade un filtro para el campo `decreto`, que permite a los usuarios filtrar las ayudas según el decreto específico relacionado con la solicitud.

## Conclusión

El informe de ayudas proporciona una visión detallada y clara de las solicitudes y su estado. La utilización de una consulta SQL optimizada para cargar solo los datos necesarios y la implementación de gráficos y filtros mejora la interacción del usuario con la información presentada. Esta metodología no solo optimiza el rendimiento del informe, sino que también facilita la comprensión de los datos, permitiendo una toma de decisiones informada y eficiente.
