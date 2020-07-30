---
title: SQLDescribeCol | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeCol function
ms.assetid: ffbf34c6-8268-434f-829a-82009a6cda59
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 84c0a5b48196ddb6fdc5f7fcfb7fe0f9d6cd4d55
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332346"
---
# <a name="sqldescribecol"></a>SQLDescribeCol
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En el caso de las instrucciones ejecutadas, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no necesita consultar el servidor para describir las columnas de un conjunto de resultados. En este caso, **SQLDescribeCol** no produce un viaje de ida y vuelta al servidor. Como [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md)y[SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md), al llamar a **SQLDescribeCol** en instrucciones preparadas pero no ejecutadas se genera un viaje de ida y vuelta al servidor.  
  
 Cuando una instrucción o lote de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] devuelve varios conjuntos de filas de resultados, es posible que una columna, a la que se hace referencia mediante un ordinal, se cree en una tabla independiente o haga referencia a una columna completamente diferente del conjunto de resultados. Se debe llamar a **SQLDescribeCol** para cada conjunto. Cuando el conjunto de resultados cambie, la aplicación debe volver a enlazar los valores de datos antes de capturar los resultados de la fila. Para obtener más información sobre cómo administrar la devolución de varios conjuntos de resultados, vea [SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md).  
  
 Los atributos de columna solo se notifican para el primer conjunto de resultados cuando un lote preparado de instrucciones SQL genera varios conjuntos de resultados.  
  
 En el caso de los tipos de datos de valores grandes, el valor devuelto en *DataTypePtr* es SQL_VARCHAR, SQL_VARBINARY o SQL_NVARCHAR. Un valor de SQL_SS_LENGTH_UNLIMITED en *ColumnSizePtr* indica que el tamaño es "ilimitado".  
  
 Las mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permiten a SQLDescribeCol obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por SQLDescribeCol en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Detección de metadatos](../../relational-databases/native-client/features/metadata-discovery.md).  
  
## <a name="sqldescribecol-support-for-enhanced-date-and-time-features"></a>SQLDescribeCol admite las características mejoradas de fecha y hora  
 Los valores devueltos para los tipos de fecha y hora son los siguientes:  
  
| Atributo | *DataTypePtr* | *ColumnSizePtr* | *DecimalDigitsPtr* |  
| --------- | ------------- |---------------- | ------------------ |  
|datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|date|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribecol-support-for-large-clr-udts"></a>SQLDescribeCol admite tipos definidos por el usuario de CLR grandes  
 **SQLDescribeCol** admite tipos definidos por el usuario (UDT) CLR grandes. Para obtener más información, vea [tipos CLR grandes definidos por el usuario &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLDescribeCol función)](https://go.microsoft.com/fwlink/?LinkID=59338)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
