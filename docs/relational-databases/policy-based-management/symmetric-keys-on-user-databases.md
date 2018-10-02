---
title: Claves simétricas en bases de datos de usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 213ae962f1dbc45d9e6fc2bed67c94f2eafb1183
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601743"
---
# <a name="symmetric-keys-on-user-databases"></a>Claves simétricas en bases de datos de usuario
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla comprueba si las claves que tienen una longitud de menos de 128 bytes no utilizan el algoritmo de cifrado RC2 o RC4.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Utilice AES de 128 bits o más para crear las claves simétricas para el cifrado de los datos. Si el sistema operativo no admite AES, utilice 3DES.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Elegir un algoritmo de cifrado](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>Ver también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
