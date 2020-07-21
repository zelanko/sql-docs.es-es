---
title: Definir propiedades de jerarquía de cubos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8903a49754357aad9cf24ee63fffa45fbf120e4d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546997"
---
# <a name="define-cube-hierarchy-properties"></a>Definir propiedades de las jerarquías de cubos
  Las propiedades de la jerarquía de cubo permiten especificar valores únicos para jerarquías definidas por el usuario en dimensiones de cubo basadas en la misma dimensión de base de datos. En la siguiente tabla se describen las propiedades de una jerarquía de cubo.  
  
|Propiedad.|Descripción|  
|--------------|-----------------|  
|`Enabled`|Determina si está habilitada la jerarquía para la dimensión de cubo.|  
|`HierarchyID`|Contiene el identificador único de la jerarquía.|  
|`OptimizedState`|Determina el nivel de optimización que se aplica a la jerarquía. Esta propiedad puede tener los valores siguientes:<br /><br /> `FullyOptimized`: La instancia genera índices para la jerarquía, para mejorar el rendimiento de las consultas. Este es el valor predeterminado.<br /><br /> `NotOptimized`: La instancia no genera otros índices.|  
|`Visible`|Determina la visibilidad de la jerarquía de cubo. El valor predeterminado es `True`.|  
  
## <a name="see-also"></a>Consulte también  
 [Jerarquías de usuario](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
