---
title: Archivos de registro de seguimiento predeterminados deshabilitados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: c27761e6-75ed-4ee4-a236-0cbc42e500a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5c59490dc800aeeae4f3cc7562a12456db7dc32b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132285"
---
# <a name="default-trace-log-files-disabled"></a>Archivos de registro de seguimiento predeterminados deshabilitados
  Esta regla comprueba el valor de la opción de procedimiento almacenado sp_configure default trace enabled para determinar si el seguimiento predeterminado está establecido en ON (1) o en OFF (0). Cuando esta opción está habilitada, el seguimiento predeterminado proporciona información sobre la configuración y los cambios de DDL de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. En algunos casos, esta información puede ser útil para los clientes y el Servicio de atención al cliente y soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] al solucionar problemas con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Utilice el procedimiento almacenado sp_configure para habilitar el seguimiento estableciendo el valor de default trace enabled en 1.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
