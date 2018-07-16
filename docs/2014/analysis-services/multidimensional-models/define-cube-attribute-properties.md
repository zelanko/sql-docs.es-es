---
title: Definir las propiedades de atributo de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af8e4c54aac81e4f6decdd6533a052fce751b627
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299225"
---
# <a name="define-cube-attribute-properties"></a>Definir propiedades de los atributos de los cubos
  Las propiedades de atributo de los cubos le permiten especificar valores únicos para atributos de dimensión en dimensiones de cubo basadas en la misma dimensión de base de datos. En la siguiente tabla se describen las propiedades de un atributo de cubo.  
  
|Property|Descripción|  
|--------------|-----------------|  
|`AggregationUsage`|Especifica el modo en que el Asistente para diseñar agregaciones diseña las agregaciones para el atributo. Esta propiedad puede tener los valores siguientes:<br /><br /> `Default`: Valor predeterminado. El Asistente para diseñar agregaciones aplica una regla predeterminada basada en el tipo de atributo (Full para las claves, Unrestricted para los demás elementos).<br /><br /> `None`: Ninguna agregación del cubo debe incluir este atributo.<br /><br /> `Unrestricted`: Restricciones no se colocan en el Asistente para diseñar agregaciones.<br /><br /> `Full`: Todas las agregaciones del cubo deben incluir este atributo.|  
|`AttributeHierarchyEnabled`|Indica si la jerarquía de atributo está habilitada en esta dimensión de cubo. Permite deshabilitar las jerarquías de atributo en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente está deshabilitada. Valor predeterminado es `True`.|  
|`OptimizedState`|Indica si la jerarquía de atributo está optimizada en esta dimensión de cubo. Permite optimizar las jerarquías de atributo en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente no está optimizada. Esta propiedad puede tener los valores siguientes:<br /><br /> `FullyOptimized`: Valor predeterminado. La instancia genera índices para la jerarquía, para mejorar el rendimiento de las consultas. Este es el valor predeterminado.<br /><br /> `NotOptimized`: La instancia no genera otros índices.|  
|`AttributeHierarchyVisible`|Indica si la jerarquía de atributo está visible en esta dimensión de cubo. Permite hacer que las jerarquías de atributo estén visibles en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente no está visible. El valor predeterminado es `True`.|  
|`AttributeID`|Contiene el identificador único (Id.) del atributo.|  
  
## <a name="see-also"></a>Vea también  
 [Definir las propiedades de dimensión de cubo](define-cube-dimension-properties.md)   
 [Definir las propiedades de las jerarquías de cubos](define-cube-hierarchy-properties.md)  
  
  
