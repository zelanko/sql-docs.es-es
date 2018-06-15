---
title: Tipos de datos admitidos para OLTP en memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c4d69ffbb4c8efb71f31fc18009284ad0cfab9e6
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
ms.locfileid: "34328186"
---
# <a name="supported-data-types-for-in-memory-oltp"></a>Tipos de datos admitidos para OLTP en memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  En este artículo se enumeran los tipos de datos que no son compatibles para las características de OLTP en memoria de:  
  
-   Tablas con optimización para memoria  
  
-   Módulos T-SQL compilados de manera nativa  
  
## <a name="unsupported-data-types"></a>Tipos de datos no compatibles  
 No se admiten los tipos de datos siguientes:  
  
||||  
|-|-|-|  
|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography &#40;Transact-SQL&#41;](../../t-sql/spatial-geography/spatial-types-geography.md)|[geometry &#40;Transact-SQL&#41;](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)|  
|[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|Tipos definidos por el usuario|.|  
  
## <a name="notable-supported-data-types"></a>Tipos de datos admitidos importantes  
 La mayoría de los tipos de datos son compatibles con las características de OLTP en memoria. A continuación se indican solo algunos que conviene señalar explícitamente:  
  
|Tipos de cadena y binario|Para obtener más información|  
|-----------------------------|--------------------------|  
|binary y varbinary*|[binary y varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char y varchar*|[char y varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar y nvarchar*|[nchar y nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
A partir de SQL Server 2016, cabe destacar lo siguiente en relación con los tipos de datos binarios y de cadena anteriores:  
  
- Cada tabla individual optimizada para memoria puede tener varias columnas long como `nvarchar(4000)`, aunque sus longitudes agregarían más que el tamaño de fila físico de 8060 bytes.  
  
- Una tabla optimizada para memoria puede tener columnas de tipos de datos de cadena y binarias de longitud máxima, como `varchar(max)`.  


### <a name="identify-lobs-and-other-columns-that-are-off-row"></a>Identificar las columnas de LOB y otras columnas no consecutivas

A partir de SQL Server 2016, las tablas optimizadas en memoria [admiten las columnas de forma no consecutiva](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md), lo que permite que una sola fila de tabla sea mayor que 8060 bytes. La siguiente instrucción Transact-SQL SELECT informa de todas las columnas que no son consecutivas en tablas optimizadas para memoria. Tenga en cuenta lo siguiente:

- Todas las columnas de clave de índice se almacenan en filas consecutivas.
  - Las claves de índice no únicas ahora pueden incluir columnas que aceptan valores NULL en tablas optimizadas para memoria.
  - Los índices se pueden declarar como UNIQUE en una tabla optimizada para memoria.
- Todas las columnas de LOB se almacenan en filas no consecutivas.
- Un valor en max_length de -1 indica una columna de objetos grandes (LOB).


```sql
SELECT
        OBJECT_NAME(m.object_id) as [table],
        c.name                   as [column],
        c.max_length
    FROM
             sys.memory_optimized_tables_internal_attributes AS m
        JOIN sys.columns                                     AS c
                ON  m.object_id = c.object_id
                AND m.minor_id  = c.column_id
    WHERE
        m.type = 5;
```


### <a name="other-data-types"></a>Otros tipos de datos


|Otros tipos|Para obtener más información|  
|-----------------|--------------------------|  
|Tipos de tabla|[Variables de tabla con optimización para memoria](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)|  
  
## <a name="see-also"></a>Ver también  
 [Compatibilidad de Transact-SQL con OLTP en memoria](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [Implementar SQL_VARIANT en una tabla con optimización para memoria](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
 [Tamaño de tabla y fila de tabla optimizada para memoria](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
