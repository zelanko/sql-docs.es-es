---
title: Aumentar o deshabilitar el umbral de procesos bloqueados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fbf49603290a921a29e0a985837771feb645e54c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760518"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>Aumentar o deshabilitar el umbral de procesos bloqueados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
