---
title: "Definir propiedades de las jerarqu&#237;as de cubos | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "jerarquías [Analysis Services], varios niveles"
  - "jerarquías [Analysis Services], cubos"
ms.assetid: 819d0a4e-7815-4332-a605-b07ca2ade6ac
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 18
---
# Definir propiedades de las jerarqu&#237;as de cubos
  Las propiedades de la jerarquía de cubo permiten especificar valores únicos para jerarquías definidas por el usuario en dimensiones de cubo basadas en la misma dimensión de base de datos. En la siguiente tabla se describen las propiedades de una jerarquía de cubo.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|**Habilitado**|Determina si está habilitada la jerarquía para la dimensión de cubo.|  
|**HierarchyID**|Contiene el identificador único de la jerarquía.|  
|**OptimizedState**|Determina el nivel de optimización que se aplica a la jerarquía. Esta propiedad puede tener los valores siguientes:<br /><br /> **FullyOptimized**:<br />                    La instancia genera índices para la jerarquía, para mejorar el rendimiento de las consultas. Es el valor predeterminado.<br /><br /> **NotOptimized**:<br />                    La instancia no genera otros índices.|  
|**Visible**|Determina la visibilidad de la jerarquía de cubo. El valor predeterminado es **True**.|  
  
## Vea también  
 [Jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)  
  
  