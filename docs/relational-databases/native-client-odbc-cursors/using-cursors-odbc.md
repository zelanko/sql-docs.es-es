---
title: Uso de cursores (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC cursors, about ODBC cursors
- ODBC applications, cursors
- cursors [ODBC]
- ODBC cursors
ms.assetid: 51322f92-0d76-44c9-9c33-9223676cf1d3
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4955949e513b61ac46c335c2785b76d52d8eb8e8
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427694"
---
# <a name="using-cursors-odbc"></a>Uso de cursores (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  ODBC admite un modelo de cursor que permite:  
  
-   Varios tipos de cursores.  
  
-   Desplazamiento y colocación en un cursor.  
  
-   Varias opciones de simultaneidad.  
  
-   Actualizaciones posicionadas.  
  
 Las aplicaciones ODBC raramente declaran y abren cursores o utilizan cualquier instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionada con cursores. ODBC abre automáticamente un cursor para cada conjunto de resultados que devuelve una instrucción SQL. Las características de los cursores se controlan mediante atributos de instrucción establecidos con [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md) antes de la instrucción SQL se ejecuta la instrucción. Las funciones de la API de ODBC para procesar conjuntos de resultados admiten toda la funcionalidad del cursor, entre la que se incluye la captura, el desplazamiento y las actualizaciones posicionadas.  
  
 A continuación se ofrece una comparación de cómo los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] y las aplicaciones ODBC trabajan con cursores.  
  
|Acción|[!INCLUDE[tsql](../../includes/tsql-md.md)]|ODBC|  
|------------|------------------------|----------|  
|Definir el comportamiento del cursor|Se especifica a través de parámetros DECLARE CURSOR|Establecer atributos de cursor mediante [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)|  
|Abrir un cursor|DECLARE CURSOR OPEN *cursor_name*|**SQLExecDirect** o **SQLExecute**|  
|Capturar filas|FETCH|**SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)|  
|Actualización posicionada|Cláusula WHERE CURRENT OF en UPDATE o DELETE|**SQLSetPos**|  
|Cerrar un cursor|CERRAR *cursor_name* DEALLOCATE|[SQLCloseCursor](../../relational-databases/native-client-odbc-api/sqlclosecursor.md)|  
  
 Los cursores de servidor implementados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten la funcionalidad del modelo de cursores de ODBC. El controlador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client utiliza cursores de servidor para admitir la funcionalidad de cursor de la API de ODBC.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Cómo se implementan los cursores](../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
-   [Tipos de cursor](../../relational-databases/native-client-odbc-cursors/cursor-types.md)  
  
-   [Comportamientos de los cursores](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
-   [Propiedades de cursor](../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
-   [Detalles de programación de cursores &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/programming/cursor-programming-details-odbc.md)  
  
-   [Desplazamiento y captura de filas](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
-   [Las actualizaciones posicionadas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/positioned-updates-odbc.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)  
  
  
