---
title: "Mantenimiento del valor predeterminado de la opción de configuración Bloqueos | Microsoft Docs"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: f214f05b-5f0b-4786-b2ad-b8b4b6e58d72
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a220fc3ad6d6946c5823190440dd3b3f1aa9c286
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="keep-the-locks-configuration-option-default-value"></a>Mantener el valor predeterminado de la opción de configuración Bloqueos
  Esta regla comprueba el valor de la opción de configuración locks. Esta opción determina el número máximo de bloqueos disponibles. Limita cuánta memoria usa [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para los bloqueos. El valor predeterminado es 0, lo que habilita al [!INCLUDE[ssDE](../../includes/ssde-md.md)] para asignar y cancelar la asignación de estructuras de bloqueos de manera dinámica a partir de requisitos variables del sistema.  
  
 Si locks es distinto de cero, los trabajos por lotes se detendrán y se generará un mensaje de error "sin bloqueos", si se supera el valor especificado.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Utilice el procedimiento almacenado de sistema sp_configure para cambiar el valor de locks a su configuración predeterminada utilizando la instrucción siguiente:  
  
```  
EXEC sp_configure 'locks', 0;  
```  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Establecer la opción de configuración del servidor Bloqueos](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)  
  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
  
 [Artículo 271509 de Microsoft Knowledge Base](http://go.microsoft.com/fwlink/?linkid=117788)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
