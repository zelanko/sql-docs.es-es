---
title: compatibilidad con tipos de fecha y hora de sql_variant | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e16fe8289ae2e92ee21a59c378b4093c0380e1ac
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409094"
---
# <a name="sqlvariant-support-for-date-and-time-types"></a>compatibilidad con tipos de fecha y hora de sql_variant
  En este tema se describe la forma en que el tipo de datos `sql_variant` admite una funcionalidad de fecha y hora mejorada.  
  
 El atributo de columna SQL_CA_SS_VARIANT_TYPE se usa para devolver el tipo C de una columna de resultados variant. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Introduce un atributo adicional, SQL_CA_SS_VARIANT_SQL_TYPE, que establece el tipo SQL de una columna de resultados variant en el descriptor de fila de implementación (IRD). SQL_CA_SS_VARIANT_SQL_TYPE también puede usarse en el descriptor de parámetro de implementación (IPD) para especificar el tipo SQL de un SQL_SS_TIME2 o parámetro SQL_SS_TIMESTAMPOFFSET que tiene un tipo SQL_C_BINARY de C enlazado al tipo SQL_SS_VARIANT.  
  
 Se pueden establecer los nuevos tipos SQL_SS_TIME2 y SQL_SS_TIMESTAMPOFFSET SQLColAttribute. SQLGetDescField puede devolver SQL_CA_SS_VARIANT_SQL_TYPE.  
  
 Para las columnas de resultados, el controlador convertirá el tipo variant en un tipo de fecha y hora. Para obtener más información, consulte [conversiones de SQL a C](datetime-data-type-conversions-from-sql-to-c.md). Al realizar un enlace a SQL_C_BINARY, la longitud del búfer debe ser lo suficientemente grande como para recibir la estructura correspondiente al tipo SQL.  
  
 Para los parámetros SQL_SS_TIME2 y SQL_SS_TIMESTAMPOFFSET, el controlador convertirá los valores de C en valores `sql_variant`, tal y como describe a continuación en la tabla. Si un parámetro se enlaza como SQL_C_BINARY y el tipo de servidor es SQL_SS_VARIANT, se considerará como un valor binario a menos que la aplicación haya establecido SQL_CA_SS_VARIANT_SQL_TYPE en un otro tipo SQL. En este caso, SQL_CA_SS_VARIANT_SQL_TYPE tiene prioridad; es decir, si se establece SQL_CA_SS_VARIANT_SQL_TYPE, invalida el comportamiento predeterminado de deducir el tipo variant de SQL a partir del tipo de C.  
  
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
|SQL_C_BINARY|time|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de `SQLBindParameter`).|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de `SQLBindParameter`).|  
|SQL_C_TYPE_DATE|Date|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TYPE_TIME|time(0)|Se omite SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Escala se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de `SQLBindParameter`).|  
|SQL_C_NUMERIC|Decimal|Precisión se establece en SQL_DESC_PRECISION (el *ColumnSize* parámetro de `SQLBindParameter`).<br /><br /> Conjunto de escalado en SQL_DESC_SCALE (el *ColumnSize* parámetro de SQLBindParameter).|  
|SQL_C_SS_TIME2|time|Se ignora SQL_CA_SS_VARIANT_SQL_TYPE.|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|Se ignora SQL_CA_SS_VARIANT_SQL_TYPE.|  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
