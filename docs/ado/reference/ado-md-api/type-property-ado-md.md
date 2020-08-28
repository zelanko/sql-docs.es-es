---
description: Tipo (propiedad, ADO MD)
title: Propiedad Type (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 52b07fe68f905c7f27bad4685d5df56c25cb2c13
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985976"
---
# <a name="type-property-ado-md"></a>Tipo (propiedad, ADO MD)
Indica el tipo del [miembro](./member-object-ado-md.md)actual.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un valor de [MemberTypeEnum](./membertypeenum.md) y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad solo se admite en los objetos [member](./member-object-ado-md.md) que pertenecen a un objeto [LEVEL](./level-object-ado-md.md) . Se produce un error cuando se hace referencia a esta propiedad desde objetos **member** que pertenecen a un objeto [Position](./position-object-ado-md.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de miembro (ADO MD)](./member-object-ado-md.md)