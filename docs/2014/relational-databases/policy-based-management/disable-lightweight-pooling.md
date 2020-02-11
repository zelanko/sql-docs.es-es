---
title: Deshabilitar la agrupación ligera | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 481bb43d-6fe5-497c-9096-971fb6bf733b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8e04ec8fa809f4bea8c19e2e0167b943767224c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62705338"
---
# <a name="disable-lightweight-pooling"></a>Deshabilitar la agrupación ligera
  Esta regla comprueba que la agrupación ligera está deshabilitada en el servidor. Si establece lightweightpooling en el valor 1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cambiará a la programación en modo de fibra. El modo de fibra se destina a determinadas situaciones en las que el cambio de contexto de los trabajadores de UMS es un cuello de botella importante para el rendimiento. Al ser esta situación inusual, el modo de fibra rara vez mejora el rendimiento o la escalabilidad en el sistema típico.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 La opción lightweightpooling solo debería habilitarse después de realizar pruebas minuciosas, una vez evaluadas todas las demás oportunidades de ajustar el rendimiento y cuando el cambio de contexto sea un problema constatado del entorno.  
  
 Se recomienda no usar la programación del modo de fibra en el funcionamiento normal porque puede reducir el rendimiento al impedir las ventajas normales del cambio de contexto y que algunos componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usan el almacenamiento local de subprocesos (TLS) u objetos de subprocesos, como exclusiones mutuas (un tipo de objeto de kernel de Win32), no pueden funcionar correctamente en modo de fibra.  
  
 Para quitar la agrupación ligera, ejecute la instrucción siguiente y, a continuación, reinicie [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```  
sp_configure 'show advanced options', 1;  
GO  
sp_configure 'lightweightpooling', 0;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="for-more-information"></a>Para obtener más información  
 [lightweight pooling (opción de configuración del servidor)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
