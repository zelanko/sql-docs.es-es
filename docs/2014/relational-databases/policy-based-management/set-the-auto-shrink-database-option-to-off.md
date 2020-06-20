---
title: Establecer la opción de base de datos AUTO_SHRINK en OFF | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 42d79ed13a691c3d39a28e7ab35a740a9f613fac
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066676"
---
# <a name="set-the-auto_shrink-database-option-to-off"></a>Establecer la opción de base de datos AUTO_SHRINK en OFF
  Esta regla comprueba si la opción de base de datos AUTO_SHRINK está establecida en OFF. Si se reduce y se expande con frecuencia una base de datos, puede provocar la fragmentación física.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción de base de datos AUTO_SHRINK en OFF. Si sabe que el espacio que está reclamando no se va a necesitar en el futuro, puede reclamarlo reduciendo manualmente la base de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 Artículo [315512](https://go.microsoft.com/fwlink/?linkid=117750)de Microsoft Knowledge Base  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
