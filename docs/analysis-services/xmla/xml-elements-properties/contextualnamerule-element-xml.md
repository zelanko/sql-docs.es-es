---
title: Elemento ContextualNameRule (XML) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: eb567ef8-f412-4d34-837a-75e53b88b3ce
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ec3b0b9d396f16f13943eb9d16461f5850466e6a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="contextualnamerule-element-xml"></a>Elemento ContextualNameRule (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Proporciona una sugerencia sobre la mejor manera de construir un nombre compuesto para el atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <ContextualNameRule>...</ContextualNameRule>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|-1|  
|Cardinalidad|0-1: elemento opcional que aparece una y solo una.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Proporciona una sugerencia a las aplicaciones cliente sobre cómo crear nombres inequívocos para este atributo.  
  
 El valor de la **ContextualNameRule** elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Ninguno*|Usar el nombre del atributo.|  
|*Contexto*|Usar el nombre de la relación entrante.|  
|*Mezcla*|Concatenar el nombre de la relación entrante y el del atributo siguiendo las reglas del lenguaje de la aplicación.|  
  
  
