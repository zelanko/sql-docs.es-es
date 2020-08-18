---
description: Características duplicados
title: Características duplicadas | Microsoft Docs
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
ms.openlocfilehash: 0aa03482efbadc8dac2fa887deb0f01d9b167214
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483028"
---
# <a name="duplicated-features"></a>Características duplicados
Las funciones ODBC *2.* x siguientes se han duplicado con las funciones ODBC *3. x* . Como resultado, las funciones ODBC *2. x* están en desuso en ODBC *3. x*. Las funciones ODBC *3. x* se conocen como funciones de reemplazo.  
  
 Cuando una aplicación utiliza una función ODBC *2. x* desusada y el controlador subyacente es un controlador ODBC *3. x* , el administrador de controladores asigna la llamada de función a la función de reemplazo correspondiente. La única excepción a esta regla es **SQLExtendedFetch**. (Vea la nota al final de la tabla siguiente). Para obtener más información acerca de estas asignaciones, consulte [asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) en el Apéndice G: instrucciones de controlador para la compatibilidad con versiones anteriores.  
  
 Cuando una aplicación utiliza una función de reemplazo y el controlador subyacente es un controlador ODBC *2. x* , el administrador de controladores asigna la llamada de función a la función desusada correspondiente.  
  
|ODBC *2. x* (función)|ODBC *3. x* (función)|  
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
  
 [1] la función **SQLExtendedFetch** es una funcionalidad duplicada; **SQLFetchScroll** proporciona la misma funcionalidad en ODBC *3. x*. Sin embargo, el administrador de controladores no asigna **SQLExtendedFetch** a **SQLFetchScroll** al pasar a un controlador ODBC *3. x* . Para obtener más información, consulte [lo que hace el administrador de controladores en el](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) Apéndice G: instrucciones del controlador para la compatibilidad con versiones anteriores. El administrador de controladores asigna **SQLFetchScroll** a **SQLExtendedFetch** al pasar a un controlador ODBC *2. x* .  
  
> [!NOTE]
>  La función **SQLBindParam** es un caso especial. **SQLBindParam** es una funcionalidad duplicada. Esta no es una función ODBC *2. x* , sino una función que está presente en los estándares Open Group e ISO. La funcionalidad proporcionada por esta función está totalmente incluida en la de **SQLBindParameter**. Como resultado, el administrador de controladores asigna una llamada a **SQLBindParam** a **SQLBindParameter** cuando el controlador subyacente es un controlador ODBC *3. x* . Sin embargo, cuando el controlador subyacente es un controlador ODBC *2. x* , el administrador de controladores no realiza esta asignación.
