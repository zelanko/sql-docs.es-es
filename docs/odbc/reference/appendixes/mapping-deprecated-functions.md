---
title: Asignación de funciones en desuso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b59d2604dd9d4b7c3166027c1917dea096b331d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818377"
---
# <a name="mapping-deprecated-functions"></a>Asignación de funciones en desuso
Esta sección describen las funciones en desuso de cómo se asignan por el ODBC 3 *.x* Administrador de controladores para garantizar la compatibilidad con versiones anteriores de ODBC 3 *.x* controladores que se usan con ODBC 2. *x* aplicaciones. El Administrador de controladores se realiza esta asignación independientemente de la versión de la aplicación. Dado que cada uno de ODBC 2. *x* funciones en la lista siguiente se asigna a la correspondiente ODBC 3 *.x* funcionar cuando se llama en una aplicación ODBC 3 *.x* controlador, el 3 de ODBC *.x*controlador no tiene que implementar el 2 de ODBC. *x* funciones.  
  
 La asignación en la lista se desencadena cuando el controlador es una aplicación ODBC 3 *.x* controlador y el controlador no admite la función que se está asignando.  
  
 En la tabla siguiente se enumera todos los duplicados funcionalidad que se introdujo en ODBC 3 *.x*.  
  
|ODBC 2. *x* (función)|ODBC 3 *.x* (función)|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** con un *opción* de SQL_DROP|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1], aunque esta función no existía en ODBC 2 *.x*, se encuentra en los estándares de Open Group e ISO.  
  
 [2] se trata de una función ODBC 1.0.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignación de SQLAllocConnect](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [Asignación de SQLAllocEnv](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [Asignación de SQLAllocStmt](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [Asignación de SQLBindParam](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [Asignación de SQLColAttributes](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [Asignación de SQLError](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [Asignación de SQLFreeConnect](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [Asignación de SQLFreeEnv](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [Asignación de SQLFreeStmt](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [Asignación de SQLGetConnectOption](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [Asignación de SQLGetStmtOption](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [Asignación de SQLInstallTranslator](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [Asignación de SQLParamOptions](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [Asignación de SQLSetConnectOption](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [Asignación de SQLSetParam](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [Asignación de SQLSetScrollOptions](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [Asignación de SQLSetStmtOption](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [Asignación de SQLTransact](../../../odbc/reference/appendixes/sqltransact-mapping.md)
