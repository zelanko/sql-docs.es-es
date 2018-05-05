---
title: SQLSetConnectOption (controlador de Paradox) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLSetConnectOption
ms.assetid: 050ee2be-594e-4dbd-af67-8b6aae756cd1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8a4edef9b5c4f48a3abba39962978a9e38a008ff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconnectoption-paradox-driver"></a>SQLSetConnectOption (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador Paradox. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|El fOption SQL_ACCESS_MODE puede establecerse en SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no evita que las actualizaciones si SQL_ACCESS_MODE se establece en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|El controlador de Paradox sólo admite SQL_AUTOCOMMIT está activada (el estado predeterminado), ya que no admiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Compatible.|  
|SQL_LOGIN_TIMEOUT|No compatible.|  
|SQL_OPT_TRACE|Compatible.|  
|SQL_OPT_TRACEFILE|Compatible.|  
|SQL_PACKET_SIZE|No compatible.|  
|SQL_QUIET_MODE|No compatible.|  
|SQL_TRANSLATE_DLL|No compatible.|  
|SQL_TRANSLATION_OPTION|No compatible.|  
|SQL_TXN_ISOLATION|No compatible.|
