---
title: Claves simétricas en bases de datos de usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3333ab5b-2518-4753-a0a8-57df5e5af74f
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2764ed2bed7446b5c536944814e1c113f6fb58b9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109233"
---
# <a name="symmetric-keys-on-user-databases"></a>Claves simétricas en bases de datos de usuario
  Esta regla comprueba si las claves que tienen una longitud de menos de 128 bytes no utilizan el algoritmo de cifrado RC2 o RC4.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Utilice AES de 128 bits o más para crear las claves simétricas para el cifrado de los datos. Si el sistema operativo no admite AES, utilice 3DES.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Elegir un algoritmo de cifrado](../security/encryption/choose-an-encryption-algorithm.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  