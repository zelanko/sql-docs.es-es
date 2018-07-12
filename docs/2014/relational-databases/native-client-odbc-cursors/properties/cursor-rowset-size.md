---
title: Tamaño del conjunto de filas del cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c683ec4cf8b7fd430e9bddd0d126cc132880975f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37412309"
---
# <a name="cursor-rowset-size"></a>Tamaño del conjunto de filas del cursor
  Los cursores ODBC no están limitados a capturar una fila cada vez. Pueden recuperar varias filas en cada llamada a **SQLFetch** o [SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md). Cuando se trabaja con una base de datos cliente/servidor, como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de Microsoft, resulta más eficaz capturar varias filas a la vez. El número de filas devueltas en una operación de captura se denomina el tamaño del conjunto de filas y se especifica mediante el SQL_ATTR_ROW_ARRAY_SIZE de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md).  
  
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
  
 Cuando se usa el enlace de columna o fila, cada llamada a **SQLFetch** o **SQLFetchScroll** rellena las matrices enlazadas con datos desde el conjunto de filas recuperada.  
  
 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) también puede usarse para recuperar datos de la columna de un cursor de bloque. Dado que **SQLGetData** funciona una fila a la vez, **SQLSetPos** debe llamarse para establecer una fila específica en el conjunto de filas como la fila actual antes de llamar a **SQLGetData**.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client proporciona una optimización mediante conjuntos de filas para recuperar un conjunto completo de resultados rápidamente. Para usar esta optimización, establezca los atributos de cursor en sus valores predeterminados (tamaño del conjunto de filas de solo avance y solo lectura = 1) en el momento **SQLExecDirect** o **SQLExecute** se llama. El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client configura un conjunto de resultados predeterminado. Esto es más eficaz que los cursores de servidor al transferir los resultados al cliente sin desplazarse. Después de ejecutar la instrucción, aumente el tamaño del conjunto de filas y use el enlace de modo de columna o de modo de fila. Esto permite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use un resultado predeterminado establecido en enviar de forma eficaz las filas de resultados al cliente, mientras que el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client extrae continuamente filas de los búferes de red en el cliente.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de cursor](cursor-properties.md)  
  
  
