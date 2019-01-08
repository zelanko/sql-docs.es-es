---
title: Aumentar o deshabilitar el umbral de procesos bloqueados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 694c5676a5d55fe4fca227d9042ff4f1a9e9d618
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761867"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>Aumentar o deshabilitar el umbral de procesos bloqueados
  Esta regla comprueba si la opción blocked process threshold esté establecida en 0 (deshabilitada) o en un valor mayor o igual que 5 (segundos). Si se establece la opción blocked process threshold en un valor comprendido entre 1 y 4, puede provocar que el monitor de interbloqueo se ejecute constantemente. Los valores 1 a 4 solo se deberían utilizar para solucionar problemas y nunca a largo plazo o en un entorno de producción sin la ayuda del servicio de atención al cliente y soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Para resolver este problema, establezca el valor de la opción blocked process threshold en 5 (segundos) o más, o deshabilite el umbral de procesos bloqueados estableciendo el valor en 0. Para establecer el valor en `5` segundos, ejecute la instrucción siguiente:  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 5 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="for-more-information"></a>Para obtener más información  
 [blocked process threshold (opción de configuración del servidor)](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
