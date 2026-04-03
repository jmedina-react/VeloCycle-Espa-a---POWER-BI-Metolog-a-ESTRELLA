🚴 VeloCycle España — Dashboard de Ventas en Power BI
Mostrar imagen
Mostrar imagen
Mostrar imagen
Mostrar imagen

🏢 Contexto de la Empresa
VeloCycle España S.L. es una empresa distribuidora de bicicletas y accesorios deportivos con sede en Madrid, fundada en 2010. Opera a nivel nacional a través de una red de 4 representantes comerciales que atienden 21 clientes distribuidos en 15 comunidades autónomas, organizados en 5 zonas geográficas: Centro, Este, Norte, Oeste y Sur.
Su catálogo incluye 16 referencias de producto, desde bicicletas de carretera y mountain bikes hasta accesorios como gafas y cascos, comercializados a través de tres canales: Mayoristas, Distribuidores y Clientes Finales.

❗ Problema de Negocio
Entre 2013 y 2015, la dirección comercial de VeloCycle España detectó una serie de problemas críticos que amenazaban la rentabilidad de la empresa:

Caída brusca de ventas en 2015: Las ventas netas cayeron de ~3,5M€ en 2014 a ~1,5M€ en 2015, una reducción de más del 56% que no tenía explicación clara para la gerencia.
Desconocimiento del rendimiento por zona: El equipo directivo no sabía qué zonas geográficas generaban más ingresos ni cuáles estaban por debajo del objetivo. Las decisiones de asignación de representantes se tomaban sin datos.
Márgenes opacos: Existía una diferencia significativa entre el precio bruto facturado y el neto cobrado, pero nadie controlaba de forma sistemática el descuento medio aplicado ni su impacto por cliente o familia de producto.
Canal de venta sin monitoreo: La empresa vendía a mayoristas, distribuidores y clientes finales, pero no tenía visibilidad de qué canal era más rentable ni cómo evolucionaba la mezcla de clientes mes a mes.
Reportes manuales lentos: Los informes de ventas se generaban en Excel de forma manual cada mes, lo que consumía horas de trabajo y generaba errores frecuentes.


💡 Solución: Dashboard de Ventas en Power BI
Se desarrolló un Dashboard interactivo en Power BI que centraliza toda la información de ventas (2013–2015) con capacidad de filtrado dinámico por año, mes y zona. El modelo de datos sigue la metodología de modelo estrella (Star Schema), garantizando rendimiento óptimo y facilidad de mantenimiento.

⭐ Modelo de Datos — Esquema Estrella
El modelo está compuesto por 1 tabla de hechos y 4 tablas de dimensión, siguiendo estrictamente la metodología estrella:
                    ┌─────────────┐
                    │  DIM Tiempo │
                    │  (Fecha,    │
                    │  Mes, Año,  │
                    │  Trimestre) │
                    └──────┬──────┘
                           │
┌──────────────┐    ┌──────▼───────┐    ┌─────────────────┐
│  DIM Cliente │    │              │    │  DIM Artículo   │
│  (Cod, Nombre│◄───┤  FCT Venta   ├───►│  (Cod, Nombre,  │
│  Clasificac.)│    │  (Neto,Bruto │    │  Familia)       │
└──────────────┘    │  Unidades,   │    └─────────────────┘
                    │  Nº Factura) │
┌──────────────┐    └──────┬───────┘
│  DIM Territ. │           │
│  (Zona,      │◄──────────┘
│  Comunidad,  │
│  Provincia)  │
└──────────────┘
Tablas del modelo
TablaTipoDescripciónVentaHechosTransacciones de venta: Neto, Bruto, Unidades, Nº FacturaClienteDimensiónCódigo, nombre, clasificación (Mayorista / Distribuidor / Cliente Final)ArtículoDimensiónCódigo, descripción, familia de productoTerritorio VentaDimensiónZona, comunidad autónoma, provinciaTiempoDimensiónFecha completa, mes, trimestre, año, nombre mes

📊 Dashboard — Vistas Principales
Vista Principal: Análisis por Zona y Periodo
El dashboard principal permite filtrar por año (2013, 2014, 2015), mes y zona geográfica, mostrando:

KPIs superiores: Total Bruto, Total Neto, Unidades vendidas y Número de Facturas
Gráfico Bruto vs Neto por provincia: Comparativa de barras con línea de tendencia del neto
Mapa geográfico: Burbujas proporcionales al volumen de ventas por región en España
Gráfico de dona por zona: Distribución porcentual de ventas (Centro 46%, Oeste 21%, Norte 18%, Este 13%, Sur 2%)
Facturas por mes y tipo de cliente: Segmentado entre Distribuidores y Mayoristas


📐 Medidas DAX Implementadas
dax-- Ventas netas totales
Total Neto = SUM(Venta[Neto])

-- Ventas brutas totales
Total Bruto = SUM(Venta[Bruto])

-- Descuento medio aplicado (%)
Descuento Medio % = DIVIDE([Total Bruto] - [Total Neto], [Total Bruto], 0)

-- Total de unidades vendidas
Total Unidades = SUM(Venta[Unidades])

-- Número de facturas únicas
Nº Facturas = DISTINCTCOUNT(Venta[Nº factura])

-- Venta neta del año anterior (YoY)
Neto Año Anterior = CALCULATE([Total Neto], SAMEPERIODLASTYEAR(Tiempo[Fecha]))

-- Crecimiento interanual
Crecimiento YoY % = DIVIDE([Total Neto] - [Neto Año Anterior], [Neto Año Anterior], 0)

📈 KPIs Adicionales Recomendados
Los siguientes KPIs están planificados para la siguiente iteración del dashboard:
KPIFórmula DAXPropósitoTicket Medio por FacturaDIVIDE([Total Neto], [Nº Facturas])Medir el valor promedio por operaciónMargen Bruto %DIVIDE([Total Neto], [Total Bruto])Controlar el nivel de descuentos aplicadosUnidades por FacturaDIVIDE([Total Unidades], [Nº Facturas])Eficiencia comercial por transacción% Ventas por CanalDIVIDE([Neto Canal], [Total Neto])Peso de mayoristas vs. distribuidoresCrecimiento YoY %SAMEPERIODLASTYEARComparativa interanual de ventas netasRanking de RepresentantesRANKX(ALL(Cliente[Representante]))Identificar los comerciales más productivosDías sin Venta por ClienteCalculado con MAX y TODAY()Detectar clientes inactivos o en riesgo

🗂️ Estructura del Proyecto
VeloCycle-PowerBI/
│
├── 📁 Data/
│   └── Ventas-Totales-Detalladas.xlsx    # Fuente de datos original
│
├── 📁 PowerBI/
│   └── VeloCycle_Dashboard.pbix          # Archivo Power BI Desktop
│
├── 📁 Screenshots/
│   ├── dashboard_principal.png           # Vista principal - año 2015
│   └── modelo_estrella.png              # Estructura del modelo de datos
│
└── README.md

🔍 Hallazgos Clave

📉 La caída de 2015 se explica por datos parciales (solo hasta abril), no por una crisis real de negocio.
🏆 Cantabria y Madrid son las provincias con mayor volumen bruto, superando los 88K y 100K respectivamente (zona Centro).
💼 Mayoristas representan el canal dominante con más del 50% de las facturas, seguidos por distribuidores.
🗺️ La zona Centro concentra el 46% de todas las ventas nacionales, siendo la más estratégica.
📦 Las bicicletas de carretera y mountain bikes son las familias con mayor rotación.


🛠️ Tecnologías Utilizadas

Power BI Desktop — Modelado, DAX y visualización
Power Query (M) — Transformación y limpieza de datos
Excel — Fuente de datos transaccional
DAX — Medidas y KPIs calculados


👤 Autor
Proyecto desarrollado como práctica de Business Intelligence aplicando la metodología de modelo estrella para análisis comercial de una empresa distribuidora.
