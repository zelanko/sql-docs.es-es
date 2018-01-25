---
title: "Establecer la opción de base de datos AUTO_SHRINK en OFF | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
caps.latest.revision: "11"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 91e260a447d022f04bc74268a8243e3993a7ce61
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="set-the-autoshrink-database-option-to-off"></a>Establecer la opción de base de datos AUTO_SHRINK en OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Esta regla comprueba si la opción de base de datos AUTO_SHRINK está establecida en OFF. Si se reduce y se expande con frecuencia una base de datos, puede provocar la fragmentación física.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción de base de datos AUTO_SHRINK en OFF. Si sabe que el espacio que está reclamando no se va a necesitar en el futuro, puede reclamarlo reduciendo manualmente la base de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 Artículo [315512](http://go.microsoft.com/fwlink/?linkid=117750)de Microsoft Knowledge Base  
  
## <a name="see-also"></a>Ver también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
