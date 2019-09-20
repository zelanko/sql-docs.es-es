---
title: Creación y acceso a tablas de TempDB desde procedimientos almacenados | Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: 14f1d7712973c2c51812a8606b1fc4c1ba15264d
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846788"
---
# <a name="create-and-access-tables-in-tempdb-from-stored-procedures"></a>Creación y acceso a tablas de TempDB desde procedimientos almacenados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  No es posible crear ni obtener acceso a tablas de TempDB desde procedimientos almacenados compilados de forma nativa. En su lugar, use tablas optimizadas para memoria con DURABILITY=SCHEMA_ONLY, o bien use tipos de tabla y variables de tabla. 

Para obtener más información sobre la optimización de memoria de la tabla temporal y escenarios de variable de tabla, vea: [Tabla temporal y variable de tabla más rápidas con optimización para memoria](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).
  
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
 [Construcciones Transact-SQL no admitidas por OLTP en memoria](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
