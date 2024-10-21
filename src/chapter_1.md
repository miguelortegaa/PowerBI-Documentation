# Documentación de Informes en Power BI

## Introducción
En este proyecto se han desarrollado dos informes utilizando Power BI, conectados a una base de datos PostgreSQL. El objetivo es mostrar datos relevantes de los *actos documentados* y los *recibos*, así como una lista de ayudas. A continuación, se detallan los pasos realizados para la configuración de la aplicación, la carga de los datos, y la creación de los informes.

---

## 1. Configuración del entorno y de la base de datos

### 1.1 Instalación de Power BI
Para comenzar con la creación de los informes, es necesario tener instalada la herramienta Power BI Desktop. Puedes descargarla desde el siguiente enlace: [Power BI Desktop](https://powerbi.microsoft.com/es-es/downloads/).

### 1.2 Conexión a la base de datos PostgreSQL
1. **Instalación del conector de PostgreSQL**: Para conectarte a PostgreSQL desde Power BI, primero asegúrate de tener instalado el controlador de PostgreSQL. Lo puedes obtener en la página oficial de [PostgreSQL](https://www.postgresql.org/download/).
2. **Configuración de la conexión**: Al abrir Power BI, selecciona la opción "Obtener datos" > "PostgreSQL". Luego, ingresa los detalles de conexión (servidor, puerto, base de datos, usuario, contraseña).

```plaintext
Servidor: localhost
Puerto: 5432
Base de datos: nombre_de_tu_base_de_datos
Usuario: usuario
Contraseña: contraseña
```