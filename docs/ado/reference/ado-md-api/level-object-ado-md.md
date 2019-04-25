---
title: Nivel de objeto (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 27e789c4eb34ed275d6f18f62325287febb73422
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740195"
---
# <a name="level-object-ado-md"></a>Objeto Level (ADO MD)
Contiene un conjunto de miembros, cada uno de los cuales tiene el mismo rango dentro de una jerarquía.  
  
## <a name="remarks"></a>Comentarios  
 Con las colecciones y propiedades de un **nivel** de objeto, puede hacer lo siguiente:  
  
-   Identificar el **nivel** con el [nombre](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propiedades.  
  
-   Devolver una cadena que se usará al mostrar la **nivel** con el [título](../../../ado/reference/ado-md-api/caption-property-ado-md.md) propiedad.  
  
-   Devolver una cadena que describe el **nivel** con el [descripción](../../../ado/reference/ado-md-api/description-property-ado-md.md) propiedad.  
  
-   Devolver el [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos que componen el **nivel** con el [miembros](../../../ado/reference/ado-md-api/members-collection-ado-md.md) colección.  
  
-   Devolver el número de niveles de la raíz de la **nivel** con el [profundidad](../../../ado/reference/ado-md-api/depth-property-ado-md.md) propiedad.  
  
-   Usar el estándar de ADO [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección para obtener información adicional sobre el **nivel** objeto.  
  
 El **propiedades** colección contiene las propiedades proporcionadas por el proveedor. En la tabla siguiente se enumera las propiedades que podrían estar disponibles. La lista de propiedades reales puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista completa de las propiedades disponibles.  
  
|Name|Descripción|  
|----------|-----------------|  
|CatalogName|El nombre del catálogo al que pertenece este cubo.|  
|CubeName|Nombre del cubo.|  
|Descripción|Una descripción significativa del nivel.|  
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
