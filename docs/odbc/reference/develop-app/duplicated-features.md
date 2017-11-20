---
title: "Duplican características | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b12ba1b5b8c70e6ab0f7efe6f0811984411a6022
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="duplicated-features"></a>Características duplicados
Las siguientes 2 de ODBC. *x* funciones se han duplicado por ODBC 3. *x* funciones. Como resultado, la API ODBC 2. *x* funciones están desusadas en ODBC 3. *x*. ODBC 3. *x* funciones se conocen como funciones de reemplazo.  
  
 Cuando una aplicación usa un 2 de ODBC en desuso. *x* función y el controlador subyacente es una aplicación ODBC 3. *x* controlador, el Administrador de controladores asigna la llamada de función a la función de reemplazo correspondiente. La única excepción a esta regla es **SQLExtendedFetch**. (Vea la nota al pie al final de la tabla siguiente). Para obtener más información acerca de estas asignaciones, consulte [asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores.  
  
 Cuando una aplicación usa una función de reemplazo y el controlador subyacente es una API ODBC 2. *x* controlador, el Administrador de controladores asigna la llamada de función a la función en desuso correspondiente.  
  
|ODBC 2. *x* (función)|ODBC 3. *x* (función)|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] en la función **SQLExtendedFetch** funcionalidad duplicados; **SQLFetchScroll** proporciona la misma funcionalidad en ODBC 3. *x*. Sin embargo, el Administrador de controladores que no se asigna **SQLExtendedFetch** a **SQLFetchScroll** al ir en una aplicación ODBC 3. *x* controlador. Para obtener más información, consulte [lo que el Administrador de controladores hace](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) en Apéndice G: controlador directrices para la compatibilidad con versiones anteriores. Asigna el Administrador de controladores **SQLFetchScroll** a **SQLExtendedFetch** al ir en una API ODBC 2. *x* controlador.  
  
> [!NOTE]  
>  La función **SQLBindParam** es un caso especial. **SQLBindParam** funcionalidad duplicada. Esto no es una API ODBC 2*.x* función, pero las funciones que se encuentra en los estándares Open Group e ISO. La funcionalidad proporcionada por esta función es incluir completamente de **SQLBindParameter**. Como resultado, el Administrador de controladores se asigna una llamada a **SQLBindParam** a **SQLBindParameter** cuando el controlador subyacente es una aplicación ODBC 3. *x* controlador. Sin embargo, cuando el controlador subyacente es una API ODBC 2*.x* controlador, el Administrador de controladores no realiza esta asignación.

