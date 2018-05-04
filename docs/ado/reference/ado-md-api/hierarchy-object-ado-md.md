---
title: Objeto Hierarchy (ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b920f2235a0e259194165692278ed55cac304b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="hierarchy-object-ado-md"></a>Objeto Hierarchy (ADO MD)
Representa una forma en que los miembros de un [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) puede agregar o "acumular." Una dimensión puede agregarse a lo largo de una o más jerarquías.  
  
## <a name="remarks"></a>Comentarios  
 Con las colecciones y las propiedades de un **jerarquía** objeto, puede hacer lo siguiente:  
  
-   Identificar la **jerarquía** con el [nombre](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propiedades.  
  
-   Devolver una cadena que describe la **jerarquía** con el [descripción](../../../ado/reference/ado-md-api/description-property-ado-md.md) propiedad.  
  
-   Devolver el [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) objetos que componen la **jerarquía** con el [niveles](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) colección.  
  
-   Use la propiedad ADO estándar [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección para obtener información adicional sobre la **jerarquía** objeto.  
  
 El **propiedades** colección contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumera propiedades que estén disponibles. La lista de propiedades reales puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista completa de propiedades disponibles.  
  
|Nombre|Description|  
|----------|-----------------|  
|AllMember|El miembro en el nivel superior del resumen de la jerarquía.|  
|CatalogName|El nombre del catálogo al que pertenece este cubo.|  
|CubeName|Nombre del cubo.|  
|DefaultMember|El nombre único del miembro predeterminado para esta jerarquía.|  
|Description|Descripción de la jerarquía.|  
|DimensionType|El tipo de dimensión al que pertenece esta jerarquía.|  
|DimensionUniqueName|El nombre no ambiguo de la dimensión.|  
|HierarchyCaption|Etiqueta o título asociado a la jerarquía.|  
|HierarchyCardinality|Número de miembros de la jerarquía.|  
|HierarchyGUID|El GUID de la jerarquía.|  
|HierarchyName|Es el nombre de la jerarquía.|  
|HierarchyUniqueName|El nombre no ambiguo de la jerarquía.|  
|SchemaName|El nombre del esquema al que pertenece este cubo.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto de dimensión (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Colección Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Colección de niveles (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
