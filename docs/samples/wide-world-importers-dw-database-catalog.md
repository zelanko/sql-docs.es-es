---
title: Catálogo de base de datos OLAP WideWorldImporters - SQL | Documentos de Microsoft
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
ms.openlocfilehash: 7b4533ec0667bc59317ba213578db7301c15b241
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimportersdw-database-catalog"></a>Catálogo de base de datos de WideWorldImportersDW
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Explicaciones de esquemas, tablas y procedimientos almacenados en la base de datos de WideWorldImportersDW. 

La base de datos de WideWorldImportersDW se usa para el almacenamiento de datos y procesamiento analítico. Los datos transaccionales sobre ventas y las compras se generado en la base de datos WideWorldImporters y cargan en la base de datos de WideWorldImportersDW mediante un **proceso ETL diario**.

Por lo tanto, los datos de WideWorldImportersDW refleja los datos de WideWorldImporters, pero las tablas se organizan de manera diferente. Mientras que WideWorldImporters tiene un esquema normalizado tradicional, WideWorldImportersDW usa la [esquema de estrella](https://wikipedia.org/wiki/Star_schema) enfoque para el diseño de tabla. Además de las tablas de hechos y dimensiones, la base de datos incluye una serie de tablas de almacenamiento provisional que se utilizan en el proceso ETL.

## <a name="schemas"></a>Esquemas

Los diferentes tipos de tablas se organizan en tres esquemas.

|Esquema|Description|
|-----------------------------|---------------------|
|Dimensión|Tablas de dimensiones.|
|Hecho|Tablas de hechos.|  
|Integración|Las tablas de ensayo y otros objetos necesarios para ETL.|  

## <a name="tables"></a>Tablas

Las tablas de hechos y dimensiones se muestran a continuación. Las tablas en el esquema de integración se usan únicamente para el proceso ETL y no se muestran.

### <a name="dimension-tables"></a>Tablas de dimensiones

WideWorldImportersDW tiene las siguientes tablas de dimensiones. La descripción incluye la relación con las tablas de origen en la base de datos WideWorldImporters.

|Table|Tablas de origen|
|-----------------------------|---------------------|
|City|`Application.Cities`, `Application.StateProvinces`, `Application.Countries`.|
|Customer|`Sales.Customers`, `Sales.BuyingGroups`, `Sales.CustomerCategories`.|
|Date|Nueva tabla con información acerca de las fechas, incluyendo el año financiero (según el 1 de noviembre de inicio para el ejercicio).|
|Employee|`Application.People`.|
|StockItem|`Warehouse.StockItems`, `Warehouse.Colors`, `Warehouse.PackageType`.|
|Proveedor|`Purchasing.Suppliers`, `Purchasing.SupplierCategories`.|
|PaymentMethod|`Application.PaymentMethods`.|
|TransactionType|`Application.TransactionTypes`.|

### <a name="fact-tables"></a>Tablas de hechos

WideWorldImportersDW tiene las siguientes tablas de hechos. La descripción incluye la relación con las tablas de origen en la base de datos WideWorldImporters, así como las clases de informes de análisis y consultas, con que cada tabla de hechos se suele utilizar.

|Table|Tablas de origen|Análisis de ejemplo|
|-----------------------------|---------------------|---------------------|
|Pedido de|`Sales.Orders`y`Sales.OrderLines`|Ventas personas, productividad de compresor/selector y en el tiempo suficiente para elegir los pedidos. Además, bajo cotizaciones situaciones que conducen a pedidos en espera.|
|Venta|`Sales.Invoices`y`Sales.InvoiceLines`|Fechas de ventas, las fechas de entrega, rentabilidad con el tiempo, la rentabilidad por vendedor.|
|Compra|`Purchasing.PurchaseOrderLines`|Tiempos de entrega real de vs esperado|
|Transaction|`Sales.CustomerTransactions`y`Purchasing.SupplierTransactions`|Medir la fechas de finalización de vs de problema fechas y cantidades.|
|Movimiento|`Warehouse.StockTransactions`|Movimientos con el tiempo.|
|Cartera de valores|`Warehouse.StockItemHoldings`|Los niveles de existencias del inventario y el valor.|

## <a name="stored-procedures"></a>Procedimientos almacenados

Los procedimientos almacenados se utilizan principalmente para el proceso ETL y para fines de configuración.

Las extensiones de la muestra se recomienda utilizar la `Reports` esquema para los informes de Reporting Services y el `PowerBI` esquema para el acceso de Power BI.

### <a name="application-schema"></a>Esquema de la aplicación

Estos procedimientos se utilizan para configurar el ejemplo. Se utilizan para aplicar las características de la edición enterprise a la versión standard edition de la muestra, agregar PolyBase y reinicializar ETL.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|Configuration_ApplyPartitionedColumnstoreIndexing|Se aplica a índices de partición y almacén de columnas para las tablas de hechos.|
|Configuration_ConfigureForEnterpriseEdition|Aplica particiones, indización y en memoria de almacén de columnas.|
|Configuration_EnableInMemory|Reemplaza las tablas de ensayo de integración con las tablas optimizadas en memoria para mejorar el rendimiento de ETL.|
|Configuration_ApplyPolybase|Configura un origen de datos externo, el formato de archivo y la tabla.|
|Configuration_PopulateLargeSaleTable|Aplica los cambios de enterprise edition, a continuación, rellena una mayor cantidad de datos para el año 2012 como historial adicional.|
|Configuration_ReseedETL|Quita los datos existentes y se reinicia las inicializaciones de ETL. Esto permite al rellenar la base de datos OLAP para que coincida con las filas actualizadas en la base de datos OLTP.|

### <a name="integration-schema"></a>Esquema de integración

Los procedimientos utilizados en el proceso ETL se dividen en estas categorías:
- Procedimientos auxiliares para el paquete ETL - Get * todos los procedimientos.
- Utilizado por el paquete ETL para migrar los procedimientos almacenados provisionalmente datos en las tablas de almacenamiento de datos - todos los procedimientos de migración *.
- `PopulateDateDimensionForYear` -Toma un año y se asegura de que todas las fechas de dicho año se rellenan en el `Dimension.Date` tabla.

### <a name="sequences-schema"></a>Esquema de secuencias

Procedimientos para configurar las secuencias en la base de datos.

|Procedimiento|Finalidad|
|-----------------------------|---------------------|
|ReseedAllSequences|Llama al procedimiento `ReseedSequenceBeyondTableValue` para todas las secuencias.|
|ReseedSequenceBeyondTableValue|Se utiliza para volver a colocar el siguiente valor de secuencia por encima del valor de cualquier tabla que usa la misma secuencia. (Al igual que un `DBCC CHECKIDENT` para equivalente de columnas de identidad para las secuencias pero entre varias tablas potencialmente.)|
