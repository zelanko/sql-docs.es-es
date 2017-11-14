---
title: Nivel de objeto (ADO MD) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 73258b69ee6a341098365443f388c6944eb2dd51
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="level-object-ado-md"></a>Objeto Level (ADO MD)
Contiene un conjunto de miembros, cada uno de los cuales tiene el mismo rango dentro de una jerarquía.  
  
## <a name="remarks"></a>Comentarios  
 Con las colecciones y las propiedades de un **nivel** de objeto, puede hacer lo siguiente:  
  
-   Identificar la **nivel** con el [nombre](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propiedades.  
  
-   Devolver una cadena para utilizarla al mostrar el **nivel** con el [título](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propiedad.  
  
-   Devolver una cadena que describe la **nivel** con el [descripción](../../../ado/reference/ado-md-api/description-property-ado-md.md) propiedad.  
  
-   Devolver el [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos que componen la **nivel** con el [miembros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) colección.  
  
-   Devolver el número de niveles de la raíz de la **nivel** con el [profundidad](../../../ado/reference/ado-md-api/depth-property-ado-md.md) propiedad.  
  
-   Use la propiedad ADO estándar [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección para obtener información adicional sobre la **nivel** objeto.  
  
 El **propiedades** colección contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumera propiedades que estén disponibles. La lista de propiedades reales puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista completa de propiedades disponibles.  
  
|Nombre|Description|  
|----------|-----------------|  
|CatalogName|El nombre del catálogo al que pertenece este cubo.|  
|CubeName|Nombre del cubo.|  
|Description|Una descripción significativa del nivel.|  
|DimensionUniqueName|El nombre no ambiguo de la [dimensión](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|El nombre no ambiguo de la jerarquía.|  
|LevelCaption|Etiqueta o título asociado al nivel.|  
|LevelCardinality|Número de miembros del nivel.|  
|LevelGUID|El GUID del nivel.|  
|LevelName|Nombre del nivel.|  
|LevelNumber|La distancia entre el nivel y la raíz de la jerarquía.|  
|LevelType|El tipo de nivel.|  
|LevelUniqueName|Nombre inequívoco del nivel.|  
|SchemaName|El nombre del esquema al que pertenece este cubo.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto Hierarchy (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [Colección de niveles (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Colección Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

