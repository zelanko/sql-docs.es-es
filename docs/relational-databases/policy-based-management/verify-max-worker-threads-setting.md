---
description: Comprobar el valor de Máximo de subprocesos de trabajo
title: Comprobar el valor de Máximo de subprocesos de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 2d94adfd-3ba1-493a-b29a-b436f9d583df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8c82c2359a8dd4828b8d7da465752eeec44c70f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420479"
---
# <a name="verify-max-worker-threads-setting"></a>Comprobar el valor de Máximo de subprocesos de trabajo
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esta regla comprueba si la opción de servidor Máximo de subprocesos de trabajo tiene valores potencialmente incorrectos. Al establecer la opción Máximo de subprocesos de trabajo en un valor pequeño, puede evitar que suficientes subprocesos atiendan las solicitudes de clientes entrantes de una manera oportuna y podría provocar el "colapso de los subprocesos". Sin embargo, al establecer la opción en un valor grande, puede desperdiciar el espacio de direcciones, porque cada subproceso activo consume hasta 4 MB en los servidores de 64 bits.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción Máximo de subprocesos de trabajo en 0. Esto permite que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determine automáticamente el número correcto de subprocesos de trabajo activos según las solicitudes de usuario.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Establecer la opción de configuración del servidor Máximo de subprocesos de trabajo](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
