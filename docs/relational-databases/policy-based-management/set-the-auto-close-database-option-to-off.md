---
title: Establecer en OFF la opción de base de datos AUTO_CLOSE | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bc10818d1c868036be461a92eb57e24b476066df
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806131"
---
# <a name="set-the-autoclose-database-option-to-off"></a>Establecer en OFF la opción de base de datos AUTO_CLOSE
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba si la opción AUTO_ CLOSE está establecida en OFF. Cuando AUTO_CLOSE se establece en ON, esta opción puede producir la degradación del rendimiento en las bases de datos a las que se tiene acceso con frecuencia debido a la mayor sobrecarga que supone la apertura y el cierre de la base de datos después de cada conexión. AUTO_CLOSE también vacía la memoria caché de procedimientos después de cada conexión.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Si se tiene acceso a una base de datos con frecuencia, establezca la opción AUTO_CLOSE en OFF para la base de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Ver también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
