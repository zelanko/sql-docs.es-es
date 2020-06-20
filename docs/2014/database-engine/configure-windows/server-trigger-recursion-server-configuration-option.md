---
title: server trigger recursion (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- recursive triggers [SQL Server]
- triggers [SQL Server], recursive
- server trigger recursion option
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 23a4997bd1a6f8b2c04af34d5cdc3229575901a9
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934857"
---
# <a name="server-trigger-recursion-server-configuration-option"></a>server trigger recursion (opción de configuración del servidor)
  Use la opción **server trigger recursion** para especificar si se permite la activación repetida de los desencadenadores del servidor. Cuando esta opción se establece en 1 (activada), se permite esta activación repetida. Cuando el valor es 0 (desactivada), los desencadenadores del servidor no pueden activarse repetidamente. Cuando la opción server trigger recursion se establece en 0 (desactivada), solo se impide la recursividad directa. (Para deshabilitar la recursividad indirecta, establezca la opción **nested triggers** en 0). El valor predeterminado para esta opción es 1 (activada). El valor surte efecto inmediatamente (sin necesidad de reiniciar el servidor).  
  
 Para obtener más información, vea [Crear desencadenadores anidado](../../relational-databases/triggers/create-nested-triggers.md).  
  
## <a name="see-also"></a>Consulte también  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
