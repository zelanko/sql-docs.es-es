---
title: Tamaño del conjunto de filas del cursor | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], rowset size
- ODBC cursors, rowset size
- rowsets [ODBC]
ms.assetid: 2febe2ae-fdc1-490e-a79f-c516bc8e7c3f
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bec0b6eb7f85c5dc11c1e590d809ba0a32079fe2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104229"
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
  
 Cuando se usa el enlace de modo de columna o fila, cada llamada a **SQLFetch** o **SQLFetchScroll** rellena las matrices enlazadas con datos del conjunto de filas recuperado.  
  
 [SQLGetData](../../native-client-odbc-api/sqlgetdata.md) también puede usarse para recuperar datos de la columna de un cursor de bloque. Dado que **SQLGetData** funciona una fila a la vez, **SQLSetPos** debe llamarse para establecer una fila específica en el conjunto de filas como la fila actual antes de llamar a **SQLGetData**.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client proporciona una optimización mediante conjuntos de filas para recuperar un conjunto completo de resultados establecer rápidamente. Para usar esta optimización, establezca los atributos de cursor en sus valores predeterminados (conjunto de filas de solo avance y solo lectura, tamaño = 1) en el momento de **SQLExecDirect** o **SQLExecute** se llama. El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client configura un conjunto de resultados predeterminado. Esto es más eficaz que los cursores de servidor al transferir los resultados al cliente sin desplazarse. Después de ejecutar la instrucción, aumente el tamaño del conjunto de filas y use el enlace de modo de columna o de modo de fila. Esto permite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use un resultado predeterminado establecido para enviar filas de resultados de forma eficaz al cliente, mientras que la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client extrae continuamente filas de los búferes de red en el cliente.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de cursor](cursor-properties.md)  
  
  