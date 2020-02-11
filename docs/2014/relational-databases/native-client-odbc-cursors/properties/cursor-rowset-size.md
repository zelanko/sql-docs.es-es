---
title: Tamaño del conjunto de filas cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bff145e7e3c6e429ca0877c81c5188b02e428809
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63207167"
---
# <a name="cursor-rowset-size"></a>Tamaño del conjunto de filas del cursor
  Los cursores ODBC no están limitados a capturar una fila cada vez. Pueden recuperar varias filas en cada llamada a **SQLFetch** o [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md). Cuando se trabaja con una base de datos cliente/servidor, como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de Microsoft, resulta más eficaz capturar varias filas a la vez. El número de filas devueltas en una captura se denomina tamaño del conjunto de filas y se especifica mediante el SQL_ATTR_ROW_ARRAY_SIZE de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md).  
  
```  
SQLUINTEGER uwRowsize;  
SQLSetStmtAttr(m_hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)uwRowsetSize, SQL_IS_UINTEGER);  
```  
  
 Los cursores con un tamaño del conjunto de filas mayor que 1 reciben el nombre de cursores de bloque.  
  
 Hay dos opciones para enlazar las columnas de conjunto de resultados para los cursores de bloque:  
  
-   Enlace de modo de columna  
  
     Cada columna se enlaza a una matriz de variables. Cada matriz tiene el mismo número de elementos que el tamaño del conjunto de filas.  
  
-   Enlace de modo de fila  
  
     Una matriz se genera mediante estructuras que contienen los datos e indicadores para todas las columnas de una fila. La matriz tiene el mismo número de estructuras que el tamaño del conjunto de filas.  
  
 Cuando se usa un enlace de modo de columna o de modo de fila, cada llamada a **SQLFetch** o **SQLFetchScroll** rellena las matrices enlazadas con los datos del conjunto de filas recuperado.  
  
 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) también se puede usar para recuperar datos de columna de un cursor de bloque. Dado que **SQLGetData** funciona una fila cada vez, se debe llamar a **SQLSetPos** para establecer una fila específica del conjunto de filas como la fila actual antes de llamar a **SQLGetData**.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client ofrece una optimización mediante conjuntos de filas para recuperar rápidamente un conjunto de resultados completo. Para usar esta optimización, establezca los atributos de cursor en sus valores predeterminados (solo avance, solo lectura, tamaño del conjunto de filas = 1) en el momento en que se llama a **SQLExecDirect** o **SQLExecute** . El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client configura un conjunto de resultados predeterminado. Esto es más eficaz que los cursores de servidor al transferir los resultados al cliente sin desplazarse. Después de ejecutar la instrucción, aumente el tamaño del conjunto de filas y use el enlace de modo de columna o de modo de fila. Esto permite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usar un conjunto de resultados predeterminado para enviar filas de resultados de forma eficaz al cliente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mientras que el controlador ODBC de Native Client extrae continuamente filas de los búferes de red en el cliente.  
  
## <a name="see-also"></a>Consulte también  
 [Propiedades de cursor](cursor-properties.md)  
  
  
