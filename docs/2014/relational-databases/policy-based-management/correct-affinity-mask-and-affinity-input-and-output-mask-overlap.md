---
title: Superposición correcta de la máscara de afinidad y de salida de entrada de afinidad | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 1a0da6df-57ff-4f3f-aae9-2fbc4897508c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3139c864805c7df9220afc9b81d2a242775f4fa7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62856699"
---
# <a name="correct-affinity-mask-and-affinity-input-output-mask-overlap"></a>Superposición correcta de la máscara de afinidad y de salida de entrada de afinidad
  Esta regla comprueba si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene uno o varios procesadores que están asignados para usarse con las opciones de máscara de afinidad y de máscara de afinidad de E/S. En un equipo con más de un procesador, las opciones de máscara de afinidad y de máscara de afinidad de E/S se utilizan para designar qué CPU usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al habilitar una CPU con la máscara de afinidad y con la máscara de afinidad de E/S, se puede ralentizar el rendimiento al exigir que el procesador se use demasiado.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Al especificar las opciones de máscara de afinidad o de máscara de afinidad de E/S, debería especificar ambas, pero habilitar cada CPU únicamente una vez.  
  
 No habilite la misma CPU en ambas opciones de máscara de afinidad y de máscara de afinidad de E/S. Los bits que corresponden a cada CPU deberían estar en alguno de los estados siguientes:  
  
-   0 tanto en la opción de máscara de afinidad de E/S como en la opción máscara de afinidad.  
  
-   0 en la opción de máscara de afinidad y 1 en la opción de máscara de afinidad de E/S.  
  
-   1 en la opción de máscara de afinidad y 0 en la opción de máscara de afinidad de E/S.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [affinity mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)  
  
 [affinity Input-Output mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)  
  
 [affinity64 mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md)  
  
 [affinity64 I/O mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
