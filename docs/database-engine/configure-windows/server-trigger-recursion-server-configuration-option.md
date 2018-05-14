---
title: server trigger recursion (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- recursive triggers [SQL Server]
- triggers [SQL Server], recursive
- server trigger recursion option
ms.assetid: da4c25f5-d04c-4951-a3db-409e71a1b468
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9c9dff6f026f00b46d525f35e7794e4708e74e4c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="server-trigger-recursion-server-configuration-option"></a>server trigger recursion (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use la opción **server trigger recursion** para especificar si se permite la activación repetida de los desencadenadores del servidor. Cuando esta opción se establece en 1 (activada), se permite esta activación repetida. Cuando el valor es 0 (desactivada), los desencadenadores del servidor no pueden activarse repetidamente. Cuando la opción server trigger recursion se establece en 0 (desactivada), solo se impide la recursividad directa. (Para deshabilitar la recursividad indirecta, establezca la opción **nested triggers** en 0). El valor predeterminado para esta opción es 1 (activada). El valor surte efecto inmediatamente (sin necesidad de reiniciar el servidor).  
  
 Para obtener más información, vea [Crear desencadenadores anidado](../../relational-databases/triggers/create-nested-triggers.md).  
  
## <a name="see-also"></a>Ver también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
