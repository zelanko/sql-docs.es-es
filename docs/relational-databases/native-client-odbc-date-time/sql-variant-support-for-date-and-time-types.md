---
title: compatibilidad con tipos de fecha y hora de sql_variant | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a5eec057cc9d11f1bae5eb4d50e5ab560f11f9ea
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlvariant-support-for-date-and-time-types"></a>compatibilidad con tipos de fecha y hora de sql_variant
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tema se describe cómo el **sql_variant** tipo de datos admite la funcionalidad mejorada fecha y hora.  
  
 El atributo de columna SQL_CA_SS_VARIANT_TYPE se usa para devolver el tipo C de una columna de resultados variant. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Introduce un atributo adicional, SQL_CA_SS_VARIANT_SQL_TYPE, que establece el tipo SQL de una columna de resultados variant en el descriptor de fila de implementación (IRD). SQL_CA_SS_VARIANT_SQL_TYPE también puede utilizarse en el descriptor de parámetro de implementación (IPD) para especificar el tipo SQL de un SQL_SS_TIME2 o parámetro SQL_SS_TIMESTAMPOFFSET que tiene el tipo de C SQL_C_BINARY enlazado al tipo SQL_SS_VARIANT.  
  
 Los nuevos tipos SQL_SS_TIME2 y SQL_SS_TIMESTAMPOFFSET pueden establecerse SQLColAttribute. SQLGetDescField puede devolver SQL_CA_SS_VARIANT_SQL_TYPE.  
  
 Para las columnas de resultados, el controlador convertirá el tipo variant en un tipo de fecha y hora. Para obtener más información, consulte [conversiones de SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Al realizar un enlace a SQL_C_BINARY, la longitud del búfer debe ser lo suficientemente grande como para recibir la estructura correspondiente al tipo SQL.  
  
 Para los parámetros SQL_SS_TIME2 y SQL_SS_TIMESTAMPOFFSET, el controlador convertirá los valores de C a **sql_variant** valores, como se describe en la tabla siguiente. Si un parámetro se enlaza como SQL_C_BINARY y el tipo de servidor es SQL_SS_VARIANT, se considerará como un valor binario a menos que la aplicación haya establecido SQL_CA_SS_VARIANT_SQL_TYPE en un otro tipo SQL. En este caso, SQL_CA_SS_VARIANT_SQL_TYPE tiene prioridad; es decir, si se establece SQL_CA_SS_VARIANT_SQL_TYPE, invalida el comportamiento predeterminado de deducir el tipo variant de SQL a partir del tipo de C.  
  
|Tipo de C|Tipo de servidor|Comentarios|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_WCHAR|nvarcar|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TINYINT|smallint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_STINYINT|smallint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SHORT|smallint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SSHORT|smallint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_USHORT|int|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_LONG|int|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SLONG|int|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_ULONG|bigint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SBIGINT|bigint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_FLOAT|real|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_DOUBLE|float|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BIT|bit|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_UTINYINT|tinyint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BINARY|varbinary|No se establece SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de **SQLBindParameter**).|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de **SQLBindParameter**).|  
|SQL_C_TYPE_DATE|date|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TYPE_TIME|time(0)|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de **SQLBindParameter**).|  
|SQL_C_NUMERIC|decimal|Precisión se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de **SQLBindParameter**).<br /><br /> Escala se establece en SQL_DESC_SCALE (el *ColumnSize* parámetro de SQLBindParameter).|  
|SQL_C_SS_TIME2|time|Se ignora SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|Se ignora SQL_CA_SS_VARIANT_SQL_TYPE.|  
  
## <a name="see-also"></a>Vea también  
 [Fecha y hora mejoras & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
