---
description: Propiedad primaria (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c599bd75388dc0b2ea7e4a5c16f495817f917ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440797"
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
