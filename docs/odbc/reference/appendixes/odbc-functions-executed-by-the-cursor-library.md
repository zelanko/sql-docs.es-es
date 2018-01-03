---
title: Funciones ODBC ejecutadas por la biblioteca de cursores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursor library [ODBC], functions
- functions [ODBC], cursor library
- ODBC functions [ODBC], cursor library
- ODBC cursor library [ODBC], functions
ms.assetid: 2f1d3386-7e59-4d55-a5b4-3440b61343a3
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3fd744310a198057d3c6973873f9b34b61b2050a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="odbc-functions-executed-by-the-cursor-library"></a>Funciones ODBC ejecutadas por la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 La biblioteca de cursores ejecuta las siguientes funciones. Cuando una aplicación llama a una función en esta lista, el Administrador de controladores, se invoca la biblioteca de cursores, no el controlador. Tenga en cuenta que la biblioteca de cursores puede llamar a los controladores cuando se ejecuta la función.  
  
|||  
|-|-|  
|**SQLBindCol**|**SQLGetStmtOption**|  
|**SQLBindParam**|**SQLNativeSql**|  
|**SQLBindParameter**|**SQLNumParams**|  
|**SQLCloseCursor**|**SQLParamOptions**|  
|**SQLEndTran**|**SQLRowCount**|  
|**SQLExtendedFetch**|**SQLSetConnectAttr**|  
|**SQLFetchScroll**|**SQLSetConnectOption**|  
|**SQLFreeHandle**|**SQLSetDescField**|  
|**SQLFreeStmt**|**SQLSetDescRec**|  
|**SQLGetData**|**SQLSetPos**|  
|**SQLGetDescField**|**SQLSetScrollOptions**|  
|**SQLGetDescRec**|**SQLSetStmtAttr**|  
|**SQLGetFunctions**|**SQLSetStmtOption**|  
|**SQLGetInfo**|**SQLTransact**|  
|**SQLGetStmtAttr**||
