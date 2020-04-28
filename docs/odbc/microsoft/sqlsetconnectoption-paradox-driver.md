---
title: SQLSetConnectOption (controlador de Paradox) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06a90a83e2cbf24e6e85a67d961684c230bca924
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301496"
---
# <a name="sqlsetconnectoption-paradox-driver"></a>SQLSetConnectOption (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|El SQL_ACCESS_MODE fOption se puede establecer en SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no impide las actualizaciones si SQL_ACCESS_MODE está establecido en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|El controlador de Paradox solo admite SQL_AUTOCOMMIT se establece en ON (el estado predeterminado), ya que no admiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Se admite.|  
|SQL_LOGIN_TIMEOUT|No se admite.|  
|SQL_OPT_TRACE|Se admite.|  
|SQL_OPT_TRACEFILE|Se admite.|  
|SQL_PACKET_SIZE|No se admite.|  
|SQL_QUIET_MODE|No se admite.|  
|SQL_TRANSLATE_DLL|No se admite.|  
|SQL_TRANSLATION_OPTION|No se admite.|  
|SQL_TXN_ISOLATION|No se admite.|
