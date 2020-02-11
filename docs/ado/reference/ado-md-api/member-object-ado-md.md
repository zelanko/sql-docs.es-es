---
title: Objeto miembro (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44d6b5f06bffb1cea786ba34d3d2aa8a3efb45ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949496"
---
# <a name="member-object-ado-md"></a>Objeto de miembro (ADO MD)
Representa un miembro de un nivel de un cubo, los elementos secundarios de un miembro de un nivel o un miembro de una posición a lo largo de un eje de un Cellset.  
  
## <a name="remarks"></a>Observaciones  
 Las propiedades de un **miembro** difieren en función del contexto en el que se utiliza. Un **miembro** de un [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) de un [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) tiene una propiedad [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) que devuelve los **miembros** del siguiente nivel inferior de la jerarquía del **miembro**actual. Para un **miembro** de una [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md), la colección **Children** siempre está vacía. Además, la propiedad [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) solo se aplica a **los miembros** de un **nivel**.  
  
 Un **miembro** de **Position** tiene dos propiedades que son útiles al mostrar el [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) y [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md). Se producirá un error si se tiene acceso a estas propiedades en un **miembro** de un **nivel**.  
  
 Con las colecciones y las propiedades de un objeto de **miembro** de un **nivel**, puede hacer lo siguiente:  
  
-   Identifique el **miembro** con las propiedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Devuelve una cadena que se va a usar al mostrar el **miembro** con la propiedad [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) .  
  
-   Devuelva una cadena significativa que describa una medida o un **miembro** de fórmula con la propiedad [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Determinar la naturaleza del **miembro** con la propiedad [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) .  
  
-   Obtenga información sobre el **nivel** del **miembro** con las propiedades [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) y [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) .  
  
-   Obtener **miembros** relacionados en una [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) con las propiedades [Parent](../../../ado/reference/ado-md-api/parent-property-ado-md.md) y [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) .  
  
-   Cuente los elementos secundarios de un **miembro** con la propiedad [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) .  
  
-   Utilice la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de ADO estándar para obtener información adicional sobre el objeto de **nivel** .  
  
 Con las colecciones y las propiedades de un **miembro** de una **posición** a lo largo de un [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md), puede hacer lo siguiente:  
  
-   Identifique el **miembro** con las propiedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Devuelve una cadena que se va a usar al mostrar el **miembro** con la propiedad [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) .  
  
-   Devuelva una cadena significativa que describa una medida o un **miembro** de fórmula con la propiedad [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Obtenga información sobre el **nivel** del **miembro** con las propiedades [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) y [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) .  
  
-   Cuente los elementos secundarios de un **miembro** con la propiedad [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) .  
  
-   Utilice la propiedad [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) para determinar si existe al menos un elemento secundario en el **eje** que sigue inmediatamente a este **miembro**.  
  
-   Utilice la propiedad [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) para determinar si el elemento primario de este **miembro** es igual que el elemento primario del **miembro**inmediatamente anterior.  
  
-   Utilice la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de ADO estándar para obtener información adicional sobre el objeto de **nivel** .  
  
 La colección **Properties** contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumeran las propiedades que pueden estar disponibles. La lista de propiedades real puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista más completa de las propiedades disponibles.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|CatalogName|Nombre del catálogo al que pertenece este cubo.|  
|ChildrenCardinality|Número de elementos secundarios que tiene este miembro.|  
|CubeName|Nombre del cubo.|  
|Descripción|Una descripción significativa del miembro.|  
|DimensionUniqueName|Nombre no ambiguo de la [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|Nombre no ambiguo de la jerarquía.|  
|LevelNumber|Distancia entre el nivel y la raíz de la jerarquía.|  
|LevelUniqueName|Nombre no ambiguo del nivel.|  
|MemberCaption|Etiqueta o descripción asociada al miembro.|  
|MemberGUID|GUID del miembro.|  
|MemberName|Nombre del miembro.|  
|MemberOrdinal|Número ordinal del miembro.|  
|MemberType|Tipo del miembro.|  
|MemberUniqueName|Nombre no ambiguo del miembro.|  
|ParentCount|Recuento del número de elementos primarios que tiene este miembro.|  
|ParentLevel|Número de nivel del elemento primario del miembro.|  
|ParentUniqueName|Nombre no ambiguo del elemento primario del miembro.|  
|SchemaName|Nombre del esquema al que pertenece este cubo.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Colección de miembros (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
