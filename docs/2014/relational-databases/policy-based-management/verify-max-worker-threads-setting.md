---
title: Comprobar el valor de Máximo de subprocesos de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 01e397437c7ed2912b6d6225ee1f3bd5073a405c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48185025"
---
# <a name="verify-max-worker-threads-setting"></a>Comprobar el valor de Máximo de subprocesos de trabajo
  Esta regla comprueba si la opción de servidor Máximo de subprocesos de trabajo tiene valores potencialmente incorrectos. Al establecer la opción Máximo de subprocesos de trabajo en un valor pequeño, puede evitar que suficientes subprocesos atiendan las solicitudes de clientes entrantes de una manera oportuna y podría provocar el "colapso de los subprocesos". Sin embargo, al establecer la opción en un valor grande, puede desperdiciar el espacio de direcciones, porque cada subproceso activo consume 512 KB en los servidores de 32 bits y hasta 4 MB en los servidores de 64 bits.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción Máximo de subprocesos de trabajo en 0. Esto permite que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine automáticamente el número correcto de subprocesos de trabajo activos según las solicitudes de usuario.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Establecer la opción de configuración del servidor Máximo de subprocesos de trabajo](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
