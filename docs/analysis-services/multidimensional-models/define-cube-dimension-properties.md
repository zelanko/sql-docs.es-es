---
title: "Definir las propiedades de la dimensión de cubo | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6b537ac59e0ca4e680d21cd92cb2f06f34e4adf9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="define-cube-dimension-properties"></a>Definir las propiedades de una dimensión de cubo
  Una dimensión de cubo es una instancia de una dimensión de base de datos en un cubo. Se puede utilizar una dimensión de base de datos en varios cubos y se pueden basar varias dimensiones de cubo en una sola dimensión de base de datos. En la siguiente tabla se describen las propiedades de una dimensión de cubo.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**|Controla cómo se diseñan las agregaciones en el Diseñador de agregaciones, en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Esta propiedad puede tener los valores siguientes:<br /><br /> **Full**: todas las agregaciones del cubo deben incluir el miembro All.<br /><br /> **None**: ninguna agregación del cubo puede incluir el miembro All. Es el valor predeterminado.<br /><br /> **Unrestricted**: no se aplica ninguna restricción en el Diseñador de agregaciones.<br /><br /> **Default**: la misma funcionalidad que Unrestricted.|  
|**Description**|Proporciona un nombre descriptivo para el nivel.|  
|**DimensionID**|Contiene el identificador único de la dimensión de base de datos.|  
|**HierarchyUniqueNameStyle**|Determina cómo se generan los nombres únicos para las jerarquías contenidas en la dimensión de cubo. Esta propiedad puede tener los valores siguientes:<br /><br /> **IncludeDimensionName**:<br />                    El nombre de la dimensión se incluye como parte del nombre de la jerarquía. Es el valor predeterminado.<br /><br /> **ExcludeDimensionName**:<br />                    El nombre de la dimensión no se incluye como parte del nombre de la jerarquía.|  
|**ID**|Contiene el identificador único de la dimensión de cubo.|  
|**MemberUniqueNameStyle**|Determina cómo se generan los nombres únicos para los miembros de las jerarquías contenidas en la dimensión de cubo. Esta propiedad puede tener los valores siguientes:<br /><br /> **Native**:<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina automáticamente los nombres únicos de los miembros. Es el valor predeterminado.<br /><br /> **NamePath**: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un nombre compuesto formado por el nombre de cada nivel y el título del miembro.|  
|**Nombre**|Contiene el nombre descriptivo de la dimensión de cubo. De forma predeterminada, el nombre de una dimensión de cubo coincide con el nombre de la dimensión de base de datos, a no ser que se haya definido previamente otra dimensión de cubo con el mismo nombre.|  
|**Visible**|Determina si la dimensión de cubo es visible. El valor predeterminado es **True**.|  
  
## <a name="see-also"></a>Vea también  
 [Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
