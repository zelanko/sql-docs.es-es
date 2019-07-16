---
title: SQLSetConnectOption (dBASE controlador) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], dBASE Driver
ms.assetid: b1924c33-6820-4566-b716-6897807edd0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9f2fc32287df9da61d8eabc1b22445d19a0f027
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090864"
---
# <a name="sqlsetconnectoption-dbase-driver"></a>SQLSetConnectOption (dBASE controlador)
> [!NOTE]  
>  Este tema proporciona información específica del controlador de dBASE. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Puede establecerse la fOption SQL_ACCESS_MODE SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no impide que las actualizaciones si SQL_ACCESS_MODE está establecido en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|El controlador de dBASE sólo admite SQL_AUTOCOMMIT está activado (el estado predeterminado), porque no admite transacciones.|  
|SQL_CURRENT_QUALIFIER|Se admite.|  
|SQL_LOGIN_TIMEOUT|No compatible.|  
|SQL_OPT_TRACE|Se admite.|  
|SQL_OPT_TRACEFILE|Se admite.|  
|SQL_PACKET_SIZE|No compatible.|  
|SQL_QUIET_MODE|No compatible.|  
|SQL_TRANSLATE_DLL|No compatible.|  
|SQL_TRANSLATION_OPTION|No compatible.|  
|SQL_TXN_ISOLATION|No compatible.|
