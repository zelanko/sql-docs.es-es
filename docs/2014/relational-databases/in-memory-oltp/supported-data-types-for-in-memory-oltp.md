---
title: Tipos de datos admitidos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a7380ef0-c9d7-49e4-b6de-fad34752b9f3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de5f805a9d722974adf7975f713436bc7b1ca4d0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075305"
---
# <a name="supported-data-types"></a>Tipos de datos admitidos
  Los siguientes tipos de datos se **admiten** en las tablas optimizadas para memoria y los procedimientos almacenados compilados de forma nativa:  
  
 **Tipos de datos numéricos**  
  
|Tipo de datos|Para obtener más información|  
|---------------|--------------------------|  
|INT|[int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|BIGINT|[int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|SMALLINT|[int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|TINYINT|[int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql)|  
|Decimal|[decimal y numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|NUMERIC|[decimal y numeric &#40;Transact-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)|  
|FLOAT|[float y real &#40;Transact-SQL&#41;](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|REAL|[float y real &#40;Transact-SQL&#41;](/sql/t-sql/data-types/float-and-real-transact-sql)|  
|money|[money y smallmoney &#40;Transact-SQL&#41;](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
|SMALLMONEY|[money y smallmoney &#40;Transact-SQL&#41;](/sql/t-sql/data-types/money-and-smallmoney-transact-sql)|  
  
 **Tipos de datos de cadena**  
  
|Tipo de datos|Para obtener más información|  
|---------------|--------------------------|  
|char(n)|[char y varchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|varchar (n) <sup>1</sup>|[char y varchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/char-and-varchar-transact-sql)|  
|nchar(n)|[nchar y nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|nvarchar (n) <sup>1</sup>|[nchar y nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
|sysname|[nchar y nvarchar &#40;Transact-SQL&#41;](/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)|  
  
 <sup>1</sup> limitación es de 8060 bytes por fila en total, contando (n) en los tipos de longitud variable.  
  
 Para obtener información sobre las intercalaciones admitidas, consulte [intercalaciones y páginas de códigos](../../database-engine/collations-and-code-pages.md).  
  
 **Tipos de datos de fecha y hora**  
  
|Tipo de datos|Para obtener más información|  
|---------------|--------------------------|  
|Date|[fecha &#40;Transact-SQL&#41;](/sql/t-sql/data-types/date-transact-sql)|  
|time|[time &#40;Transact-SQL&#41;](/sql/t-sql/data-types/time-transact-sql)|  
|DATETIME|[datetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql)|  
|datetime2|[datetime2 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/datetime2-transact-sql)|  
|smalldatetime|[smalldatetime &#40;Transact-SQL&#41;](/sql/t-sql/data-types/smalldatetime-transact-sql)|  
  
 **Tipos de datos binarios**  
  
|Tipo de datos|Para obtener más información|  
|---------------|--------------------------|  
|bit|[bit &#40;Transact-SQL&#41;](/sql/t-sql/data-types/bit-transact-sql)|  
|binary(n)|[binary y varbinary &#40;Transact-SQL&#41;](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
|varbinary <sup>1</sup>|[binary y varbinary &#40;Transact-SQL&#41;](/sql/t-sql/data-types/binary-and-varbinary-transact-sql)|  
  
 <sup>1</sup> limitación es de 8060 bytes por fila en total, contando (n) en los tipos de longitud variable.  
  
 **Otros tipos de datos**  
  
|Tipo de datos|Para obtener más información|  
|---------------|--------------------------|  
|UNIQUEIDENTIFIER|[uniqueidentifier &#40;Transact-SQL&#41;](/sql/t-sql/data-types/uniqueidentifier-transact-sql)|  
  
 **Tipos de datos no admitido**  
  
 No se admiten los tipos de datos siguientes:  
  
||||  
|-|-|-|  
|DATETIMEOFFSET|GEOGRAPHY|GEOMETRY|  
|HIERARCHYID|Objetos grandes (LOB). Por ejemplo, varchar(max), nvarchar(max), varbinary(max), image, xml, text y ntext.|ROWVERSION|  
|sql_variant|Funciones CLR|Tipos definidos por el usuario (UDT)|  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad de Transact-SQL con OLTP en memoria](transact-sql-support-for-in-memory-oltp.md)   
 [Implementar columnas LOB en una tabla con optimización para memoria](../../database-engine/implementing-lob-columns-in-a-memory-optimized-table.md)   
 [Implementar SQL_VARIANT en una tabla con optimización para memoria](implementing-sql-variant-in-a-memory-optimized-table.md)  
  
  
