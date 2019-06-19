---
title: Definir las propiedades de atributo de cubo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7e2ab2374955710452f1ba1cba91e3a4d8ff8c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025492"
---
# <a name="define-cube-attribute-properties"></a>Definir propiedades de los atributos de los cubos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Las propiedades de atributo de los cubos le permiten especificar valores únicos para atributos de dimensión en dimensiones de cubo basadas en la misma dimensión de base de datos. En la siguiente tabla se describen las propiedades de un atributo de cubo.  
  
|Property|Descripción|  
|--------------|-----------------|  
|**AggregationUsage**|Especifica el modo en que el Asistente para diseñar agregaciones diseña las agregaciones para el atributo. El valor predeterminado es **Default**. Esta propiedad puede tener los valores siguientes:<br /><br /> **Default**:<br />                    El Asistente para diseñar agregaciones aplica una regla predeterminada basada en el tipo de atributo (Full para las claves, Unrestricted para los demás elementos).<br /><br /> **None**:<br />                    Ninguna agregación del cubo debe incluir este atributo.<br /><br /> **Unrestricted**:<br />                    No se aplica ninguna restricción en el Asistente para diseñar agregaciones.<br /><br /> **Full**:<br />                    Todas las agregaciones del cubo deben incluir este atributo.|  
|**AttributeHierarchyEnabled**|Indica si la jerarquía de atributo está habilitada en esta dimensión de cubo. Permite deshabilitar las jerarquías de atributo en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente está deshabilitada. El valor predeterminado es **True**.|  
|**OptimizedState**|Indica si la jerarquía de atributo está optimizada en esta dimensión de cubo. Permite optimizar las jerarquías de atributo en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente no está optimizada. El valor predeterminado es **FullyOptimized**. Esta propiedad puede tener los valores siguientes:<br /><br /> **FullyOptimized**: La instancia genera índices para la jerarquía, para mejorar el rendimiento de las consultas. Este es el valor predeterminado.<br /><br /> **NotOptimized**:<br />                    La instancia no genera otros índices.|  
|**AttributeHierarchyVisible**|Indica si la jerarquía de atributo está visible en esta dimensión de cubo. Permite hacer que las jerarquías de atributo estén visibles en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente no está visible. El valor predeterminado es **True**.|  
|**AttributeID**|Contiene el identificador único (Id.) del atributo.|  
  
## <a name="see-also"></a>Vea también  
 [Definir las propiedades de una dimensión de cubo](../../analysis-services/multidimensional-models/define-cube-dimension-properties.md)   
 [Definir propiedades de las jerarquías de cubos](../../analysis-services/multidimensional-models/define-cube-hierarchy-properties.md)  
  
  
