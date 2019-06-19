---
title: Establecer en OFF la opción de base de datos AUTO_CLOSE | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 6b9fda04dd570d0077b692b86937e401bac54e42
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62930889"
---
# <a name="set-the-autoclose-database-option-to-off"></a>Establecer en OFF la opción de base de datos AUTO_CLOSE
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba si la opción AUTO_ CLOSE está establecida en OFF. Cuando AUTO_CLOSE se establece en ON, esta opción puede producir la degradación del rendimiento en las bases de datos a las que se tiene acceso con frecuencia debido a la mayor sobrecarga que supone la apertura y el cierre de la base de datos después de cada conexión. AUTO_CLOSE también vacía la memoria caché de procedimientos después de cada conexión.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Si se tiene acceso a una base de datos con frecuencia, establezca la opción AUTO_CLOSE en OFF para la base de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
