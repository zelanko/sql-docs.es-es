---
title: Mantenimiento del valor predeterminado de la opción de configuración Bloqueos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: f214f05b-5f0b-4786-b2ad-b8b4b6e58d72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a45e9b7cb639b0588750fc9b2a9b70a25cd7f0f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057971"
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
  
 [sys.dm_tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql)  
  
 [Artículo 271509 de Microsoft Knowledge Base](https://go.microsoft.com/fwlink/?linkid=117788)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
