---
title: El tamaño de paquete de red no debería superar 8060 bytes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 86db5da1-afe4-4fbb-8bf8-33cedc7e4361
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1d66ba3298b2346e2ec139f27ec53d6104ad0ac9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62625822"
---
# <a name="network-packet-size-should-not-exceed-8060-bytes"></a>El tamaño de paquete de red no debería superar 8060 bytes
  Si el valor especificado para sp_configure 'network packet size' o si el tamaño de paquete de red de cualquier usuario registrado es mayor que 8060 bytes, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza diferentes operaciones de asignación de memoria. Esto puede producir un aumento en el espacio de direcciones virtuales de proceso que no se reserva para el grupo de búferes.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 El tamaño de paquete de red no debería superar 8060 bytes.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Artículo 903002 de Microsoft Knowledge Base](https://go.microsoft.com/fwlink/?linkid=117749)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
