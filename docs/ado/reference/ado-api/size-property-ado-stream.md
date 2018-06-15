---
title: Cambiar el tamaño de propiedad (Stream de ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d6d39bb563acfde83a08f08c00fee66cc9b81967
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35281890"
---
# <a name="size-property-ado-stream"></a>Propiedad Size (Stream de ADO)
Indica el tamaño de la secuencia en número de bytes.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** valor que especifica el tamaño de la secuencia en número de bytes. El valor predeterminado es el tamaño de la secuencia, o -1 si no se conoce el tamaño de la secuencia.  
  
## <a name="remarks"></a>Notas  
 **Tamaño** puede utilizarse solo con abierta [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
> [!NOTE]
>  Cualquier número de bits puede almacenarse en un **flujo** objeto, limitado por los recursos del sistema. Si el **flujo** contiene más bits que puede representarse mediante un **largo** valor, **tamaño** se trunca y por lo tanto, no se representen con precisión de la longitud de la **Flujo**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad Size (parámetro de ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
