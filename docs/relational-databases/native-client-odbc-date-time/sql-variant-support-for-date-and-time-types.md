---
title: compatibilidad con tipos de fecha y hora de sql_variant | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 79b4999db83063e8096abce8a8e1c4dcd5e3a6b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62738892"
---
# <a name="sqlvariant-support-for-date-and-time-types"></a>Compatibilidad con sql_variant para tipos de fecha y hora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tema se describe cómo el **sql_variant** tipo de datos admite la funcionalidad mejorada fecha y hora.  
  
 El atributo de columna SQL_CA_SS_VARIANT_TYPE se usa para devolver el tipo C de una columna de resultados variant. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Introduce un atributo adicional, SQL_CA_SS_VARIANT_SQL_TYPE, que establece el tipo SQL de una columna de resultados variant en el descriptor de fila de implementación (IRD). SQL_CA_SS_VARIANT_SQL_TYPE también puede usarse en el descriptor de parámetro de implementación (IPD) para especificar el tipo SQL de un SQL_SS_TIME2 o parámetro SQL_SS_TIMESTAMPOFFSET que tiene un tipo SQL_C_BINARY de C enlazado al tipo SQL_SS_VARIANT.  
  
 Se pueden establecer los nuevos tipos SQL_SS_TIME2 y SQL_SS_TIMESTAMPOFFSET SQLColAttribute. SQLGetDescField puede devolver SQL_CA_SS_VARIANT_SQL_TYPE.  
  
 Para las columnas de resultados, el controlador convertirá el tipo variant en un tipo de fecha y hora. Para obtener más información, consulte [conversiones de SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Cuando un enlace a SQL_C_BINARY, la longitud del búfer debe ser lo suficientemente grande como para recibir la estructura que corresponde al tipo SQL.  
  
 Para los parámetros SQL_SS_TIME2 y SQL_SS_TIMESTAMPOFFSET, el controlador convertirá los valores de C a **sql_variant** valores, como se describe en la tabla siguiente. Si un parámetro se enlaza como SQL_C_BINARY y el tipo de servidor es SQL_SS_VARIANT, se considerará como un valor binario a menos que la aplicación haya establecido SQL_CA_SS_VARIANT_SQL_TYPE en un otro tipo SQL. En este caso, SQL_CA_SS_VARIANT_SQL_TYPE tiene prioridad; es decir, si se establece SQL_CA_SS_VARIANT_SQL_TYPE, invalida el comportamiento predeterminado de deducir el tipo variant de SQL a partir del tipo de C.  
  
|Tipo de C|Tipo de servidor|Comentarios|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_WCHAR|nvarcar|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TINYINT|SMALLINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_STINYINT|SMALLINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SHORT|SMALLINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SSHORT|SMALLINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_USHORT|INT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_LONG|INT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SLONG|INT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_ULONG|BIGINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SBIGINT|BIGINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_FLOAT|REAL|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_DOUBLE|FLOAT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BIT|bit|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_UTINYINT|TINYINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BINARY|varbinary|No se establece SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de **SQLBindParameter**).|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de **SQLBindParameter**).|  
|SQL_C_TYPE_DATE|date|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TYPE_TIME|time(0)|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de **SQLBindParameter**).|  
|SQL_C_NUMERIC|Decimal|Precisión se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de **SQLBindParameter**).<br /><br /> Conjunto de escalado en SQL_DESC_SCALE (el *ColumnSize* parámetro de SQLBindParameter).|  
|SQL_C_SS_TIME2|time|Se ignora SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|Se ignora SQL_CA_SS_VARIANT_SQL_TYPE.|  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
