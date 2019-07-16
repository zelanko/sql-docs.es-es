---
title: Uso de cursores (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc53253c93f5f52c6bbe00941eadbf14b65d5f64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206821"
---
# <a name="using-cursors-odbc"></a>Usar cursores (ODBC)
  ODBC admite un modelo de cursor que permite:  
  
-   Varios tipos de cursores.  
  
-   Desplazamiento y colocación en un cursor.  
  
-   Varias opciones de simultaneidad.  
  
-   Actualizaciones posicionadas.  
  
 Las aplicaciones ODBC raramente declaran y abren cursores o utilizan cualquier instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionada con cursores. ODBC abre automáticamente un cursor para cada conjunto de resultados que devuelve una instrucción SQL. Las características de los cursores se controlan mediante atributos de instrucción establecidos con [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md) antes de la instrucción SQL se ejecuta la instrucción. Las funciones de la API de ODBC para procesar conjuntos de resultados admiten toda la funcionalidad del cursor, entre la que se incluye la captura, el desplazamiento y las actualizaciones posicionadas.  
  
 A continuación se ofrece una comparación de cómo los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] y las aplicaciones ODBC trabajan con cursores.  
  
|.|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|Definir el comportamiento del cursor|Se especifica a través de parámetros DECLARE CURSOR|Establecer atributos de cursor mediante [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)|  
|Abrir un cursor|DECLARE CURSOR OPEN *cursor_name*|**SQLExecDirect** o **SQLExecute**|  
|Capturar filas|FETCH|**SQLFetch** o [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)|  
|Actualización posicionada|Cláusula WHERE CURRENT OF en UPDATE o DELETE|**SQLSetPos**|  
|Cerrar un cursor|CERRAR *cursor_name* DEALLOCATE|[SQLCloseCursor](../native-client-odbc-api/sqlclosecursor.md)|  
  
 Los cursores de servidor implementados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten la funcionalidad del modelo de cursores de ODBC. El controlador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client utiliza cursores de servidor para admitir la funcionalidad de cursor de la API de ODBC.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Cómo se implementan los cursores](implementation/how-cursors-are-implemented.md)  
  
-   [Tipos de cursor](cursor-types.md)  
  
-   [Comportamientos de los cursores](cursor-behaviors.md)  
  
-   [Propiedades de cursor](properties/cursor-properties.md)  
  
-   [Detalles de programación de cursores &#40;ODBC&#41;](programming/cursor-programming-details-odbc.md)  
  
-   [Desplazamiento y captura de filas](../native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [Las actualizaciones posicionadas &#40;ODBC&#41;](positioned-updates-odbc.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [CLOSE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/close-transact-sql)   
 [Cursores](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/deallocate-transact-sql)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-cursor-transact-sql)   
 [FETCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/fetch-transact-sql)   
 [OPEN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/open-transact-sql)  
  
  
