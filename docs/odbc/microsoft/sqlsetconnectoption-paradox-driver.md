---
title: SQLSetConnectOption (Paradox Driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLSetConnectOption
ms.assetid: 050ee2be-594e-4dbd-af67-8b6aae756cd1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fac808000fb2c1fba4993b8a9ee3639d702bb48
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305681"
---
# <a name="sqlsetconnectoption-paradox-driver"></a>SQLSetConnectOption (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Puede establecerse la fOption SQL_ACCESS_MODE SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no impide que las actualizaciones si SQL_ACCESS_MODE está establecido en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|El controlador de Paradox sólo admite SQL_AUTOCOMMIT está activado (el estado predeterminado), porque no admiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Compatible.|  
|SQL_LOGIN_TIMEOUT|No compatible.|  
|SQL_OPT_TRACE|Compatible.|  
|SQL_OPT_TRACEFILE|Compatible.|  
|SQL_PACKET_SIZE|No compatible.|  
|SQL_QUIET_MODE|No compatible.|  
|SQL_TRANSLATE_DLL|No compatible.|  
|SQL_TRANSLATION_OPTION|No compatible.|  
|SQL_TXN_ISOLATION|No compatible.|
