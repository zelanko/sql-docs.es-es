---
title: "Dimensión (objeto) (ADO MD) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Dimension
helpviewer_keywords: Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b8b166484928abbeba70934d5b597c7e27d41f1f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dimension-object-ado-md"></a>Objeto de dimensión (ADO MD)
Representa una de las dimensiones de un cubo multidimensional, que contiene una o más jerarquías de miembros.  
  
## <a name="remarks"></a>Comentarios  
 Con las colecciones y las propiedades de un **dimensión** objeto, puede hacer lo siguiente:  
  
-   Identificar la **dimensión** con el [nombre](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propiedades.  
  
-   Devolver una cadena que describe la **dimensión** con el [descripción](../../../ado/reference/ado-md-api/description-property-ado-md.md) propiedad.  
  
-   Devolver el [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) objetos que componen la **dimensión** con el [jerarquías](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) colección.  
  
-   Use la propiedad ADO estándar [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección para obtener información adicional sobre la **dimensión** objeto.  
  
 El **propiedades** colección contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumera propiedades que estén disponibles. La lista de propiedades reales puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista completa de propiedades disponibles.  
  
|Nombre|Description|  
|----------|-----------------|  
|CatalogName|El nombre del catálogo al que pertenece este cubo.|  
|CubeName|Nombre del cubo.|  
|Valor de DefaultHierarchy|El nombre único de la jerarquía predeterminada.|  
|Description|Una descripción significativa del cubo.|  
|DimensionCaption|Etiqueta o título asociado a la dimensión.|  
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
