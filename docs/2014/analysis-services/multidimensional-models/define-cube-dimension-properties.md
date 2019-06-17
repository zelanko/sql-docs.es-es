---
title: Definir las propiedades de dimensión de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], characteristics
- properties [Analysis Services], dimensions
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecf47eff045aa379a8e67332a82b2045a8569a2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075691"
---
# <a name="define-cube-dimension-properties"></a>Definir las propiedades de una dimensión de cubo
  Una dimensión de cubo es una instancia de una dimensión de base de datos en un cubo. Se puede utilizar una dimensión de base de datos en varios cubos y se pueden basar varias dimensiones de cubo en una sola dimensión de base de datos. En la siguiente tabla se describen las propiedades de una dimensión de cubo.  
  
|Property|Descripción|  
|--------------|-----------------|  
|`AllMemberAggregationUsage`|Controla cómo se diseñan las agregaciones en el Diseñador de agregaciones, en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Esta propiedad puede tener los valores siguientes:<br /><br /> **Full**: Todas las agregaciones del cubo deben incluir el miembro All.<br /><br /> **Ninguno**: Ninguna agregación del cubo puede incluir al miembro All. Este es el valor predeterminado.<br /><br /> **Unrestricted**: No se aplica ninguna restricción en el Diseñador de agregaciones.<br /><br /> **Default**: La misma funcionalidad que Unrestricted.|  
|`Description`|Proporciona un nombre descriptivo para el nivel.|  
|`DimensionID`|Contiene el identificador único de la dimensión de base de datos.|  
|`HierarchyUniqueNameStyle`|Determina cómo se generan los nombres únicos para las jerarquías contenidas en la dimensión de cubo. Esta propiedad puede tener los valores siguientes:<br /><br /> `IncludeDimensionName`: El nombre de la dimensión se incluye como parte del nombre de la jerarquía. Este es el valor predeterminado.<br /><br /> `ExcludeDimensionName`: El nombre de la dimensión no se incluye como parte del nombre de la jerarquía.|  
|`ID`|Contiene el identificador único de la dimensión de cubo.|  
|`MemberUniqueNameStyle`|Determina cómo se generan los nombres únicos para los miembros de las jerarquías contenidas en la dimensión de cubo. Esta propiedad puede tener los valores siguientes:<br /><br /> `Native`: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina automáticamente los nombres únicos de los miembros. Este es el valor predeterminado.<br /><br /> `NamePath`: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un nombre compuesto formado por el nombre de cada nivel y el título del miembro.|  
|`Name`|Contiene el nombre descriptivo de la dimensión de cubo. De forma predeterminada, el nombre de una dimensión de cubo coincide con el nombre de la dimensión de base de datos, a no ser que se haya definido previamente otra dimensión de cubo con el mismo nombre.|  
|`Visible`|Determina si la dimensión de cubo es visible. El valor predeterminado es `True`.|  
  
## <a name="see-also"></a>Vea también  
 [Dimensiones &#40;Analysis Services - Datos multidimensionales&#41;](../multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
