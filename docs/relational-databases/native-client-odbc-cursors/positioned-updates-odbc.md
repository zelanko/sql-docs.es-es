---
title: Actualizaciones posicionadas (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- SQLSetPos function
- SQLSetCursorName function
- ODBC applications, cursors
- cursors [ODBC], positioned updates
- positioned updates [ODBC]
- ODBC cursors, positioned updates
ms.assetid: ff404e02-630f-474d-b5d4-06442b756991
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1424d4e7ff08cee6dea1e53dfac0e5cf231ea266
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73784388"
---
# <a name="positioned-updates-odbc"></a>Actualizaciones por posición (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC admite dos métodos para realizar actualizaciones por posición en un cursor:  
  
-   **SQLSetPos**  
  
-   Cláusula WHERE CURRENT OF  
  
 El enfoque más común consiste en usar **SQLSetPos**. Tiene las opciones siguientes.  
  
 SQL_POSITION  
 Sitúa el cursor en una fila específica del conjunto de filas actual.  
  
 SQL_REFRESH  
 Actualiza las variables de programa enlazadas a las columnas del conjunto de resultados mediante los valores de la fila en la que está situado el cursor actualmente.  
  
 SQL_UPDATE  
 Actualiza la fila actual del cursor mediante los valores almacenados en las variables de programa que están enlazadas a las columnas del conjunto de resultados.  
  
 SQL_DELETE  
 Elimina la fila actual del cursor.  
  
 **SQLSetPos** se puede usar con cualquier conjunto de resultados de instrucciones cuando la instrucción que controla los atributos de cursor está establecida para usar cursores de servidor. Las columnas del conjunto de resultados deben estar enlazadas a variables de programa. En cuanto la aplicación ha capturado una fila, llama a **SQLSetPos**(SQL_POSTION) para colocar el cursor en la fila. A continuación, la aplicación podría llamar a SQLSetPos(SQL_DELETE) para eliminar la fila actual, o puede mover los nuevos valores de datos a las variables de programa enlazadas y llamar a SQLSetPos(SQL_UPDATE) para actualizar la fila actual.  
  
 Las aplicaciones pueden actualizar o eliminar cualquier fila del conjunto de filas con **SQLSetPos**. Llamar a **SQLSetPos** es una alternativa práctica para construir y ejecutar una instrucción SQL. **SQLSetPos** funciona en el conjunto de filas actual y solo se puede usar después de una llamada a [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
 El tamaño del conjunto de filas se establece mediante una llamada a [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) con un argumento de atributo de SQL_ATTR_ROW_ARRAY_SIZE. **SQLSetPos** usa un nuevo tamaño de conjunto de filas, pero solo después de una llamada a **SQLFetch** o **SQLFetchScroll**. Por ejemplo, si se cambia el tamaño del conjunto de filas, se llama a **SQLSetPos** y luego se llama a **SQLFetch** o **SQLFetchScroll** . La llamada a **SQLSetPos** utiliza el tamaño del conjunto de filas anterior, pero **SQLFetch** o **SQLFetchScroll** usa el nuevo tamaño del conjunto de filas.  
  
 La primera fila del conjunto de filas es el número de fila 1. El argumento RowNumber de **SQLSetPos** debe identificar una fila del conjunto de filas; es decir, su valor debe estar en el intervalo comprendido entre 1 y el número de filas que se capturaron más recientemente. Esto valor puede ser menor que el tamaño del conjunto de filas. Si RowNumber es 0, la operación se aplica a cada fila del conjunto de filas.  
  
 La operación de eliminación de **SQLSetPos** hace que el origen de datos elimine una o varias filas seleccionadas de una tabla. Para eliminar filas con **SQLSetPos**, la aplicación llama a **SQLSetPos** con la operación establecida en SQL_DELETE y RowNumber establecida en el número de la fila que se va a eliminar. Si RowNumber es 0, se eliminan todas las filas del conjunto de filas.  
  
 Una vez que **SQLSetPos** devuelve, la fila eliminada es la fila actual y su estado es SQL_ROW_DELETED. La fila no se puede usar en ninguna operación posicionada adicional, como las llamadas a [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) o **SQLSetPos**.  
  
 Cuando se eliminan todas las filas del conjunto de filas (RowNumber es igual a 0), la aplicación puede evitar que el controlador elimine determinadas filas mediante el uso de la matriz de operaciones de filas igual que en el caso de la operación de actualización de **SQLSetPos**.  
  
 Cada fila que se elimina debe ser una fila que exista en el conjunto de resultados. Si los búferes de la aplicación se rellenaron con los valores capturados, y si se ha mantenido una matriz de estado de fila, sus valores en cada una de estas posiciones de fila no deben ser SQL_ROW_DELETED, SQL_ROW_ERROR ni SQL_ROW_NOROW.  
  
 Las actualizaciones por posición también se pueden realizar utilizando la cláusula WHERE CURRENT OF en instrucciones UPDATE, DELETE e INSERT. DONDE CURRENT OF requiere un nombre de cursor que ODBC generará cuando se llame a la función [SQLGetCursorName](../../relational-databases/native-client-odbc-api/sqlgetcursorname.md) , o que se puede especificar llamando a **SQLSetCursorName**. A continuación, se incluyen los pasos generales utilizados para ejecutar una actualización WHERE CURRENT OF en una aplicación ODBC:  
  
-   Llame a **SQLSetCursorName** para establecer un nombre de cursor para el identificador de instrucción.  
  
-   Genere una instrucción SELECT con una cláusula FOR UPDATE OF y ejecútela.  
  
-   Llame a **SQLFetchScroll** para recuperar un conjunto de filas o **SQLFetch** para recuperar una fila.  
  
-   Llame a **SQLSetPos** (SQL_POSITION) para colocar el cursor en la fila.  
  
-   Compile y ejecute una instrucción UPDATE con la cláusula WHERE CURRENT OF con el nombre de cursor establecido con **SQLSetCursorName**.  
  
 Como alternativa, puede llamar a **SQLGetCursorName** después de ejecutar la instrucción SELECT en lugar de llamar a **SQLSetCursorName** antes de ejecutar la instrucción SELECT. **SQLGetCursorName** devuelve un nombre de cursor predeterminado asignado por ODBC si no se establece un nombre de cursor mediante **SQLSetCursorName**.  
  
 Se prefiere **SQLSetPos** en lugar de cuando se utilizan cursores de servidor. Si utiliza un cursor estático actualizable con la biblioteca de cursores ODBC, la biblioteca de cursores implementa las actualizaciones WHERE CURRENT OF agregando una cláusula WHERE con los valores de clave de la tabla subyacente. Esto puede dar lugar a actualizaciones no deseadas si las claves de la tabla no son únicas.  
  
## <a name="see-also"></a>Consulte también  
 [Usar cursores &#40;&#41;ODBC](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
