---
title: Aumentar o deshabilitar el umbral de procesos bloqueados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b392ec86b64ee41864dfa3c2067e549031b31900
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

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
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  

