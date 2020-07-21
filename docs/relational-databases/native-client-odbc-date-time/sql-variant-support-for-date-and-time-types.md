---
title: Compatibilidad sql_variant con tipos de fecha y hora | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 004cd59192a0512581a9d70f4cc754d39dd84fd9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004317"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>Compatibilidad con sql_variant para tipos de fecha y hora
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En este tema se describe cómo el tipo de datos **sql_variant** admite la funcionalidad mejorada de fecha y hora.  
  
 El atributo de columna SQL_CA_SS_VARIANT_TYPE se usa para devolver el tipo C de una columna de resultados variant. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduce un atributo adicional, SQL_CA_SS_VARIANT_SQL_TYPE, que establece el tipo SQL de una columna de resultados variant en el descriptor de filas de implementación (IRD). SQL_CA_SS_VARIANT_SQL_TYPE también puede usarse en el descriptor de parámetros de implementación (IPD) para especificar el tipo SQL de un parámetro SQL_SS_TIME2 o SQL_SS_TIMESTAMPOFFSET que tiene un tipo SQL_C_BINARY de C enlazado al tipo SQL_SS_VARIANT.  
  
 Los nuevos tipos SQL_SS_TIME2 y SQL_SS_TIMESTAMPOFFSET pueden establecerse mediante SQLColAttribute. SQLGetDescField puede devolver SQL_CA_SS_VARIANT_SQL_TYPE.  
  
 Para las columnas de resultados, el controlador convertirá el tipo variant en un tipo de fecha y hora. Para obtener más información, vea [conversiones de SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Al enlazar a SQL_C_BINARY, la longitud del búfer debe ser lo suficientemente grande como para recibir el struct correspondiente al tipo SQL.  
  
 En el caso de los parámetros SQL_SS_TIME2 y SQL_SS_TIMESTAMPOFFSET, el controlador convertirá los valores de C en **sql_variant** valores, como se describe en la tabla siguiente. Si un parámetro se enlaza como SQL_C_BINARY y el tipo de servidor es SQL_SS_VARIANT, se considerará como un valor binario a menos que la aplicación haya establecido SQL_CA_SS_VARIANT_SQL_TYPE en un otro tipo SQL. En este caso, SQL_CA_SS_VARIANT_SQL_TYPE tiene prioridad; es decir, si se establece SQL_CA_SS_VARIANT_SQL_TYPE, invalida el comportamiento predeterminado de deducir el tipo variant de SQL a partir del tipo de C.  
  
|Tipo de C|Tipo de servidor|Comentarios|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_WCHAR|nvarcar|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TINYINT|SMALLINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_STINYINT|SMALLINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SHORT|SMALLINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SSHORT|SMALLINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_USHORT|int|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_LONG|int|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SLONG|int|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_ULONG|bigint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SBIGINT|bigint|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_FLOAT|real|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_DOUBLE|FLOAT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BIT|bit|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_UTINYINT|TINYINT|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BINARY|varbinary|No se establece SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Scale se establece en SQL_DESC_PRECISION (el parámetro *ColumnSize* de **SQLBindParameter**).|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Scale se establece en SQL_DESC_PRECISION (el parámetro *ColumnSize* de **SQLBindParameter**).|  
|SQL_C_TYPE_DATE|date|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TYPE_TIME|time(0)|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Scale se establece en SQL_DESC_PRECISION (el parámetro *ColumnSize* de **SQLBindParameter**).|  
|SQL_C_NUMERIC|Decimal|La precisión se establece en SQL_DESC_PRECISION (el parámetro *columnas* de **SQLBindParameter**).<br /><br /> Conjunto de escalado a SQL_DESC_SCALE (el parámetro *ColumnSize* de SQLBindParameter).|  
|SQL_C_SS_TIME2|time|Se ignora SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|Se ignora SQL_CA_SS_VARIANT_SQL_TYPE.|  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
