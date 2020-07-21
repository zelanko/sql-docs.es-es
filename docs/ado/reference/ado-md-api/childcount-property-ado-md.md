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
author: rothja
ms.author: jroth
ms.openlocfilehash: 858bed2c2fe04a1fbf0486b0e0bfc9a26447e4ef
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764406"
---
# <a name="childcount-property-ado-md"></a>Propiedad ChildCount (ADO MD)
Indica el número de miembros para los que el objeto [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) actual es el elemento primario de una jerarquía.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un entero **largo** y es de solo lectura.  
  
## <a name="remarks"></a>Comentarios  
 Use la propiedad **ChildCount** para devolver una estimación del número de elementos secundarios que tiene un **miembro** . Los elementos secundarios reales de un **miembro** pueden ser devueltos por la propiedad [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) .  
  
 Para los objetos **miembro** de un objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) , el número máximo devuelto es 65536. Si el número real de elementos secundarios supera 65536, el valor devuelto seguirá siendo 65536. Por lo tanto, la aplicación debe interpretar un valor de **ChildCount** de 65536 como igual o superior a 65536 elementos secundarios.  
  
 Para los objetos de **miembro** de un objeto de [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) , use la propiedad [recuento](../../../ado/reference/ado-api/count-property-ado.md) de colecciones de ADO en la colección de **elementos secundarios** para determinar el número exacto de elementos secundarios. La determinación del número exacto de elementos secundarios puede ser lenta si el número de elementos secundarios de la colección es grande.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad Children (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Propiedad Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Colección Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
