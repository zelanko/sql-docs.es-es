---
title: Creación y acceso a tablas TempDB desde procedimientos almacenados
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 12be8011-b76c-45c1-8f55-7f46e0e374e9
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f4ae543590e5985904e44235da89069c06c649ee
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "74412718"
---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>Creación y acceso a tablas de TempDB desde procedimientos almacenados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  No es posible crear ni obtener acceso a tablas de TempDB desde procedimientos almacenados compilados de forma nativa. En su lugar, use tablas optimizadas para memoria con DURABILITY=SCHEMA_ONLY, o bien use tipos de tabla y variables de tabla. 

Para obtener más información sobre la optimización para memoria de escenarios de tabla temporal y variable de tabla, vea [Faster temp table and table variable by using memory optimization](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)(Tabla temporal y variable de tabla más rápidas mediante la optimización para memoria).
  
  En el ejemplo siguiente se muestra cómo el uso de una tabla temporal con tres columnas (id, ProductID, Quantity) se puede reemplazar mediante una variable de tabla **\@OrderQuantityByProduct** de tipo **dbo.OrderQuantityByProduct**:  
  
```sql  
CREATE TYPE dbo.OrderQuantityByProduct   
  AS TABLE   
   (id INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=100000),   
    ProductID INT NOT NULL,   
    Quantity INT NOT NULL) WITH (MEMORY_OPTIMIZED=ON)  
GO  
CREATE PROCEDURE dbo.usp_OrderQuantityByProduct   
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
    LANGUAGE = N'ENGLISH'  
)  
  -- declare table variables for the list of orders   
  DECLARE @OrderQuantityByProduct dbo.OrderQuantityByProduct  
  
  -- populate input  
  INSERT @OrderQuantityByProduct SELECT ProductID, Quantity FROM dbo.[Order Details]  
  end  
```  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de migración para los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [Construcciones de Transact-SQL no admitidas en In-Memory OLTP.](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
