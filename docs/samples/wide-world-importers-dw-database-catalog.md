---
title: Catálogo de base de datos OLAP WideWorldImporters - SQL | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 9ead11248d0eebe198890884b427f864cfea756c
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51270168"
---
# <a name="wideworldimportersdw-database-catalog"></a>Catálogo de base de datos de WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Explicación de los esquemas, tablas y procedimientos almacenados en la base de datos de WideWorldImportersDW. 

La base de datos de WideWorldImportersDW se utiliza para el almacenamiento de datos y procesamiento analítico. Los datos transaccionales sobre ventas y compras se genera en la base de datos de WideWorldImporters y cargados en la base de datos de WideWorldImportersDW con un **proceso ETL diario**.

Por lo tanto, los datos de WideWorldImportersDW duplica los datos en WideWorldImporters, pero las tablas se organizan de forma diferente. Mientras que WideWorldImporters tiene un esquema normalizado tradicional, WideWorldImportersDW utiliza la [esquema de estrella](https://wikipedia.org/wiki/Star_schema) enfoque para el diseño de la tabla. Además de las tablas de hechos y dimensiones, la base de datos incluye una serie de tablas de ensayo que se utilizan en el proceso ETL.

## <a name="schemas"></a>Esquemas

Los diferentes tipos de tablas se organizan en tres esquemas.

|esquema|Descripción|
|-----------------------------|---------------------|
|Dimensión|Tablas de dimensiones.|
|Hecho|Tablas de hechos.|  
|Integración|Almacenamiento de tablas y otros objetos necesarios para el ETL.|  

## <a name="tables"></a>Tablas

Las tablas de hechos y dimensiones aparecen a continuación. Las tablas en el esquema de integración se utilizan únicamente para el proceso ETL y no aparecen.

### <a name="dimension-tables"></a>Tablas de dimensiones

WideWorldImportersDW tiene las siguientes tablas de dimensión. La descripción incluye la relación con las tablas de origen en la base de datos de WideWorldImporters.

|Table|Tablas de origen|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|date|Nueva tabla con información sobre fechas, incluyendo ejercicio (basado en 1 de noviembre iniciar ejercicio).|
|Employee|`Application.People` |
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|Proveedor|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods` |
|TransactionType|`Application.TransactionTypes` |

### <a name="fact-tables"></a>Tablas de hechos

WideWorldImportersDW tiene las siguientes tablas de hechos. La descripción incluye la relación con las tablas de origen en la base de datos de WideWorldImporters, así como las clases de consultas de análisis y reporting que suele utilizarse con cada tabla de hechos.

|Table|Tablas de origen|Análisis de la muestra|
|-----------------------------|---------------------|---------------------|
|Pedido de|`Sales.Orders` y `Sales.OrderLines`|Personal, productividad de selector/envasador, de ventas y en tiempo para elegir los pedidos. Además, bajo stock situaciones conducen a pedidos en espera.|
|Venta|`Sales.Invoices` y `Sales.InvoiceLines`|Fechas de ventas, las fechas de entrega, rentabilidad con el tiempo, rentabilidad por vendedor.|
|Compra|`Purchasing.PurchaseOrderLines`|Tiempos de entrega real vs esperado|
|Transacción|`Sales.CustomerTransactions` y `Purchasing.SupplierTransactions`|Medición de importes y fechas de finalización de vs de fechas de problema.|
|Movimiento|`Warehouse.StockTransactions`|Movimientos con el tiempo.|
|Cartera de valores|`Warehouse.StockItemHoldings`|Los niveles de existencias del inventario y el valor.|

## <a name="stored-procedures"></a>Procedimientos almacenados

Los procedimientos almacenados se utilizan principalmente para el proceso ETL y para fines de configuración.

Las extensiones de la muestra se les recomienda usar la `Reports` esquema para los informes de Reporting Services y el `PowerBI` esquema para el acceso de BI de energía.

### <a name="application-schema"></a>Esquema de la aplicación

Estos procedimientos se utilizan para configurar la muestra. Se utilizan para aplicar características de enterprise edition a la versión standard edition de la muestra, agregar PolyBase y sembrar ETL.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|Se aplica a particionar y columnstore índices para las tablas de hechos.|
|Configuration_ConfigureForEnterpriseEdition|Aplica la partición columnstore indización y en la memoria.|
|Configuration_EnableInMemory|Reemplaza las tablas de ensayo de la integración con las tablas optimizadas para memoria SCHEMA_ONLY para mejorar el rendimiento de ETL.|
|Configuration_ApplyPolyBase|Configura un origen de datos externo, el formato de archivo y la tabla.|
|Configuration_PopulateLargeSaleTable|Aplica cambios de edición enterprise y rellena una mayor cantidad de datos para el año 2012 como historial adicional.|
|Configuration_ReseedETL|Elimina los datos existentes y reinicia las semillas ETL. Esto permite rellenar la base de datos OLAP para que coincidan con las filas actualizadas en la base de datos OLTP.|

### <a name="integration-schema"></a>Esquema de integración

Procedimientos utilizados en el proceso ETL se dividen en estas categorías:
- Procedimientos auxiliares para el paquete ETL - Get * todos los procedimientos.
- Procedimientos utilizados por el paquete ETL para migrar datos de prueba en las tablas de DW - todos los procedimientos de migración *.
- `PopulateDateDimensionForYear` -Toma un año y garantiza que todas las fechas para ese año se llenan en el `Dimension.Date` tabla.

### <a name="sequences-schema"></a>Esquema de secuencias

Procedimientos para configurar las secuencias de la base de datos.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|ReseedAllSequences|Llama al procedimiento `ReseedSequenceBeyondTableValue` para todas las secuencias.|
|ReseedSequenceBeyondTableValue|Se utiliza para cambiar la posición del siguiente valor de secuencia más allá del valor de cualquier tabla que utiliza la misma secuencia. (Como un `DBCC CHECKIDENT` para el equivalente de columnas de identidad para secuencias pero en potencialmente varias tablas.)|
