---
title: SQLDescribeCol | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb0ae64b7a34dc06814d94bbdeafd90f3b4af4cc
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410454"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
  Las instrucciones ejecutadas, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no necesita consultar el servidor para describir las columnas de un conjunto de resultados. En este caso, `SQLDescribeCol` no provoca un ida y vuelta del servidor. Al igual que [SQLColAttribute](sqlnumresultcols.md), al llamar a `SQLDescribeCol` en preparado, pero las instrucciones ejecutadas no genera un ida y vuelta del servidor.  
  
 Cuando una instrucción o lote de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] devuelve varios conjuntos de filas de resultados, es posible que una columna, a la que se hace referencia mediante un ordinal, se cree en una tabla independiente o haga referencia a una columna completamente diferente del conjunto de resultados. `SQLDescribeCol` debe llamarse para cada conjunto. Cuando el conjunto de resultados cambie, la aplicación debe volver a enlazar los valores de datos antes de capturar los resultados de la fila. Para obtener más información sobre el control de resultados múltiples conjuntos, vea [SQLMoreResults](sqlmoreresults.md).  
  
 Los atributos de columna solo se notifican para el primer conjunto de resultados cuando un lote preparado de instrucciones SQL genera varios conjuntos de resultados.  
  
 Tipos de datos de valor grande, el valor devuelto en *DataTypePtr* es SQL_VARCHAR, SQL_VARBINARY o SQL_NVARCHAR. Un valor de SQL_SS_LENGTH_UNLIMITED en *ColumnSizePtr* indica que el tamaño es "ilimitado".  
  
 Mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLDescribeCol obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por SQLDescribeCol en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [detección de metadatos](../native-client/features/metadata-discovery.md).  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>SQLDescribeCol admite las características mejoradas de fecha y hora  
 Los valores devueltos para los tipos de fecha y hora son los siguientes:  
  
||*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|---------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|Date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>SQLDescribeCol admite tipos definidos por el usuario de CLR grandes  
 `SQLDescribeCol` admite tipos CLR definidos por el usuario (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLDescribeCol (función)](http://go.microsoft.com/fwlink/?LinkID=59338)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
