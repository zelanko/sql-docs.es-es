---
title: Definir las propiedades de jerarquía de cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], cubes
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b064db7ff0e496ea7a46085825afc202fced605
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087325"
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
  
  
