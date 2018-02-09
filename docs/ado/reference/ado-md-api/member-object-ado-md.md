---
title: Objeto de miembro (ADO MD) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c7b34e45ff23a1a71c1a45b1190d923e94328154
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="member-object-ado-md"></a>Objeto de miembro (ADO MD)
Representa a un miembro de un nivel en un cubo, los elementos secundarios de un miembro de un nivel o un miembro de una posición a lo largo de un eje de un conjunto de celdas.  
  
## <a name="remarks"></a>Comentarios  
 Las propiedades de un **miembro** varían según el contexto en el que se usa. A **miembro** de un [nivel](../../../ado/reference/ado-md-api/level-object-ado-md.md) en un [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) tiene un [elementos secundarios](../../../ado/reference/ado-md-api/children-property-ado-md.md) propiedad que devuelve el **miembros** en el siguiente nivel inferior de la jerarquía actual **miembro**. Para una **miembro** de un [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md), **elementos secundarios** colección siempre está vacía. Además, el [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) propiedad se aplica únicamente a **miembros** de un **nivel**.  
  
 A **miembro** de **posición** tiene dos propiedades que son útiles cuando se muestra la [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) y [ ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md). Se producirá un error si se tiene acceso a estas propiedades en un **miembro** de un **nivel**.  
  
 Con las colecciones y las propiedades de un **miembro** objeto de un **nivel**, puede hacer lo siguiente:  
  
-   Identificar la **miembro** con el [nombre](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propiedades.  
  
-   Devolver una cadena para utilizarla al mostrar el **miembro** con el [título](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propiedad.  
  
-   Devolver una cadena que describe una medida o fórmula **miembro** con el [descripción](../../../ado/reference/ado-md-api/description-property-ado-md.md) propiedad.  
  
-   Determinar la naturaleza de la **miembro** con el [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) propiedad.  
  
-   Obtener información sobre la **nivel** de la **miembro** con el [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) y [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) propiedades.  
  
-   Obtener relacionados **miembros** en un [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) con el [primario](../../../ado/reference/ado-md-api/parent-property-ado-md.md) y [elementos secundarios](../../../ado/reference/ado-md-api/children-property-ado-md.md) propiedades.  
  
-   Contar los miembros secundarios de un **miembro** con el [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) propiedad.  
  
-   Use la propiedad ADO estándar [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección para obtener información adicional sobre la **nivel** objeto.  
  
 Con las colecciones y las propiedades de un **miembro** de un **posición** a lo largo de un [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md), puede hacer lo siguiente:  
  
-   Identificar la **miembro** con el [nombre](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propiedades.  
  
-   Devolver una cadena para utilizarla al mostrar el **miembro** con el [título](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propiedad.  
  
-   Devolver una cadena que describe una medida o fórmula **miembro** con el [descripción](../../../ado/reference/ado-md-api/description-property-ado-md.md) propiedad.  
  
-   Obtener información sobre la **nivel** de la **miembro** con el [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) y [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) propiedades.  
  
-   Contar los miembros secundarios de un **miembro** con el [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) propiedad.  
  
-   Use la [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) propiedad para determinar si hay al menos un elemento secundario en el **eje** inmediatamente después de este procedimiento **miembro**.  
  
-   Use la [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) propiedad para determinar si el elemento primario de este **miembro** es el mismo que el elemento primario de la antecede **miembro**.  
  
-   Use la propiedad ADO estándar [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección para obtener información adicional sobre la **nivel** objeto.  
  
 El **propiedades** colección contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumera propiedades que estén disponibles. La lista de propiedades reales puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista completa de propiedades disponibles.  
  
|Nombre|Description|  
|----------|-----------------|  
|CatalogName|El nombre del catálogo al que pertenece este cubo.|  
|ChildrenCardinality|Número de elementos secundarios que tiene este miembro.|  
|CubeName|Nombre del cubo.|  
|Description|Una descripción significativa del miembro.|  
|DimensionUniqueName|El nombre no ambiguo de la [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|El nombre no ambiguo de la jerarquía.|  
|LevelNumber|La distancia entre el nivel y la raíz de la jerarquía.|  
|LevelUniqueName|Nombre inequívoco del nivel.|  
|MemberCaption|Etiqueta o descripción asociada al miembro.|  
|MemberGUID|GUID del miembro.|  
|MemberName|Nombre del miembro.|  
|MemberOrdinal|El número ordinal del miembro.|  
|MemberType|Tipo del miembro.|  
|MemberUniqueName|Nombre inequívoco del miembro.|  
|ParentCount|El recuento del número de primarios que tiene este miembro.|  
|ParentLevel|El número de nivel de elemento primario del miembro.|  
|ParentUniqueName|Nombre inequívoco del elemento primario del miembro.|  
|SchemaName|El nombre del esquema al que pertenece este cubo.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de catálogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Colección Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
