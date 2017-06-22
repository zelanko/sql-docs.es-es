---
title: "Deshabilitar la agrupación ligera | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 481bb43d-6fe5-497c-9096-971fb6bf733b
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 373b219ff44652e584961ee950e1e3a5ca923ef7
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="disable-lightweight-pooling"></a>Deshabilitar la agrupación ligera
  Esta regla comprueba que la agrupación ligera está deshabilitada en el servidor. Si establece lightweightpooling en el valor 1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cambiará a la programación en modo de fibra. El modo de fibra se destina a determinadas situaciones en las que el cambio de contexto de los trabajadores de UMS es un cuello de botella importante para el rendimiento. Al ser esta situación inusual, el modo de fibra rara vez mejora el rendimiento o la escalabilidad en el sistema típico.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 La opción lightweightpooling solo debería habilitarse después de realizar pruebas minuciosas, una vez evaluadas todas las demás oportunidades de ajustar el rendimiento y cuando el cambio de contexto sea un problema constatado del entorno.  
  
 Se recomienda no usar la programación del modo de fibra en el funcionamiento normal porque puede reducir el rendimiento al impedir las ventajas normales del cambio de contexto y que algunos componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usan el almacenamiento local de subprocesos (TLS) u objetos de subprocesos, como exclusiones mutuas (un tipo de objeto de kernel de Win32), no pueden funcionar correctamente en modo de fibra.  
  
 Para quitar la agrupación ligera, ejecute la instrucción siguiente y, a continuación, reinicie [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```tsql  
sp_configure 'show advanced options', 1;  
GO  
sp_configure 'lightweight pooling', 0;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="for-more-information"></a>Para obtener más información  
 [lightweight pooling (opción de configuración del servidor)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  

