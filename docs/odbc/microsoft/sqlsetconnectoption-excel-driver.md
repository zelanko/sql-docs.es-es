---
title: SQLSetConnectOption (controlador de Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Excel Driver
- Excel driver [ODBC], SQLSetConnectOption
ms.assetid: 528d21d1-4516-4497-9da4-7b87d77e622a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b9ddd764823b4ed89d9aae7055cf966f9f840a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301516"
---
# <a name="sqlsetconnectoption-excel-driver"></a>SQLSetConnectOption (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|El SQL_ACCESS_MODE fOption se puede establecer en SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no impide las actualizaciones si SQL_ACCESS_MODE está establecido en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|El controlador de Microsoft Excel solo admite SQL_AUTOCOMMIT se establece en ON (el estado predeterminado), ya que no admiten transacciones.|  
|SQL_CURRENT_QUALIFIER|Se admite.|  
|SQL_LOGIN_TIMEOUT|No se admite.|  
|SQL_OPT_TRACE|Se admite.|  
|SQL_OPT_TRACEFILE|Se admite.|  
|SQL_PACKET_SIZE|No se admite.|  
|SQL_QUIET_MODE|No se admite.|  
|SQL_TRANSLATE_DLL|No se admite.|  
|SQL_TRANSLATION_OPTION|No se admite.|  
|SQL_TXN_ISOLATION|No se admite.|
