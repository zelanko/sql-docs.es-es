---
title: Name (propiedad) (ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 07a54616c2dd16a3a1c7582cbfe36c31ca0bef09
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35284724"
---
# <a name="name-property-ado-md"></a>Name (propiedad, ADO MD)
Indica el nombre de un objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **cadena** y es de solo lectura.  
  
## <a name="remarks"></a>Notas  
 Puede recuperar el **nombre** propiedad de un objeto mediante una referencia ordinal, después del cual puede hacer referencia al objeto directamente por su nombre. Por ejemplo, si `cdf.CubeDefs(0).Name` da como resultado "Equipo Video Store", puede hacer referencia a este [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) como `cdf.CubeDefs("Bobs Video Store")`.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[Objeto Catalog (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[Objeto de dimensión (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[Objeto Level (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Propiedad Caption (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Description (propiedad) (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [UniqueName (propiedad, ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
