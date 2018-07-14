---
title: Definir las propiedades de jerarquía de cubo | Microsoft Docs
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
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9ebe3b4a45791a9e5a9e136fed4e228666c8e49e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289822"
---
# <a name="define-cube-hierarchy-properties"></a>Definir propiedades de las jerarquías de cubos
  Las propiedades de la jerarquía de cubo permiten especificar valores únicos para jerarquías definidas por el usuario en dimensiones de cubo basadas en la misma dimensión de base de datos. En la siguiente tabla se describen las propiedades de una jerarquía de cubo.  
  
|Property|Descripción|  
|--------------|-----------------|  
|`Enabled`|Determina si está habilitada la jerarquía para la dimensión de cubo.|  
|`HierarchyID`|Contiene el identificador único de la jerarquía.|  
|`OptimizedState`|Determina el nivel de optimización que se aplica a la jerarquía. Esta propiedad puede tener los valores siguientes:<br /><br /> `FullyOptimized`: La instancia genera índices para la jerarquía mejorar el rendimiento de las consultas. Este es el valor predeterminado.<br /><br /> `NotOptimized`: La instancia no genera otros índices.|  
|`Visible`|Determina la visibilidad de la jerarquía de cubo. El valor predeterminado es `True`.|  
  
## <a name="see-also"></a>Vea también  
 [Jerarquías de usuario](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
