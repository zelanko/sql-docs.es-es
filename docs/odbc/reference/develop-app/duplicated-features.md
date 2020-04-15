---
title: Características duplicadas ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00f5529cfbfacebcad78a0a4433e84f34034694a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300485"
---
# <a name="duplicated-features"></a>Características duplicados
Las siguientes funciones ODBC *2.x* se han duplicado mediante funciones ODBC *3.x.* Como resultado, las funciones ODBC *2.x* están en desuso en ODBC *3.x*. Las funciones ODBC *3.x* se conocen como funciones de reemplazo.  
  
 Cuando una aplicación utiliza una función ODBC *2.x* en desuso y el controlador subyacente es un controlador ODBC *3.x,* el Administrador de controladores asigna la llamada de función a la función de reemplazo correspondiente. La única excepción a esta regla es **SQLExtendedFetch**. (Véase la nota al pie al final de la tabla siguiente.) Para obtener más información acerca de estas asignaciones, consulte Asignación de [funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) en el Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
 Cuando una aplicación utiliza una función de reemplazo y el controlador subyacente es un controlador ODBC *2.x,* el Administrador de controladores asigna la llamada de función a la función en desuso correspondiente.  
  
|Función ODBC *2.x*|Función ODBC *3.x*|  
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
  
 [1] La función **SQLExtendedFetch** es funcionalidad duplicada; **SQLFetchScroll** proporciona la misma funcionalidad en ODBC *3.x*. Sin embargo, el Administrador de controladores no asigna **SQLExtendedFetch** a **SQLFetchScroll** cuando se va en un controlador ODBC *3.x.* Para obtener más información, consulte Qué hace el Administrador de [controladores](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) en el Apéndice G: Directrices del controlador para la compatibilidad con versiones anteriores. El Administrador de controladores asigna **SQLFetchScroll** a **SQLExtendedFetch** cuando se va a un controlador ODBC *2.x.*  
  
> [!NOTE]
>  La función **SQLBindParam** es un caso especial. **SQLBindParam** es una funcionalidad duplicada. No se trata de una función ODBC *2.x,* sino de una función que está presente en las normas Open Group e ISO. La funcionalidad proporcionada por esta función está completamente subsumida por la de **SQLBindParameter**. Como resultado, el Administrador de controladores asigna una llamada a **SQLBindParam** a **SQLBindParameter** cuando el controlador subyacente es un controlador ODBC *3.x.* Sin embargo, cuando el controlador subyacente es un controlador ODBC *2.x,* el Administrador de controladores no realiza esta asignación.
