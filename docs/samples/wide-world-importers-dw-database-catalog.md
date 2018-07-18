---
title: Catálogo de base de datos OLAP WideWorldImporters - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: de537c60f8adf2d4860e236421dd0457871ea025
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37984807"
---
# <a name="wideworldimportersdw-database-catalog"></a>Catálogo de base de datos WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
Obtener una explicación de los esquemas, tablas y procedimientos almacenados en la base de datos WideWorldImportersDW. 

Se utiliza la base de datos WideWorldImportersDW de almacenamiento de datos y procesamiento analítico. Los datos transaccionales sobre ventas y compras es generados en la base de datos WideWorldImporters y cargan en la base de datos WideWorldImportersDW mediante un **proceso ETL diario**.

Por lo tanto, los datos de WideWorldImportersDW refleja los datos de WideWorldImporters, pero las tablas están organizadas de forma diferente. Aunque WideWorldImporters tiene un esquema normalizado tradicional, WideWorldImportersDW usa el [esquema de estrella](https://wikipedia.org/wiki/Star_schema) enfoque para su diseño de tabla. Además de las tablas de hechos y dimensiones, la base de datos incluye una serie de tablas de ensayo que se usan en el proceso ETL.

## <a name="schemas"></a>Esquemas

Los diferentes tipos de tablas se organizan en tres esquemas.

|esquema|Descripción|
|-----------------------------|---------------------|
|Dimensión|Tablas de dimensiones.|
|Hecho|Tablas de hechos.|  
|Integración|Las tablas de almacenamiento provisional y otros objetos necesarios para ETL.|  

## <a name="tables"></a>Tablas

A continuación, se muestran las tablas de hechos y dimensiones. Las tablas en el esquema de la integración se usan únicamente para el proceso ETL y no aparecen.

### <a name="dimension-tables"></a>Tablas de dimensiones

WideWorldImportersDW tiene las siguientes tablas de dimensiones. La descripción incluye la relación con las tablas de origen en la base de datos WideWorldImporters.

|Table|Tablas de origen|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|date|Nueva tabla con información acerca de las fechas, como ejercicio (según el 1 de noviembre iniciar ejercicio).|
|Employee|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|Proveedor|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>Tablas de hechos

WideWorldImportersDW tiene las siguientes tablas de hechos. La descripción incluye la relación con las tablas de origen en la base de datos WideWorldImporters, así como las clases de consultas de informes y análisis que suele utilizarse con cada tabla de hechos.

|Table|Tablas de origen|Análisis de ejemplo|
|-----------------------------|---------------------|---------------------|
|Pedido de|`Sales.Orders` y `Sales.OrderLines`|Ventas de personas, productividad selector/packer y en tiempo para elegir los pedidos. Además, baja conduce a hacer una copia de los pedidos de existencias.|
|Venta|`Sales.Invoices` y `Sales.InvoiceLines`|Las fechas de ventas, las fechas de entrega, la rentabilidad con el tiempo, rentabilidad por vendedor.|
|Compra|`Purchasing.PurchaseOrderLines`|Esperadas y plazos real|
|Transaction|`Sales.CustomerTransactions` y `Purchasing.SupplierTransactions`|Medición de fechas de finalización de vs de problema fechas y cantidades.|
|Movimiento|`Warehouse.StockTransactions`|Movimientos con el tiempo.|
|Cartera de valores|`Warehouse.StockItemHoldings`|En este momento los niveles de existencias y valor.|

## <a name="stored-procedures"></a>Procedimientos almacenados

Los procedimientos almacenados se utilizan principalmente para el proceso ETL y para la configuración.

Las extensiones del ejemplo, se recomienda usar la `Reports` esquema para los informes de Reporting Services y el `PowerBI` esquema para el acceso a Power BI.

### <a name="application-schema"></a>Esquema de la aplicación

Estos procedimientos se usan para configurar el ejemplo. Se utilizan para aplicar las características de enterprise edition a la versión standard edition de la muestra, agregar PolyBase y reseed ETL.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|Se aplica a los índices de almacén de columnas y creación de particiones de tablas de hechos.|
|Configuration_ConfigureForEnterpriseEdition|Se aplica la creación de particiones, indexación y en memoria de almacén de columnas.|
|Configuration_EnableInMemory|Reemplaza las tablas de ensayo de la integración con las tablas optimizadas para memoria SCHEMA_ONLY para mejorar el rendimiento de ETL.|
|Configuration_ApplyPolybase|Configura un origen de datos externo, el formato de archivo y la tabla.|
|Configuration_PopulateLargeSaleTable|Aplica los cambios de enterprise edition, a continuación, rellena una mayor cantidad de datos para el año 2012 como historiales adicionales.|
|Configuration_ReseedETL|Quita los datos existentes y reinicia las inicializaciones de ETL. Esto permite volver a rellenar la base de datos OLAP para que coincida con las filas actualizadas en la base de datos OLTP.|

### <a name="integration-schema"></a>Esquema de la integración

Los procedimientos utilizados en el proceso ETL se dividen en estas categorías:
- Procedimientos auxiliares para el paquete ETL - Get * todos los procedimientos.
- Los procedimientos utilizados por el paquete ETL para migrar los datos de almacenamiento provisional en las tablas de almacenamiento de datos - todos los procedimientos de migración *.
- `PopulateDateDimensionForYear` -Toma un año y garantiza que todas las fechas de ese año se rellenan en el `Dimension.Date` tabla.

### <a name="sequences-schema"></a>Esquema de secuencias

Procedimientos para configurar las secuencias en la base de datos.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|ReseedAllSequences|Llama al procedimiento `ReseedSequenceBeyondTableValue` para todas las secuencias.|
|ReseedSequenceBeyondTableValue|Se utiliza para volver a colocar el siguiente valor de secuencia por encima del valor en cualquier tabla que usa la misma secuencia. (Al igual que un `DBCC CHECKIDENT` para equivalente de columnas de identidad para las secuencias, pero en potencialmente varias tablas.)|
