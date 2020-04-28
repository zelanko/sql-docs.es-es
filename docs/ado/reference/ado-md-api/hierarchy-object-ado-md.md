---
title: Objeto Hierarchy (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 35e02e4823d0a3abf245e1885b95176d6350d712
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67949694"
---
# <a name="hierarchy-object-ado-md"></a>Objeto Hierarchy (ADO MD)
Representa una manera en la que los miembros de una [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) se pueden agregar o "acumular". Una dimensión se puede Agregar A una o más jerarquías.  
  
## <a name="remarks"></a>Observaciones  
 Con las colecciones y las propiedades de un objeto **Hierarchy** , puede hacer lo siguiente:  
  
-   Identifique la **jerarquía** con las propiedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Devuelve una cadena significativa que describe la **jerarquía** con la propiedad [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Devuelve los objetos de [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) que componen la **jerarquía** con la colección [Levels](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) .  
  
-   Utilice la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de ADO estándar para obtener información adicional sobre el objeto de **jerarquía** .  
  
 La colección **Properties** contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumeran las propiedades que pueden estar disponibles. La lista de propiedades real puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista más completa de las propiedades disponibles.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|AllMember|Miembro en el nivel más alto de acumulación en la jerarquía.|  
|CatalogName|Nombre del catálogo al que pertenece este cubo.|  
|CubeName|Nombre del cubo.|  
|DefaultMember|Nombre único del miembro predeterminado para esta jerarquía.|  
|Descripción|Una descripción significativa de la jerarquía.|  
|DimensionType|Tipo de dimensión a la que pertenece esta jerarquía.|  
|DimensionUniqueName|Nombre no ambiguo de la dimensión.|  
|HierarchyCaption|Etiqueta o título asociado a la jerarquía.|  
|HierarchyCardinality|Número de miembros de la jerarquía.|  
|HierarchyGUID|GUID de la jerarquía.|  
|HierarchyName|Es el nombre de la jerarquía.|  
|HierarchyUniqueName|Nombre no ambiguo de la jerarquía.|  
|SchemaName|Nombre del esquema al que pertenece este cubo.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto Dimension (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Colección Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Colección de niveles (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
