---
description: Tipo (propiedad, ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 30cf3c161e30884d370aea0fefd81260bafe141e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777824"
---
# <a name="type-property-ado-md"></a>Tipo (propiedad, ADO MD)
Indica el tipo del [miembro](./member-object-ado-md.md)actual.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor de [MemberTypeEnum](./membertypeenum.md) y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad solo se admite en los objetos [member](./member-object-ado-md.md) que pertenecen a un objeto [LEVEL](./level-object-ado-md.md) . Se produce un error cuando se hace referencia a esta propiedad desde objetos **member** que pertenecen a un objeto [Position](./position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](./member-object-ado-md.md)