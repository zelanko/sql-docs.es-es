---
description: Propiedad Size (Stream de ADO)
title: Propiedad Size (secuencia de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: rothja
ms.author: jroth
ms.openlocfilehash: dc2f09b6c5f6fd784ab5c4ca29a7596b838e38fb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989106"
---
# <a name="size-property-ado-stream"></a>Propiedad Size (Stream de ADO)
Indica el tamaño de la secuencia en número de bytes.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor de **tipo Long** que especifica el tamaño de la secuencia en número de bytes. El valor predeterminado es el tamaño de la secuencia o-1 si no se conoce el tamaño de la secuencia.  
  
## <a name="remarks"></a>Observaciones  
 **El tamaño** solo se puede usar con objetos de [secuencia](./stream-object-ado.md) abiertos.  
  
> [!NOTE]
>  Cualquier número de bits se puede almacenar en un objeto de **secuencia** , limitado solo por los recursos del sistema. Si la **secuencia** contiene más bits de los que se pueden representar con un valor **Long** , **el tamaño** se trunca y, por lo tanto, no representa con precisión la longitud de la **secuencia**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad Size (parámetro de ADO)](./size-property-ado-parameter.md)