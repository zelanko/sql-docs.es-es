---
description: Name (propiedad, ADO MD)
title: Propiedad Name (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: rothja
ms.author: jroth
ms.openlocfilehash: 83207cd13db790d645bea146b2a031604e598256
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777954"
---
# <a name="name-property-ado-md"></a>Name (propiedad, ADO MD)
Indica el nombre de un objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve una **cadena** y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 Puede recuperar la propiedad **Name** de un objeto mediante una referencia ordinal, después de la cual puede hacer referencia al objeto directamente por su nombre. Por ejemplo, si `cdf.CubeDefs(0).Name` produce "bobs Video Store", puede hacer referencia a este [CubeDef](./cubedef-object-ado-md.md) como `cdf.CubeDefs("Bobs Video Store")` .  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Objeto Axis (ADO MD)](./axis-object-ado-md.md)  
        [Objeto Catalog (ADO MD)](./catalog-object-ado-md.md)  
        [Objeto CubeDef (ADO MD)](./cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Objeto de dimensión (ADO MD)](./dimension-object-ado-md.md)  
        [Objeto Hierarchy (ADO MD)](./hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Objeto Level (ADO MD)](./level-object-ado-md.md)  
        [Objeto de miembro (ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también  
 [Ejemplo de catálogo (VB)](./catalog-example-vb.md)   
 [Propiedad Caption (ADO MD)](./caption-property-ado-md.md)   
 [Propiedad Description (ADO MD)](./description-property-ado-md.md)   
 [UniqueName (propiedad, ADO MD)](./uniquename-property-ado-md.md)