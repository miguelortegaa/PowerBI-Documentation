
# 🧮Introducción a DAX en Power BI

## ¿Qué es DAX?

DAX, acrónimo de *Data Analysis Expressions*, es un lenguaje de fórmulas utilizado en Power BI, Power Pivot y Analysis Services de Microsoft para realizar cálculos avanzados y manipulación de datos. Aunque tiene cierta similitud con las fórmulas de Excel, DAX está optimizado para trabajar con grandes cantidades de datos y crear relaciones complejas entre tablas.

Este lenguaje permite construir tanto **columnas calculadas** como **medidas**, lo que proporciona un alto grado de flexibilidad en la modelización de datos.

## Potencial de DAX

DAX es una herramienta extremadamente poderosa que te permite:

- Realizar cálculos complejos que involucran múltiples tablas.
- Aplicar lógica condicional avanzada.
- Crear medidas dinámicas que cambian según los filtros aplicados en los informes.
- Optimizar y mejorar la presentación de datos en Power BI.

DAX te permite, por ejemplo, crear una **medida** que sume los valores de ventas hasta una fecha específica, o calcular un porcentaje acumulado según un contexto de filtro de fechas.

### Ejemplo básico de DAX

Un ejemplo básico es el cálculo de una suma simple de ventas. En Power BI, una medida usando DAX para sumar una columna de ventas sería algo así:

```dax
TotalSales = SUM(Sales[SalesAmount])
```

Este ejemplo calcula el total de las ventas sumando los valores de la columna `SalesAmount` de la tabla `Sales`.

Otro ejemplo, un poco más avanzado, sería usar una función condicional para calcular una medida que devuelva el total de ventas si el importe supera un umbral determinado:

```dax
HighSales = IF(SUM(Sales[SalesAmount]) > 5000, SUM(Sales[SalesAmount]), 0)
```

Este DAX devuelve el total de ventas solo si supera los 5,000; en caso contrario, devuelve 0.

## Funciones más comunes de DAX

Algunas de las funciones más comunes que verás en DAX incluyen:

- **SUM()**: Suma los valores de una columna.
- **AVERAGE()**: Calcula el promedio de los valores de una columna.
- **CALCULATE()**: Modifica el contexto de una medida o columna calculada.
- **IF()**: Implementa una condición lógica.
- **RELATED()**: Permite acceder a valores de tablas relacionadas.
- **FILTER()**: Filtra una tabla según una condición.
  
Estas funciones, combinadas con otras más avanzadas, permiten construir modelos de datos dinámicos y complejos, ofreciendo a los usuarios de Power BI la capacidad de extraer información significativa a partir de grandes volúmenes de datos.

## Enlaces de interés

Si deseas profundizar en DAX y aprender más sobre su uso en Power BI, te recomendamos los siguientes recursos:

- [Documentación oficial de Microsoft sobre DAX](https://docs.microsoft.com/es-es/dax/)
- [Funciones DAX más usadas en Power BI](https://docs.microsoft.com/es-es/dax/dax-function-reference)

Estos recursos proporcionan guías detalladas, ejemplos prácticos y mejores prácticas para que puedas dominar el uso de DAX en Power BI.

## Conclusión

DAX es una de las herramientas más potentes en el ecosistema de Power BI y ofrece una gran cantidad de posibilidades para el análisis de datos. Aunque puede parecer complejo al principio, con práctica y el uso de recursos adecuados, es posible crear modelos de datos avanzados y cálculos dinámicos que elevan el potencial de los informes y dashboards.

El dominio de DAX no solo mejora la precisión y utilidad de los informes, sino que también permite que los datos revelen patrones y tendencias que serían difíciles de detectar sin un análisis profundo.
