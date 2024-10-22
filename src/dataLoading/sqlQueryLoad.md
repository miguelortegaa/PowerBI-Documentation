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
```
Esta consulta selecciona solo los actos documentados y recibos que fueron pagados después del 1 de enero de 2022. El resultado será mucho más pequeño que cargar todas las tablas completas, lo que mejora la eficiencia y reduce el tiempo de carga.

### Ejemplo de uso

Este enfoque es útil si solo necesitas un subconjunto de datos para análisis específicos. Por ejemplo, si solo te interesa analizar los recibos de un período de tiempo determinado, una consulta SQL personalizada te permitirá filtrar los datos antes de cargarlos en Power BI.