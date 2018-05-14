---
title: Elemento ContextualNameRule (XML) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: beb58b21c88bf5500ba7c15c336b866df59b0c7e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="contextualnamerule-element-xml"></a>Elemento ContextualNameRule (XML)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Proporciona una sugerencia sobre la mejor manera de construir un nombre compuesto para el atributo.  
  
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
  
|Value|Description|  
|-----------|-----------------|  
|*Ninguno*|Usar el nombre del atributo.|  
|*Contexto*|Usar el nombre de la relación entrante.|  
|*Mezcla*|Concatenar el nombre de la relación entrante y el del atributo siguiendo las reglas del lenguaje de la aplicación.|  
  
  
