---
title: Bit de confianza | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3198188a-2b59-4865-9560-10f760934b8e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c63c98eda9ef0827919bfe36f3a2b14ef717f648
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68021501"
---
# <a name="trustworthy-bit"></a>Bit de confianza
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla determina si el rol dbo para una base de datos está asignado al rol fijo de servidor sysadmin y la base de datos tiene su bit de confianza establecido en ON.  
  
 Si se cumplen estas condiciones, un usuario privilegiado de la base de datos puede elevar los privilegios al rol sysadmin. En este rol, el usuario puede crear y ejecutar ensamblados no seguros que ponen en peligro el sistema.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Desactive el bit de confianza o revoque los permisos sysadmin del rol de la base de datos dbo.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
