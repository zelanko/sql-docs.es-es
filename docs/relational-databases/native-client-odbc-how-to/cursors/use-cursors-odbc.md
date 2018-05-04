---
title: Usar cursores (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], how to topics
ms.assetid: c502736f-bca0-45c3-ae25-d2ad52d296bf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5091bb34efb441ee7350765d3f5e9d7da51f0ea2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="use-cursors-odbc"></a>Usar cursores (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
### <a name="to-use-cursors"></a>Para usar cursores  
  
1.  Llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para establecer los atributos de cursor deseados:  
  
     Establezca los atributos SQL_ATTR_CURSOR_TYPE y SQL_ATTR_CONCURRENCY (ésta es la opción preferida).  
  
     O bien  
  
     Establezca los atributos SQL_CURSOR_SCROLLABLE y SQL_CURSOR_SENSITIVITY.  
  
2.  Llame a [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) para establecer el tamaño del conjunto de filas mediante el atributo SQL_ATTR_ROW_ARRAY_SIZE.  
  
3.  Opcionalmente, llame a [SQLSetCursorName](http://go.microsoft.com/fwlink/?LinkId=58406) para establecer un nombre de cursor si las actualizaciones posicionadas se van a hacer mediante la cláusula de WHERE CURRENT OF.  
  
4.  Ejecute la instrucción SQL.  
  
5.  Opcionalmente, llame a [SQLGetCursorName](../../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) para obtener el nombre de cursor si las actualizaciones posicionadas se van a hacer mediante la cláusula WHERE ACTUAL OF y un nombre de cursor no se ha proporcionado con [SQLSetCursorName](http://go.microsoft.com/fwlink/?LinkId=58406) en el paso 3.  
  
6.  Llame a [SQLNumResultCols](../../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) para obtener el número de columnas (C) en el conjunto de filas.  
  
     Use el enlace de modo de columna.  
  
     \- O bien  
  
     Use el enlace de modo de fila.  
  
7.  Capture los conjuntos de filas del cursor según sea necesario.  
  
8.  Llame a [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) para determinar si otro conjunto de resultados está disponible.  
  
    -   Si devuelve SQL_SUCCESS, está disponible otro conjunto de resultados.  
  
    -   Si devuelve SQL_NO_DATA, no hay ningún otro conjunto de resultados disponible.  
  
    -   Si devuelve SQL_SUCCESS_WITH_INFO o SQL_ERROR, llame a [SQLGetDiagRec](http://go.microsoft.com/fwlink/?LinkId=58402) para determinar si está disponible la salida de una instrucción PRINT o RAISERROR.  
  
     Si se utilizan parámetros de instrucción enlazados como parámetros de salida o como valor devuelto de un procedimiento almacenado, utilice los datos ahora disponibles en los búferes de parámetros enlazados.  
  
     Si se usan parámetros enlazados, cada llamada a [SQLExecute](http://go.microsoft.com/fwlink/?LinkId=58400) o [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399) habrá ejecutado la instrucción SQL S veces, donde S es el número de elementos en la matriz de parámetros enlazados. Esto significa que habrá S conjuntos de resultados para procesar, donde cada conjunto de resultados comprende todos los conjuntos de resultados, parámetros de salida y códigos de retorno devueltos normalmente por una ejecución única de la instrucción SQL.  
  
     Tenga en cuenta que cuando un conjunto de resultados contiene filas del cálculo, cada fila del cálculo está disponible como un conjunto de resultados independiente. Estos conjuntos de resultados de cálculo se intercalan entre las filas normales e interrumpen las filas normales en varios conjuntos de resultados.  
  
9. Opcionalmente, llame a [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con SQL_UNBIND para liberar los búferes de columna enlazada.  
  
10. Si está disponible otro conjunto de resultados, vaya al paso 6.  
  
     En el paso 9, al llamar a [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) en un conjunto de resultados procesados parcialmente se borra el resto del conjunto de resultados. Otra manera de borrar un conjunto de resultados procesados parcialmente es llamar a [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md).  
  
     Puede controlar el tipo de cursor usado estableciendo SQL_ATTR_CURSOR_TYPE y SQL_ATTR_CONCURRENCY o estableciendo SQL_ATTR_CURSOR_SENSITIVITY y SQL_ATTR_CURSOR_SCROLLABLE. No debe mezclar los dos métodos que se utilizan para especificar el comportamiento del cursor.  
  
## <a name="see-also"></a>Vea también  
 [Uso de los temas de procedimientos de los cursores & #40; ODBC & #41;](../../../relational-databases/native-client-odbc-how-to/cursors/using-cursors-how-to-topics-odbc.md)  
  
  
