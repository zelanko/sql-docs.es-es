---
title: Dimensión (objeto) (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 332701caacd2eb4a813e8ec09ff66aa4dc4bf828
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225786"
---
# <a name="dimension-object-ado-md"></a>Objeto de dimensión (ADO MD)
Representa una de las dimensiones de un cubo multidimensional, que contiene una o más jerarquías de miembros.  
  
## <a name="remarks"></a>Comentarios  
 Con las colecciones y propiedades de un **dimensión** objeto, puede hacer lo siguiente:  
  
-   Identificar el **dimensión** con el [nombre](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propiedades.  
  
-   Devolver una cadena que describe el **dimensión** con el [descripción](../../../ado/reference/ado-md-api/description-property-ado-md.md) propiedad.  
  
-   Devolver el [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) objetos que componen el **dimensión** con el [jerarquías](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) colección.  
  
-   Usar el estándar de ADO [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección para obtener información adicional sobre el **dimensión** objeto.  
  
 El **propiedades** colección contiene las propiedades proporcionadas por el proveedor. En la tabla siguiente se enumera las propiedades que podrían estar disponibles. La lista de propiedades reales puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista completa de las propiedades disponibles.  
  
|Name|Descripción|  
|----------|-----------------|  
|CatalogName|El nombre del catálogo al que pertenece este cubo.|  
|CubeName|Nombre del cubo.|  
|DefaultHierarchy|El nombre único de la jerarquía predeterminada.|  
|Descripción|Descripción del cubo.|  
|DimensionCaption|Etiqueta o título asociado con la dimensión.|  
|DimensionCardinality|El número de miembros de la dimensión.|  
|DimensionGUID|El GUID de la dimensión.|  
|DimensionName|Nombre de la dimensión.|  
|DimensionOrdinal|El número ordinal de la dimensión entre el grupo de dimensiones que forman el cubo.|  
|DimensionType|El tipo de dimensión.|  
|DimensionUniqueName|El nombre no ambiguo de la dimensión.|  
|SchemaName|El nombre del esquema al que pertenece este cubo.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Colección Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Colección Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
