# 🧾Creación de la tabla Recibos y selección de los datos a mostrar

## Objetivo de la tabla

La tabla **Recibos** se utiliza para mostrar la información relacionada con los pagos realizados por los inmuebles. Dado que un inmueble puede estar asociado con múltiples terceros que han realizado pagos, se optó por un enfoque que permite sumar todos los importes de los actos documentados vinculados a cada cuenta. Esto es especialmente relevante en casos de subrogación, donde varios terceros pueden haber pagado por el mismo inmueble.

## Estructura de la Tabla Recibos

La tabla **Recibos** está compuesta por las siguientes columnas:

- **Cuenta**: Identifica de manera única el inmueble.
- **Importe**: Muestra el importe pagado hasta la fecha seleccionada.
- **PorcentajePagado**: Indica el porcentaje del valor total del inmueble que ha sido pagado.
- **PagadoHastaFecha**: Muestra el importe pagado hasta una fecha específica.
- **TotalImporte**: Representa el importe total cobrado por cada cuenta.
- **ValorInmueble**: Indica el valor total del inmueble asociado.

## Proceso de Creación de la Tabla

### 1. Definición de la columna Cuenta

Para resolver el problema de calcular el importe pagado por un inmueble, se definió la columna **Cuenta** en la tabla **reciboinformacion**, que es la fuente de los importes. Dado que el número de cuenta de un inmueble permanece constante, cualquier coincidencia en la cuenta indica que ha habido subrogación.

### 2. Creación de una nueva tabla de Importes Cobrados

Se creó una tabla intermedia para representar todos los importes cobrados, que se filtraron según el tipo de estado "C" (cobrado). La consulta DAX utilizada fue:

```dax
NuevaTablaRecibos = 
SELECTCOLUMNS(
    FILTER(
        'safir reciboinformacion',
        'safir reciboinformacion'[tipoestado] = "C"
    ),
    "Cuenta", 'safir reciboinformacion'[Cuenta],
    "Importe", 'safir reciboinformacion'[importe],
    "Fecha", 'safir reciboinformacion'[fecha]
)
```

### 3. Sumarización de Importes por Cuenta

A partir de la tabla anterior, se creó otra tabla que resume el importe total por cuenta utilizando la siguiente consulta DAX:

```dax
TablaSumaImportesPorCuenta = 
SUMMARIZE(
    'NuevaTablaRecibos',          -- Tabla origen
    'NuevaTablaRecibos'[Cuenta],  -- Columna para agrupar (Cuenta)
    "TotalImporte",               -- Nombre de la nueva columna que contendrá la suma
    SUM('NuevaTablaRecibos'[Importe])  -- Suma de los importes por cuenta
)
```

```admonish warning title="Importante"
Una vez que se ha creado esta nueva tabla, es necesario acceder a la **Vista de Modelo** para establecer una relación entre el campo *Cuenta* de la tabla **actodocumentado** y el campo *Cuenta* la nueva tabla.

![Relacion de los campos Cuenta](../assets/RelacionDeCuenta.png)
```

### 4. Adición de la columna ValorInmueble

Se añadió la columna ValorInmueble a la tabla de sumas, la cual se calcula para optimiza el rendimiento y reducir la carga de búsqueda por relaciones. La consulta DAX para esta columna es la siguiente:

```dax
ValorInmueble =  
CALCULATE(
    MAX('safir actodocumentado'[ValorInmueble]),
    FILTER(
        'safir actodocumentado',
        'safir actodocumentado'[Cuenta] = TablaSumaImportesPorCuenta[Cuenta])
)
```

Este enfoque permite almacenar los cálculos en la tabla, evitando cálculos continuos que podrían consumir recursos en el sistema.

### 5. Creación de Medidas para Importes y Porcentajes

Finalmente, se declararon dos medidas que permiten calcular el importe pagado hasta una fecha seleccionada y el porcentaje pagado:

#### Medida: Importe Pagado Hasta Fecha Seleccionada

```dax
ImportePagadoHastaFechaSeleccionadaPorCuenta = 
VAR MesSeleccionadoTexto = SELECTEDVALUE('safir reciboinformacion'[fecha].[Mes])
VAR MesSeleccionado = 
    SWITCH(
        MesSeleccionadoTexto,
        "enero", 1,
        "febrero", 2,
        "marzo", 3,
        "abril", 4,
        "mayo", 5,
        "junio", 6,
        "julio", 7,
        "agosto", 8,
        "septiembre", 9,
        "octubre", 10,
        "noviembre", 11,
        "diciembre", 12,
        BLANK()
    )
VAR AnioSeleccionado = SELECTEDVALUE('safir reciboinformacion'[fecha].[Año], YEAR(TODAY()))
VAR FechaFinal = 
    IF(
        ISBLANK(MesSeleccionado) && NOT ISBLANK(AnioSeleccionado),
        DATE(AnioSeleccionado, 12, 31),
        IF(
            NOT ISBLANK(MesSeleccionado) && ISBLANK(AnioSeleccionado),
            DATE(YEAR(TODAY()), MesSeleccionado, DAY(EOMONTH(TODAY(), 0))),
            IF(
                NOT ISBLANK(MesSeleccionado) && NOT ISBLANK(AnioSeleccionado),
                DATE(AnioSeleccionado, MesSeleccionado, DAY(EOMONTH(DATE(AnioSeleccionado, MesSeleccionado, 1), 0))),
                TODAY()
            )
        )
    )

RETURN
    CALCULATE(
        SUM('NuevaTablaRecibos'[Importe]),
        'NuevaTablaRecibos'[Fecha] < FechaFinal,
        'NuevaTablaRecibos'[Cuenta] = SELECTEDVALUE(TablaSumaImportesPorCuenta[Cuenta])
    )
```

#### Medida: Porcentaje Pagado

```dax
PorcentajePagadoPorCuenta = 
VAR ImportePagado = [ImportePagadoHastaFechaSeleccionadaPorCuenta]
VAR ValorInmueble = SELECTEDVALUE(TablaSumaImportesPorCuenta[ValorInmueble])

RETURN
IF(
    NOT ISBLANK(ValorInmueble) && ValorInmueble > 0,
    DIVIDE(ImportePagado, ValorInmueble, 0),  -- Calcula el porcentaje
    0  -- Devuelve 0 si el valor del inmueble es nulo o menor o igual a 0
)
```

## Conclusión

Con los pasos anteriores, se ha creado la tabla **Recibos**, que recopila información clave sobre los pagos realizados por los inmuebles. Esta tabla permite no solo visualizar el importe pagado, sino también calcular el porcentaje pagado respecto al valor total de cada inmueble. 

Es importante señalar que, aunque es posible lograr resultados similares mediante el uso de medidas DAX más directas y evitando la creación de tablas intermedias, la decisión de proceder de esta manera se debió a las limitaciones de recursos disponibles. En este informe, se optó por cargar la base de datos completa, que es considerablemente grande. Esta estrategia fue necesaria para facilitar la integración y análisis de datos, a pesar de que podría haber llevado a una mayor complejidad en el modelado. Aun así, el enfoque adoptado asegura la funcionalidad requerida y el rendimiento necesario para manejar los datos de manera eficiente en el entorno de Power BI.