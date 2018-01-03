---
title: Propiedad ChildCount (ADO MD) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords: ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83637d5fd74dd034ae33c4f2ae1a4e6dfaeca43d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="childcount-property-ado-md"></a>Propiedad ChildCount (ADO MD)
Indica el número de miembros para los que el actual [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objeto es el elemento primario en una jerarquía.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** entero y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Use la **ChildCount** propiedad para devolver una estimación del número de elementos secundarios un **miembro** tiene. Los propios elementos secundarios de un **miembro** puede devolver el [elementos secundarios](../../../ado/reference/ado-md-api/children-property-ado-md.md) propiedad.  
  
 Para **miembro** objetos desde una [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md) de objeto, el número máximo que se devuelve es 65536. Si el número real de elementos secundarios es mayor que 65.536, el valor devuelto se seguirá 65536. Por lo tanto, la aplicación debería interpretar un **ChildCount** de 65.536 como igual o mayor que 65536 elementos secundarios.  
  
 Para **miembro** objetos desde una [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) objeto, utilice la colección de ADO [recuento](../../../ado/reference/ado-api/count-property-ado.md) propiedad en el **elementos secundarios** colección para determinar el número exacto de elementos secundarios. Determinar el número exacto de elementos secundarios puede ser lento si el número de elementos secundarios en la colección es grande.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Los elementos secundarios (propiedad, ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count (propiedad, ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Colección Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
