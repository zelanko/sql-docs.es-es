---
title: "Tipos de datos admitidos para OLTP en memoria | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
caps.latest.revision: 26
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 26
---
# Tipos de datos admitidos para OLTP en memoria
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este artículo se enumeran los tipos de datos que no son compatibles para las características de OLTP en memoria de:  
  
-   Tablas con optimización para memoria  
  
-   Procedimientos almacenados compilados de forma nativa  
  
## Tipos de datos no compatibles  
 No se admiten los tipos de datos siguientes:  
  
||||  
|-|-|-|  
|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)|[geography &#40;Transact-SQL&#41;](../Topic/geography%20\(Transact-SQL\).md)|[geometry &#40;Transact-SQL&#41;](../Topic/geometry%20\(Transact-SQL\).md)|  
|[hierarchyid &#40;Transact-SQL&#41;](../Topic/hierarchyid%20\(Transact-SQL\).md)|[rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)|[xml &#40;Transact-SQL&#41;](../../t-sql/xml/xml-transact-sql.md)|  
|[sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)|Tipos definidos por el usuario|.|  
  
## Tipos de datos admitidos importantes  
 La mayoría de los tipos de datos son compatibles con las características de OLTP en memoria. A continuación se indican solo algunos que conviene señalar explícitamente:  
  
|Tipos de cadena y binario|Para obtener más información|  
|-----------------------------|--------------------------|  
|binary y varbinary*|[binary y varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|char y varchar*|[char y varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|nchar y nvarchar*|[nchar y nvarchar &#40;Transact-SQL&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
  
A partir de SQL Server 2016, cabe destacar lo siguiente en relación con los tipos de datos binarios y de cadena anteriores:  
  
- Cada tabla individual con optimización para memoria puede tener varias columnas long como `nvarchar(4000)`, aunque sus longitudes agregarían más que el tamaño de fila físico de 8060 bytes.  
  
- Una tabla con optimización para memoria puede tener columnas de tipos de datos de cadena y binarias de longitud máxima, como `varchar(max)`.  


### Identificar las columnas de LOB y otras columnas no consecutivas

La siguiente instrucción Transact-SQL SELECT informa de todas las columnas que no son consecutivas en tablas con optimización para memoria. Tenga en cuenta lo siguiente:

- Todas las columnas de clave de índice se almacenan en filas consecutivas.
  - Las claves de índice no únicas ahora pueden incluir columnas que aceptan valores NULL en tablas con optimización para memoria.
  - Los índices se pueden declarar como UNIQUE en una tabla con optimización para memoria.
- Todas las columnas de LOB se almacenan en filas no consecutivas.
- Un valor en max_length de -1 indica una columna de objetos grandes (LOB).


```tsql
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


#### Compatibilidad con LOB en módulos compilados de forma nativa


Cuando se usa una función de cadena integrada en un módulo compilado de forma nativa (como, por ejemplo, un proceso nativo), la función puede aceptar una cadena de tipo LOB. Así, en un proceso nativo, la función LTrim puede escribir un parámetro de tipo nvarchar(max) o varbinary(max).

Estos LOB pueden ser el tipo de devolución de una función definida por el usuario escalar compilada de manera nativa.


### Otros tipos de datos


|Otros tipos|Para obtener más información|  
|-----------------|--------------------------|  
|Tipos de tabla|[Variables de tabla con optimización para memoria](../Topic/Memory-Optimized%20Table%20Variables.md)|  
  
## Vea también  
 [Compatibilidad de Transact-SQL con OLTP en memoria](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)   
 [Implementar columnas LOB en una tabla con optimización para memoria](http://msdn.microsoft.com/es-es/bd8df0a5-12b9-4f4c-887c-2fb78dd79f4e)   
 [Implementar SQL_VARIANT en una tabla con optimización para memoria](../../relational-databases/in-memory-oltp/implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  