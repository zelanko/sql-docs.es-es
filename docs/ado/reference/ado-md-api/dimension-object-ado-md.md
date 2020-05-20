---
title: Objeto Dimension (ADO MD) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d5b475600ef211d8203a64a1a2c6d917bb99914
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764306"
---
# <a name="dimension-object-ado-md"></a>Objeto de dimensión (ADO MD)
Representa una de las dimensiones de un cubo multidimensional que contiene una o más jerarquías de miembros.  
  
## <a name="remarks"></a>Comentarios  
 Con las colecciones y las propiedades de un objeto **Dimension** , puede hacer lo siguiente:  
  
-   Identifique la **dimensión** con las propiedades [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) y [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Devuelva una cadena significativa que describa la **dimensión** con la propiedad [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Devuelve los objetos de la [jerarquía](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) que componen la **dimensión** con la colección [hierarchys](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md) .  
  
-   Utilice la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) de ADO estándar para obtener información adicional sobre el objeto de **dimensión** .  
  
 La colección **Properties** contiene propiedades proporcionadas por el proveedor. En la tabla siguiente se enumeran las propiedades que pueden estar disponibles. La lista de propiedades real puede variar en función de la implementación del proveedor. Consulte la documentación del proveedor para obtener una lista más completa de las propiedades disponibles.  
  
|Nombre|Descripción|  
|----------|-----------------|  
|CatalogName|Nombre del catálogo al que pertenece este cubo.|  
|CubeName|Nombre del cubo.|  
|DefaultHierarchy|Nombre único de la jerarquía predeterminada.|  
|Descripción|Una descripción significativa del cubo.|  
|DimensionCaption|Etiqueta o título asociado a la dimensión.|  
|DimensionCardinality|Número de miembros de la dimensión.|  
|DimensionGUID|GUID de la dimensión.|  
|DimensionName|Nombre de la dimensión.|  
|DimensionOrdinal|Número ordinal de la dimensión entre el grupo de dimensiones que forman el cubo.|  
|DimensionType|Tipo de dimensión.|  
|DimensionUniqueName|Nombre no ambiguo de la dimensión.|  
|SchemaName|Nombre del esquema al que pertenece este cubo.|  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto CubeDef (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Colección de dimensiones (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Colección Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
