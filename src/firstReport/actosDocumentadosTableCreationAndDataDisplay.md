# 📜Creación de las tablas y datos a mostrar

## Preparación de los datos

El primer paso es identificar las tablas implicadas en los datos que queremos mostrar en el informe y asegurarnos de que las relaciones entre estas tablas están correctamente definidas. A continuación, se muestra un ejemplo de las relaciones entre las tablas involucradas en la visualización de los datos de la tabla **Actos documentados**:

![Ejemplo de las relaciones entre tablas](../assets/MuestraDeRelaciones.png)

Para mostrar los datos requeridos en el informe, en ocasiones es necesario combinar campos de diferentes tablas. Un ejemplo de esto es el campo **Cuenta**, que se construye uniendo el campo *código* de la tabla **grupoconstruccion** y el campo *identificador* de la tabla **inmueblehistorico**. Una solución para mostrar el campo **Cuenta** correctamente consiste en crear una nueva columna en la tabla **actodocumentado**. Para ello, debes hacer clic en la parte derecha, donde dice **Datos**, seleccionar la tabla en la que deseas crear la columna y luego, en la parte superior, hacer clic en **Nueva Columna**. Posteriormente, introduce la siguiente consulta DAX en el campo de texto que se abrirá:


```dax
Cuenta = 
CALCULATE(
    FIRSTNONBLANK('safir grupoconstruccion'[codigo], 1)
) & ".VIV." & RELATED('safir inmueblehistorico'[identificador])
```
Esta consulta genera el valor del campo **Cuenta** concatenando el código del grupo de construcción y el identificador del inmueble, permitiendo así que ambos se visualicen de manera adecuada en el informe.

Además, se han creado columnas adicionales en las tablas **direccion** y **tercero**. En la tabla **direccion**, se ha añadido la columna **DireccionCompleta** para presentarla en un formato más legible para los usuarios que visualizan el informe. En la tabla **tercero**, se ha creado la columna **NombreCompleto** por la misma razón que **DireccionCompleta**.

A continuación, se presentan las consultas DAX correspondientes a cada una de estas nuevas columnas:

### Consulta DAX para la columna **NombreCompleto**
```dax
Nombre Completo = 
TRIM('safir tercero'[nombre] & " " & 'safir tercero'[apellido1] & " " & 'safir tercero'[apellido2])
```
Esta consulta concatena el nombre y los apellidos del tercero, eliminando cualquier espacio en blanco innecesario al principio y al final del resultado. Esto proporciona un formato más claro y legible del nombre completo del usuario en el informe.

### Consulta DAX para la columna **DireccionCompleta**
```dax
DireccionCompleta = 
RELATED('safir tipovia'[descripcion]) & " " & 
RELATED('safir via'[descripcion]) & " " & 
'safir direccion'[numero] & 
IF(NOT ISBLANK('safir direccion'[planta]), " " & 'safir direccion'[planta], "") & 
IF(NOT ISBLANK('safir direccion'[puerta]), " " & 'safir direccion'[puerta], "")
```
Esta consulta combina la descripción del tipo de vía, la descripción de la vía, el número de la dirección y, opcionalmente, la planta y la puerta, si están disponibles. Esto asegura que la dirección se presente de manera completa y comprensible, facilitando la identificación de la ubicación correspondiente en el informe.

## Generación de la Tabla

Una vez que los datos estén preparados, podemos proceder a generar la tabla y vincularle la información correspondiente. Para ello, sigue estos pasos:

1. En la parte derecha de la interfaz de Power BI, abre la pestaña **Visualizaciones**.
2. Selecciona el ícono de **Tabla** para crear una nueva visualización.
3. Añade los campos que deseas mostrar en la tabla. Esto se puede hacer de dos maneras:
   - Arrastrando el campo desde la pestaña **Datos** hacia la sección **Columnas** de la pestaña **Visualizaciones**.
   - Haciendo clic en el icono de verificación (checker) junto al campo que quieres añadir.


```admonish info
Puedes cambiar el nombre de los campos haciendo doble clic en la cabecera de la columna dentro de la pestaña **Visualizaciones** que deseas modificar.
```

## Tabla generada

Ahora que hemos creado y configurado la tabla con los datos necesarios, estamos listos para explorar y analizar la información presentada en el informe. Con los campos *Cuenta*, *NombreCompleto*, y *DireccionCompleta* bien definidos, puedes aplicar filtros, segmentaciones y crear visualizaciones adicionales que faciliten la interpretación de los datos. Esto te permitirá obtener insights valiosos sobre los **Actos documentados**.