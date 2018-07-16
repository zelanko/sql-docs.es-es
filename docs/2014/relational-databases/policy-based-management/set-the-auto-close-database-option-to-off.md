---
title: Establecer en OFF la opción de base de datos AUTO_CLOSE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4311a5f563c088533e28778f2023e97e12f5544a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37262541"
---
# <a name="set-the-autoclose-database-option-to-off"></a>Establecer en OFF la opción de base de datos AUTO_CLOSE
  Esta regla comprueba si la opción AUTO_ CLOSE está establecida en OFF. Cuando AUTO_CLOSE se establece en ON, esta opción puede producir la degradación del rendimiento en las bases de datos a las que se tiene acceso con frecuencia debido a la mayor sobrecarga que supone la apertura y el cierre de la base de datos después de cada conexión. AUTO_CLOSE también vacía la memoria caché de procedimientos después de cada conexión.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Si se tiene acceso a una base de datos con frecuencia, establezca la opción AUTO_CLOSE en OFF para la base de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
