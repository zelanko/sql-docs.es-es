---
title: Propiedad ChildCount (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8d9a0d746d88423c699907e266a93a2b3a08e031
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709569"
---
# <a name="childcount-property-ado-md"></a>Propiedad ChildCount (ADO MD)
Indica el número de miembros para el que el actual [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objeto es el elemento primario en una jerarquía.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** entero y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Use la **ChildCount** propiedad para devolver una estimación de cuántos elementos secundarios una **miembro** tiene. Los propios elementos secundarios de un **miembro** puede devolver el [hijos](../../../ado/reference/ado-md-api/children-property-ado-md.md) propiedad.  
  
 Para **miembro** objetos desde una [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) objeto, el número máximo de devuelto es 65536. Si el número real de elementos secundarios es mayor que 65.536, el valor devuelto será aún 65536. Por lo tanto, la aplicación debería interpretar un **ChildCount** de 65.536 como igual o mayor que 65536 secundarios.  
  
 Para **miembro** objetos desde una [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) de objeto, utilice la colección de ADO [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad en el **elementos secundarios** colección para determinar el número exacto de elementos secundarios. Determinar el número exacto de elementos secundarios puede ser lento si el número de elementos secundarios de la colección es grande.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Elementos secundarios (propiedad, ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count (propiedad, ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Colección Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
