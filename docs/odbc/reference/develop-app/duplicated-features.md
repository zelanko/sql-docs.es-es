---
title: Duplicar las características | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84752b7e23c5394757764bf5ade57cb54004b01a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62943151"
---
# <a name="duplicated-features"></a>Características duplicados
Las siguientes 2 de ODBC. *x* funciones se han duplicado en ODBC 3. *x* funciones. Como resultado, el 2 de ODBC. *x* funciones están en desuso en ODBC 3. *x*. ODBC 3. *x* funciones se conocen como funciones de reemplazo.  
  
 Cuando una aplicación usa un 2 de ODBC en desuso. *x* función y el controlador subyacente es una aplicación ODBC 3. *x* controlador, la llamada de función a la función de reemplazo correspondiente se asigna el Administrador de controladores. La única excepción a esta regla es **SQLExtendedFetch**. (Vea la nota al pie al final de la tabla siguiente). Para obtener más información acerca de estas asignaciones, vea [asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
 Cuando una aplicación usa una función de reemplazo y el controlador subyacente es un ODBC 2. *x* controlador, la llamada de función a la función en desuso correspondiente se asigna el Administrador de controladores.  
  
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
  
 [1] en la función **SQLExtendedFetch** es una funcionalidad duplicada; **SQLFetchScroll** proporciona la misma funcionalidad en ODBC 3. *x*. Sin embargo, el Administrador de controladores que no se asigna **SQLExtendedFetch** a **SQLFetchScroll** cuando va contra una aplicación ODBC 3. *x* controlador. Para obtener más información, consulte [lo que el Administrador de controladores hace](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores. Asigna el Administrador de controladores **SQLFetchScroll** a **SQLExtendedFetch** cuando va contra un ODBC 2. *x* controlador.  
  
> [!NOTE]
>  La función **SQLBindParam** es un caso especial. **SQLBindParam** es una funcionalidad duplicada. Esto no es un 2 de ODBC *.x* función, pero una función que está presente en los estándares de Open Group e ISO. La funcionalidad proporcionada por esta función es incluir completamente de **SQLBindParameter**. Como resultado, el Administrador de controladores se asigna una llamada a **SQLBindParam** a **SQLBindParameter** cuando el controlador subyacente es una aplicación ODBC 3. *x* controlador. Sin embargo, cuando el controlador subyacente es un ODBC 2 *.x* controlador, el Administrador de controladores no realiza esta asignación.
