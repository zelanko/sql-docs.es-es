---
title: Propiedad Parent (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parent
- Member::Parent
helpviewer_keywords:
- Parent property [ADO MD]
ms.assetid: 32c278c1-d8e1-4bb7-9ecd-2fbfdffee34b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f6d6e03dd3288a5b0ca71bb9e129e1a57abf7c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949327"
---
# <a name="parent-property-ado-md"></a>Propiedad primaria (ADO MD)
Indica el miembro que es primario del [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) actual de una jerarquía.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un objeto de [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 Un miembro que está en el nivel superior de una jerarquía (la raíz) no tiene ningún elemento primario. Esta propiedad solo se admite en los objetos **member** que pertenecen a un objeto [LEVEL](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Se produce un error cuando se hace referencia a esta propiedad desde objetos **member** que pertenecen a un objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Los elementos secundarios (propiedad, ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
