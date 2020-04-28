---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c248139abfd136d5c79658592e0e49d5e10444aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949393"
---
# <a name="name-property-ado-md"></a>Name (propiedad, ADO MD)
Indica el nombre de un objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve una **cadena** y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 Puede recuperar la propiedad **Name** de un objeto mediante una referencia ordinal, después de la cual puede hacer referencia al objeto directamente por su nombre. Por ejemplo, si `cdf.CubeDefs(0).Name` produce "bobs Video Store", puede hacer referencia a este [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) como `cdf.CubeDefs("Bobs Video Store")`.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[Objeto de dimensión (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[Objeto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Propiedad Caption (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Propiedad Description (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [UniqueName (propiedad, ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
