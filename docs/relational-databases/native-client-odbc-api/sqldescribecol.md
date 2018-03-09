---
title: SQLDescribeCol | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-api
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06d4431256c20928a053f8d913b961bb38c99409
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="sqldescribecol"></a>SQLDescribeCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Las instrucciones ejecutadas, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client no necesita consultar el servidor para describir las columnas de un conjunto de resultados. En este caso, **SQLDescribeCol** no provoca un ida y vuelta del servidor. Al igual que [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)y[SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md), si se llama **SQLDescribeCol** en preparado, pero las instrucciones ejecutadas no genera un ida y vuelta del servidor.  
  
 Cuando una instrucción o lote de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] devuelve varios conjuntos de filas de resultados, es posible que una columna, a la que se hace referencia mediante un ordinal, se cree en una tabla independiente o haga referencia a una columna completamente diferente del conjunto de resultados. **SQLDescribeCol** se debe llamar para cada conjunto. Cuando el conjunto de resultados cambie, la aplicación debe volver a enlazar los valores de datos antes de capturar los resultados de la fila. Para obtener más información sobre el control de resultados múltiples conjuntos devuelve, vea [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Los atributos de columna solo se notifican para el primer conjunto de resultados cuando un lote preparado de instrucciones SQL genera varios conjuntos de resultados.  
  
 Para tipos de datos de valor grande, el valor devuelto en *DataTypePtr* es SQL_VARCHAR, SQL_VARBINARY o SQL_NVARCHAR. Un valor de SQL_SS_LENGTH_UNLIMITED en *ColumnSizePtr* indica que el tamaño es "ilimitado".  
  
 Mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permitir SQLDescribeCol obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por SQLDescribeCol en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Metadata Discovery](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>SQLDescribeCol admite las características mejoradas de fecha y hora  
 Los valores devueltos para los tipos de fecha y hora son los siguientes:  
  
||*DataTypePtr*|*ColumnSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|---------------------|------------------------|  
|datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obtener más información, consulte [fecha y hora mejoras &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>SQLDescribeCol admite tipos definidos por el usuario de CLR grandes  
 **SQLDescribeCol** admite tipos de definidos por el usuario CLR (UDT) grandes. Para obtener más información, consulte [Large CLR User-Defined tipos &#40; ODBC &#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLDescribeCol (función)](http://go.microsoft.com/fwlink/?LinkID=59338)   
 [Detalles de implementación de API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
