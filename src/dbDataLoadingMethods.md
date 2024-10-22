# Carga de Datos desde la Base de Datos

En Power BI, la carga de datos desde una base de datos PostgreSQL puede realizarse de diversas maneras, dependiendo de los requisitos del proyecto y el volumen de datos que se necesita manipular. En este documento, vamos a explorar dos métodos comunes para cargar datos desde PostgreSQL en Power BI:

- Carga de la base de datos completa.
- Carga del resultado de una consulta SQL personalizada.

## 1. Carga Completa de la Base de Datos

### Descripción

Este método consiste en conectar Power BI directamente a toda la base de datos, lo que implica cargar todas las tablas disponibles en la misma. Este enfoque es adecuado cuando se requiere trabajar con una amplia variedad de datos o no se tiene un conocimiento específico de las consultas que se van a necesitar.

### Ventajas
- **Facilidad de configuración**: Al conectar toda la base de datos, no es necesario crear consultas SQL personalizadas.
- **Acceso completo**: Se tiene acceso a todas las tablas y columnas de la base de datos, lo que permite flexibilidad en los análisis.
- **Ideal para exploración**: Este método es útil si se requiere explorar los datos en Power BI antes de definir consultas más específicas.

### Desventajas
- **Mayor tiempo de carga**: Si la base de datos es grande, el tiempo de carga inicial puede ser considerable.
- **Uso elevado de recursos**: Power BI tendrá que manejar grandes volúmenes de datos, lo que puede afectar el rendimiento.
- **Datos innecesarios**: Se cargan muchas tablas y campos que quizás no se utilicen en el informe final.

### Pasos para la carga completa

1. **Conexión a PostgreSQL**:
   - En Power BI, ve a la pestaña "Inicio" y selecciona "Obtener datos" > "PostgreSQL".
   - Introduce los detalles de la conexión (servidor, base de datos, usuario y contraseña).
   
2. **Seleccionar tablas**:
   - Power BI te mostrará todas las tablas disponibles en la base de datos.
   - Selecciona las tablas que deseas cargar. Si necesitas cargar todas, simplemente selecciona todas las tablas disponibles.

3. **Cargar datos**:
   - Selecciona la opción "Cargar" para traer los datos a Power BI. Power BI comenzará a cargar toda la información seleccionada.

4. **Modelado de datos**:
   - Una vez que los datos se hayan cargado, puedes ir a la pestaña "Modelo" para crear relaciones entre las tablas si no se han detectado automáticamente.

### Ejemplo de uso

Este método es útil cuando tienes un informe que necesita acceder a varias tablas relacionadas, como un informe de ventas que involucra datos de clientes, productos y facturación. La carga completa te permitirá explorar todos estos datos sin preocuparte por definir consultas específicas.

---

## 2. Carga de Datos Mediante Consulta SQL Personalizada

### Descripción

En este escenario, se carga el resultado de una consulta SQL específica en lugar de la base de datos completa. Este enfoque es ideal cuando solo necesitas trabajar con una parte de los datos o cuando el conjunto de datos es muy grande y es necesario filtrar información antes de cargarla en Power BI.

### Ventajas
- **Mejor rendimiento**: Solo se cargan los datos que necesitas, lo que reduce el tiempo de carga y mejora el rendimiento de Power BI.
- **Filtrado de datos**: Puedes aplicar filtros, unir tablas o seleccionar columnas específicas directamente en la consulta SQL.
- **Más control**: Este método ofrece un mayor control sobre los datos que se están cargando, permitiendo optimizar tanto el tamaño de los datos como la eficiencia del informe.

### Desventajas
- **Conocimiento de SQL**: Se requiere experiencia en SQL para escribir consultas eficientes y obtener los resultados deseados.
- **Falta de flexibilidad**: Si necesitas cambiar el conjunto de datos después de cargarlo, tendrías que modificar la consulta SQL y recargar los datos en Power BI.

### Pasos para la carga mediante consulta SQL

1. **Conexión a PostgreSQL**:
   - En Power BI, selecciona "Obtener datos" > "PostgreSQL".
   - Introduce los detalles de la conexión como en el caso anterior.

2. **Escribir la consulta SQL**:
   - En la ventana de selección de tablas, en la parte superior, selecciona la opción **"Consulta SQL nativa"**.
   - Power BI abrirá un editor donde podrás escribir tu consulta SQL. Asegúrate de que la consulta extraiga solo los datos que necesitas para tu informe.

3. **Ejecutar la consulta**:
   - Una vez que la consulta esté escrita, presiona "Aceptar". Power BI ejecutará la consulta en la base de datos y cargará los resultados.

4. **Cargar datos**:
   - Selecciona "Cargar" para traer los datos filtrados a Power BI.

### Ejemplo de consulta SQL

```sql
SELECT actodocumentado.id, actodocumentado.nombre, recibo.importe, recibo.fecha_pago
FROM actodocumentado
JOIN actodocumentadorecibo ON actodocumentado.id = actodocumentadorecibo.ad_id
JOIN recibo ON actodocumentadorecibo.recibo_id = recibo.id
WHERE recibo.fecha_pago >= '2022-01-01'
