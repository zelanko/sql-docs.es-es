---
title: SQLSetConnectOption (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Text File Driver
- text file driver [ODBC], SQLSetConnectOption
ms.assetid: b631a20c-2f60-4102-a61d-93b8780a4620
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32c4a0219b049ee66a38d6c7c10295245dd48ebc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905482"
---
# <a name="sqlsetconnectoption-text-file-driver"></a>SQLSetConnectOption (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Puede establecerse la fOption SQL_ACCESS_MODE SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no impide que las actualizaciones si SQL_ACCESS_MODE está establecido en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|El controlador de texto sólo admite SQL_AUTOCOMMIT está activado (el estado predeterminado), porque no admiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Se admite.|  
|SQL_LOGIN_TIMEOUT|No compatible.|  
|SQL_OPT_TRACE|Se admite.|  
|SQL_OPT_TRACEFILE|Se admite.|  
|SQL_PACKET_SIZE|No compatible.|  
|SQL_QUIET_MODE|No compatible.|  
|SQL_TRANSLATE_DLL|No compatible.|  
|SQL_TRANSLATION_OPTION|No compatible.|  
|SQL_TXN_ISOLATION|No compatible.|
