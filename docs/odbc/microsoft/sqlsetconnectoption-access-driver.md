---
title: SQLSetConnectOption (controlador de Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18950d49afdab8517b95c59df8841c33b5d3d086
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305639"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Puede establecerse la fOption SQL_ACCESS_MODE SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no impide que las actualizaciones si SQL_ACCESS_MODE está establecido en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Cuando se usa el controlador de Microsoft Access, la opción SQL_AUTOCOMMIT puede establecerse en SQL_AUTOCOMMIT_OFF o SQL_AUTOCOMMIT_OFF, porque el controlador de Microsoft Access admite transacciones [1].|  
|SQL_CURRENT_QUALIFIER|Compatible.|  
|SQL_LOGIN_TIMEOUT|No compatible.|  
|SQL_OPT_TRACE|Compatible.|  
|SQL_OPT_TRACEFILE|Compatible.|  
|SQL_PACKET_SIZE|No compatible.|  
|SQL_QUIET_MODE|No compatible.|  
|SQL_TRANSLATE_DLL|No compatible.|  
|SQL_TRANSLATION_OPTION|No compatible.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION siempre es SQL_TXN_READ_COMMITTED.|  
  
 [1] no se admiten transacciones atómicas por el controlador de Microsoft Access. Al confirmar una transacción con el controlador de Microsoft Access, existe un retraso finito entre el momento en que se confirma la transacción y la hora en que los valores se escriben en el disco. Este retraso viene determinada por un retraso inherente en el motor de Microsoft Jet. El tiempo de espera de la página no será menor que un valor mínimo, incluso si se establece la opción PageTimeout por debajo de ese valor. Como resultado, no hay ninguna garantía de que se confirma los datos es estable, ya que se pueden realizar cambios durante el retraso.
