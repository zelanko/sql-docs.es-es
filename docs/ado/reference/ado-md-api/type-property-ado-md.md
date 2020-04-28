---
title: Propiedad Type (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Type
- Type
helpviewer_keywords:
- Type property [ADO MD]
ms.assetid: 34698910-64b9-41d8-8531-9de12f2b1e32
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1109ef6cae68fb2edb4ab3867971064637a6385f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949118"
---
# <a name="type-property-ado-md"></a>Tipo (propiedad, ADO MD)
Indica el tipo del [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md)actual.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor de [MemberTypeEnum](../../../ado/reference/ado-md-api/membertypeenum.md) y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad solo se admite en los objetos [member](../../../ado/reference/ado-md-api/member-object-ado-md.md) que pertenecen a un objeto [LEVEL](../../../ado/reference/ado-md-api/level-object-ado-md.md) . Se produce un error cuando se hace referencia a esta propiedad desde objetos **member** que pertenecen a un objeto [Position](../../../ado/reference/ado-md-api/position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)
