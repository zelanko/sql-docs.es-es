---
title: Definir propiedades de la jerarquía de cubo | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5e91bbb6bdc5ef6e84653d69fc26e4caa18c9f37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="define-cube-hierarchy-properties"></a>Definir propiedades de las jerarquías de cubos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Las propiedades de la jerarquía de cubo permiten especificar valores únicos para jerarquías definidas por el usuario en dimensiones de cubo basadas en la misma dimensión de base de datos. En la siguiente tabla se describen las propiedades de una jerarquía de cubo.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**Habilitado**|Determina si está habilitada la jerarquía para la dimensión de cubo.|  
|**HierarchyID**|Contiene el identificador único de la jerarquía.|  
|**OptimizedState**|Determina el nivel de optimización que se aplica a la jerarquía. Esta propiedad puede tener los valores siguientes:<br /><br /> **FullyOptimized**:<br />                    La instancia genera índices para la jerarquía, para mejorar el rendimiento de las consultas. Es el valor predeterminado.<br /><br /> **NotOptimized**:<br />                    La instancia no genera otros índices.|  
|**Visible**|Determina la visibilidad de la jerarquía de cubo. El valor predeterminado es **True**.|  
  
## <a name="see-also"></a>Vea también  
 [Jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  
