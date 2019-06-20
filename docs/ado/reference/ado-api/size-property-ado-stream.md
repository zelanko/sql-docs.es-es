---
title: Size (Stream de ADO) de la propiedad | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 42a4725efde507112d51b4f9c41af4ba83f63da4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66719089"
---
# <a name="size-property-ado-stream"></a>Propiedad Size (Stream de ADO)
Indica el tamaño de la secuencia en el número de bytes.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** valor que especifica el tamaño de la secuencia en el número de bytes. El valor predeterminado es el tamaño de la secuencia, o -1 si no se conoce el tamaño de la secuencia.  
  
## <a name="remarks"></a>Comentarios  
 **Tamaño** puede utilizarse solo con open [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
> [!NOTE]
>  Cualquier número de bits se puede almacenar en un **Stream** objeto, limitado únicamente por los recursos del sistema. Si el **Stream** contiene más bits que puede representarse mediante un **largo** valor, **tamaño** se trunca y, por tanto, no se representen con precisión de la longitud de la **Stream**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad Size (parámetro de ADO)](../../../ado/reference/ado-api/size-property-ado-parameter.md)
