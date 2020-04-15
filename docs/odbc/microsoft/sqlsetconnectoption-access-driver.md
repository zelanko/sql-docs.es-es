---
title: SQLSetConnectOption (controlador de acceso) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e5f15575d34031d9886219af5677b4fc5f1d5aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301538"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|El SQL_ACCESS_MODE fOption se puede establecer en SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no impide las actualizaciones si SQL_ACCESS_MODE se establece en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Cuando se usa el controlador de Microsoft Access, la opción SQL_AUTOCOMMIT se puede establecer en SQL_AUTOCOMMIT_ON o SQL_AUTOCOMMIT_OFF, ya que el controlador de Microsoft Access admite transacciones[1].|  
|SQL_CURRENT_QUALIFIER|Compatible.|  
|SQL_LOGIN_TIMEOUT|No compatible.|  
|SQL_OPT_TRACE|Compatible.|  
|SQL_OPT_TRACEFILE|Compatible.|  
|SQL_PACKET_SIZE|No compatible.|  
|SQL_QUIET_MODE|No compatible.|  
|SQL_TRANSLATE_DLL|No compatible.|  
|SQL_TRANSLATION_OPTION|No compatible.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION siempre está SQL_TXN_READ_COMMITTED.|  
  
 [1] Las transacciones atómicas no son compatibles con el controlador de Microsoft Access. Al confirmar una transacción mediante el controlador de Microsoft Access, existe un retraso finito entre el momento en que se confirma la transacción y el momento en que los valores se escriben en el disco. Este retraso viene determinado por un retraso inherente al motor de Microsoft Jet. El tiempo de espera de página no será menor que un valor mínimo, incluso si la opción PageTimeout se establece por debajo de ese valor. Como resultado, no hay garantía de que los datos confirmados sean estables, ya que se pueden realizar cambios durante el retraso.
