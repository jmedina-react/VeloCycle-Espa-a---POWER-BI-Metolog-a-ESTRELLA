# 🚴 VeloCycle España — Dashboard de Ventas en Power BI
<img width="1118" height="611" alt="image" src="https://github.com/user-attachments/assets/f71b1aff-9205-4bbe-a96d-80d9c9cf37e0" />

<img width="1018" height="550" alt="image" src="https://github.com/user-attachments/assets/457f087f-b3bf-44f8-83cf-512115a4e456" />


## 🏢 Contexto de la Empresa
VeloCycle España S.L. es una empresa distribuidora de bicicletas y accesorios deportivos con sede en Madrid, fundada en 2010. Opera a nivel nacional a través de una red de 4 representantes comerciales que atienden 21 clientes distribuidos en 15 comunidades autónomas, organizados en 5 zonas geográficas: Centro, Este, Norte, Oeste y Sur. Su catálogo incluye 16 referencias de producto, desde bicicletas de carretera y mountain bikes hasta accesorios como gafas y cascos, comercializados a través de tres canales: Mayoristas, Distribuidores y Clientes Finales.

## ❗Problema de Negocio
Entre 2013 y 2015, la dirección comercial de VeloCycle España detectó una serie de problemas críticos que amenazaban la rentabilidad de la empresa:

Caída brusca de ventas en 2015: Las ventas netas cayeron de ~3,5M€ en 2014 a ~1,5M€ en 2015, una reducción de más del 56% que no tenía explicación clara para la gerencia.
Desconocimiento del rendimiento por zona: El equipo directivo no sabía qué zonas geográficas generaban más ingresos ni cuáles estaban por debajo del objetivo. Las decisiones de asignación de representantes se tomaban sin datos.
Márgenes opacos: Existía una diferencia significativa entre el precio bruto facturado y el neto cobrado, pero nadie controlaba de forma sistemática el descuento medio aplicado ni su impacto por cliente o familia de producto.
Canal de venta sin monitoreo: La empresa vendía a mayoristas, distribuidores y clientes finales, pero no tenía visibilidad de qué canal era más rentable ni cómo evolucionaba la mezcla de clientes mes a mes.
Reportes manuales lentos: Los informes de ventas se generaban en Excel de forma manual cada mes, lo que consumía horas de trabajo y generaba errores frecuentes.


## 💡 Solución: Dashboard de Ventas en Power BI
Se desarrolló un Dashboard interactivo en Power BI que centraliza toda la información de ventas (2013–2015) con capacidad de filtrado dinámico por año, mes y zona. El modelo de datos sigue la metodología de modelo estrella (Star Schema), garantizando rendimiento óptimo y facilidad de mantenimiento.

Los datos inicialmente se encuentraron en una tabla, combinadas con la tabla de hechos y dimensiones.
<img width="1586" height="716" alt="image" src="https://github.com/user-attachments/assets/e8204ddb-a5c7-4dc3-9e3a-944838244adc" />
Lo cual para la solución viable y optimo era el "esquema estrella", por tanto se separó tablas de dimensiones, cada uno con sus propios %PK unicos.

<img width="201" height="422" alt="image" src="https://github.com/user-attachments/assets/8b3ea86f-cc40-4282-91a9-0f497eb53579" />

## ⭐ Modelo de Datos — Esquema Estrella
El modelo está compuesto por 1 tabla de hechos y 4 tablas de dimensión, siguiendo estrictamente la metodología estrella:
       <img width="846" height="602" alt="image" src="https://github.com/user-attachments/assets/c2aedb4f-3b49-47f6-8742-0d9f1a17b4fd" />

### Tablas del modelo
Tabla Tipo Descripción Venta Hechos Transacciones de venta: Neto, Bruto, Unidades, Nº FacturaCliente Dimensión Código, nombre, clasificación (Mayorista / Distribuidor / Cliente Final) ArtículoDimensión Código, descripción, familia de producto Territorio VentaDimensiónZona, comunidad autónoma, provinciaTiempoDimensiónFecha completa, mes, trimestre, año, nombre mes

## 📊 Dashboard — Vistas Principales
Vista Principal: Análisis por Zona y Periodo
El dashboard principal permite filtrar por año (2013, 2014, 2015), mes y zona geográfica, mostrando:

KPIs superiores: Total Bruto, Total Neto, Unidades vendidas y Número de Facturas.
* Gráfico Bruto vs Neto por provincia: Comparativa de barras con línea de tendencia del neto.
* Mapa geográfico: Burbujas proporcionales al volumen de ventas por región en España.
* Gráfico de dona por zona: Distribución porcentual de ventas (Centro 46%, Oeste 21%, Norte 18%, Este 13%, Sur 2%).
* Facturas por mes y tipo de cliente: Segmentado entre Distribuidores y Mayoristas.


### 📐 Medidas DAX Implementadas
dax-- Ventas netas totales
Total Neto = SUM(Venta[Neto])

-- Ventas brutas totales
Total Bruto = SUM(Venta[Bruto])

-- Total de unidades vendidas
Total Unidades = SUM(Venta[Unidades])

-- Número de facturas únicas
Nº Facturas = DISTINCTCOUNT(Venta[Nº factura])

-- Promedio Unidades
Total Unidades = SUM(Venta[Unidades])

### 🔍 Hallazgos Clave

📉 La caída de 2015 se explica por datos parciales (solo hasta abril), no por una crisis real de negocio.
🏆 Cantabria y Madrid son las provincias con mayor volumen bruto, superando los 88K y 100K respectivamente (zona Centro).
💼 Mayoristas representan el canal dominante con más del 50% de las facturas, seguidos por distribuidores.
🗺️ La zona Centro concentra el 46% de todas las ventas nacionales, siendo la más estratégica.
📦 Las bicicletas de carretera y mountain bikes son las familias con mayor rotación.


### 🛠️ Tecnologías Utilizadas

Power BI Desktop — Modelado, DAX y visualización
Power Query (M) — Transformación y limpieza de datos
Excel — Fuente de datos transaccional
DAX — Medidas y KPIs calculados


### 👤 Autor
Proyecto desarrollado como práctica de Business Intelligence aplicando la metodología de modelo estrella para análisis comercial de una empresa distribuidora.
### 💡 Los datos de clientes y empresa son ficticios con fines académicos y de demostración.
