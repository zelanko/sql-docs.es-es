---
title: Establecer la opción de base de datos AUTO_SHRINK en OFF | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2b202f2856e066047c5458ef8ed1f40b2422b391
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68021691"
---
# <a name="set-the-auto_shrink-database-option-to-off"></a>Establecer la opción de base de datos AUTO_SHRINK en OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba si la opción de base de datos AUTO_SHRINK está establecida en OFF. Si se reduce y se expande con frecuencia una base de datos, puede provocar la fragmentación física.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Establezca la opción de base de datos AUTO_SHRINK en OFF. Si sabe que el espacio que está reclamando no se va a necesitar en el futuro, puede reclamarlo reduciendo manualmente la base de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 Artículo [315512](https://go.microsoft.com/fwlink/?linkid=117750)de Microsoft Knowledge Base  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
