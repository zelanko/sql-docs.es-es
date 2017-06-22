---
title: "Establecer en OFF la opción de base de datos AUTO_CLOSE | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 73fa69efa2d294b0f77de1b93c861f8d3b071ab0
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="set-the-autoclose-database-option-to-off"></a>Establecer en OFF la opción de base de datos AUTO_CLOSE
  Esta regla comprueba si la opción AUTO_ CLOSE está establecida en OFF. Cuando AUTO_CLOSE se establece en ON, esta opción puede producir la degradación del rendimiento en las bases de datos a las que se tiene acceso con frecuencia debido a la mayor sobrecarga que supone la apertura y el cierre de la base de datos después de cada conexión. AUTO_CLOSE también vacía la memoria caché de procedimientos después de cada conexión.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Si se tiene acceso a una base de datos con frecuencia, establezca la opción AUTO_CLOSE en OFF para la base de datos.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
