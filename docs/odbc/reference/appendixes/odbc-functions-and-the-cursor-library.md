---
title: Funciones ODBC y la Biblioteca de cursores ( Cursor Library) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c609d0fb-787a-4b39-9673-332d411b3d63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8293e9bc952fc1dffc5a8f796f5a066b91ae811
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304346"
---
# <a name="odbc-functions-and-the-cursor-library"></a>Funciones ODBC y biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 Cuando la biblioteca de cursores ODBC está habilitada para una conexión, el Administrador de controladores llama a funciones en la biblioteca de cursores en lugar de en el controlador. La biblioteca de cursores ejecuta la función o la llama en el controlador especificado.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Funciones ODBC ejecutadas por la biblioteca de cursores](../../../odbc/reference/appendixes/odbc-functions-executed-by-the-cursor-library.md)  
  
-   [Funciones ODBC no ejecutadas por la biblioteca de cursores](../../../odbc/reference/appendixes/odbc-functions-not-executed-by-the-cursor-library.md)  
  
-   [SQLBindCol (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlbindcol-cursor-library.md)  
  
-   [SQLBindParameter (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlbindparameter-cursor-library.md)  
  
-   [SQLBulkOperations (Biblioteca de cursores)](../../../odbc/reference/appendixes/sqlbulkoperations-and-the-cursor-library.md)  
  
-   [SQLCloseCursor (Biblioteca de cursores)](../../../odbc/reference/appendixes/sqlclosecursor-odbc.md)  
  
-   [SQLEndTran (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlendtran-cursor-library.md)  
  
-   [SQLExtendedFetch (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlextendedfetch-cursor-library.md)  
  
-   [SQLFetch (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlfetch-cursor-library.md)  
  
-   [SQLFetchScroll (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlfetchscroll-cursor-library.md)  
  
-   [SQLFreeStmt (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlfreestmt-cursor-library.md)  
  
-   [SQLGetData (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlgetdata-cursor-library.md)  
  
-   [SQLGetDescField y SQLGetDescRec (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlgetdescfield-and-sqlgetdescrec-cursor-library.md)  
  
-   [SQLGetFunctions (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlgetfunctions-cursor-library.md)  
  
-   [SQLGetInfo (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlgetinfo-cursor-library.md)  
  
-   [SQLGetStmtAttr (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlgetstmtattr-cursor-library.md)  
  
-   [SQLGetStmtOption (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlgetstmtoption-cursor-library.md)  
  
-   [SQLNativeSql (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlnativesql-cursor-library.md)  
  
-   [SQLRowCount (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlrowcount-cursor-library.md)  
  
-   [SQLSetConnectAttr (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlsetconnectattr-cursor-library.md)  
  
-   [SQLSetDescField y SQLSetDescRec (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlsetdescfield-and-sqlsetdescrec-cursor-library.md)  
  
-   [SQLSetEnvAttr (Biblioteca de cursores)](../../../odbc/reference/appendixes/sqlsetenvattr-and-the-cursor-library.md)  
  
-   [SQLSetPos (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlsetpos-cursor-library.md)  
  
-   [SQLSetScrollOptions (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlsetscrolloptions-cursor-library.md)  
  
-   [SQLSetStmtAttr (biblioteca de cursores)](../../../odbc/reference/appendixes/sqlsetstmtattr-cursor-library.md)
