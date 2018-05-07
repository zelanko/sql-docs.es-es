---
title: SQLSetConnectOption (controlador de acceso) | Documentos de Microsoft
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
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 952bfe683dabbcedeb771c0e7f1787f7a0e6f7bb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Comentario|  
|-------------|-------------|  
|SQL_ACCESS_MODE|El fOption SQL_ACCESS_MODE puede establecerse en SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Sin embargo, el controlador no evita que las actualizaciones si SQL_ACCESS_MODE se establece en SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Cuando se utiliza el controlador de Microsoft Access, la opción SQL_AUTOCOMMIT puede establecerse en SQL_AUTOCOMMIT_OFF o SQL_AUTOCOMMIT_OFF, porque el controlador de Microsoft Access admite transacciones [1].|  
|SQL_CURRENT_QUALIFIER|Compatible.|  
|SQL_LOGIN_TIMEOUT|No compatible.|  
|SQL_OPT_TRACE|Compatible.|  
|SQL_OPT_TRACEFILE|Compatible.|  
|SQL_PACKET_SIZE|No compatible.|  
|SQL_QUIET_MODE|No compatible.|  
|SQL_TRANSLATE_DLL|No compatible.|  
|SQL_TRANSLATION_OPTION|No compatible.|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION siempre es SQL_TXN_READ_COMMITTED.|  
  
 [1] no se admiten las transacciones atómicas por el controlador de Microsoft Access. Al confirmar una transacción con el controlador de Microsoft Access, existe un retraso finito entre el momento en que se confirma la transacción y el tiempo que los valores se escriben en el disco. Este retraso se determina mediante un retraso inherente en el motor de Microsoft Jet. El tiempo de espera de página no será menor que un valor mínimo, incluso si se establece la opción de PageTimeout por debajo del valor. Como resultado, no hay ninguna garantía de que confirma los datos es estable, ya que se pueden realizar cambios durante el tiempo.
