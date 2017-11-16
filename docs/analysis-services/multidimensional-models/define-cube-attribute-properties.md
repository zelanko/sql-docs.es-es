---
title: Definir las propiedades de atributo de cubo | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cubes [Analysis Services], defining
ms.assetid: 579ca818-f33d-4060-906d-c8bfee93bf99
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fe36e6ba9ff002706260e2e195adb292ba19b085
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="define-cube-attribute-properties"></a>Definir propiedades de los atributos de los cubos
  Las propiedades de atributo de los cubos le permiten especificar valores únicos para atributos de dimensión en dimensiones de cubo basadas en la misma dimensión de base de datos. En la siguiente tabla se describen las propiedades de un atributo de cubo.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**AggregationUsage**|Especifica el modo en que el Asistente para diseñar agregaciones diseña las agregaciones para el atributo. El valor predeterminado es **Default**. Esta propiedad puede tener los valores siguientes:<br /><br /> **Default**:<br />                    El Asistente para diseñar agregaciones aplica una regla predeterminada basada en el tipo de atributo (Full para las claves, Unrestricted para los demás elementos).<br /><br /> **None**:<br />                    Ninguna agregación del cubo debe incluir este atributo.<br /><br /> **Unrestricted**:<br />                    No se aplica ninguna restricción en el Asistente para diseñar agregaciones.<br /><br /> **Full**:<br />                    Todas las agregaciones del cubo deben incluir este atributo.|  
|**AttributeHierarchyEnabled**|Indica si la jerarquía de atributo está habilitada en esta dimensión de cubo. Permite deshabilitar las jerarquías de atributo en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente está deshabilitada. El valor predeterminado es **True**.|  
|**OptimizedState**|Indica si la jerarquía de atributo está optimizada en esta dimensión de cubo. Permite optimizar las jerarquías de atributo en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente no está optimizada. El valor predeterminado es **FullyOptimized**. Esta propiedad puede tener los valores siguientes:<br /><br /> **FullyOptimized**: La instancia genera índices para la jerarquía, para mejorar el rendimiento de las consultas. Es el valor predeterminado.<br /><br /> **NotOptimized**:<br />                    La instancia no genera otros índices.|  
|**AttributeHierarchyVisible**|Indica si la jerarquía de atributo está visible en esta dimensión de cubo. Permite hacer que las jerarquías de atributo estén visibles en cubos específicos o en roles de dimensión. Esta opción no surte efecto si la jerarquía de atributo subyacente no está visible. El valor predeterminado es **True**.|  
|**AttributeID**|Contiene el identificador único (Id.) del atributo.|  
  
## <a name="see-also"></a>Vea también  
 [Definir las propiedades de una dimensión de cubo](../../analysis-services/multidimensional-models/define-cube-dimension-properties.md)   
 [Definir propiedades de la jerarquía de cubo](../../analysis-services/multidimensional-models/define-cube-hierarchy-properties.md)  
  
  

