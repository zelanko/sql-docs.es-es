---
description: DrilledDown (propiedad, ADO MD)
title: Propiedad DrilledDown (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
author: rothja
ms.author: jroth
ms.openlocfilehash: 7560f7f2c487f42d26d83236d824bf997b4f49d1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778154"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown (propiedad, ADO MD)
Indica si los elementos secundarios siguen inmediatamente al [miembro](./member-object-ado-md.md) en el eje.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor **booleano** y es de solo lectura. **DrilledDown** devuelve **true** si no hay miembros secundarios del miembro actual en el eje. **DrilledDown** devuelve **false** si el miembro actual tiene uno o más miembros secundarios en el eje.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **DrilledDown** para determinar si existe al menos un elemento secundario de este miembro en el eje que sigue inmediatamente a este miembro. Esta información es útil cuando se muestra el miembro.  
  
 Esta propiedad solo se admite en los objetos [member](./member-object-ado-md.md) que pertenezcan a un objeto [Position](./position-object-ado-md.md) . Se produce un error cuando se hace referencia a esta propiedad desde objetos **member** que pertenecen a un objeto [LEVEL](./level-object-ado-md.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [ParentSameAsPrev (propiedad, ADO MD)](./parentsameasprev-property-ado-md.md)