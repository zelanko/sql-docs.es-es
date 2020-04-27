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
manager: craigg
ms.openlocfilehash: 0ace708cc4ee09295380b814bbf21f5a1c350974
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66075705"
---
# <a name="define-cube-hierarchy-properties"></a>Definir propiedades de las jerarquías de cubos
  Las propiedades de la jerarquía de cubo permiten especificar valores únicos para jerarquías definidas por el usuario en dimensiones de cubo basadas en la misma dimensión de base de datos. En la siguiente tabla se describen las propiedades de una jerarquía de cubo.  
  
|Propiedad|Descripción|  
|--------------|-----------------|  
|`Enabled`|Determina si está habilitada la jerarquía para la dimensión de cubo.|  
|`HierarchyID`|Contiene el identificador único de la jerarquía.|  
|`OptimizedState`|Determina el nivel de optimización que se aplica a la jerarquía. Esta propiedad puede tener los valores siguientes:<br /><br /> `FullyOptimized`: La instancia genera índices para la jerarquía, para mejorar el rendimiento de las consultas. Este es el valor predeterminado.<br /><br /> `NotOptimized`: La instancia no genera otros índices.|  
|`Visible`|Determina la visibilidad de la jerarquía de cubo. El valor predeterminado es `True`.|  
  
## <a name="see-also"></a>Consulte también  
 [Jerarquías de usuario](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
