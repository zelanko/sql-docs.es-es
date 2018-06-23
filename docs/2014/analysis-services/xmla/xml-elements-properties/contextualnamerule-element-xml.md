---
title: Elemento ContextualNameRule (XML) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: eb567ef8-f412-4d34-837a-75e53b88b3ce
caps.latest.revision: 7
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 6b3d4e8f8023814fb0080b5ba7d9196aad81afee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197689"
---
# <a name="contextualnamerule-element-xml"></a>Elemento ContextualNameRule (XML)
  Proporciona una sugerencia sobre la mejor manera de construir un nombre compuesto para el atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <ContextualNameRule>...</ContextualNameRule>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|-1|  
|Cardinalidad|0-1: elemento opcional que aparece una y solo una.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Proporciona una sugerencia a las aplicaciones cliente sobre cómo crear nombres inequívocos para este atributo.  
  
 El valor del elemento `ContextualNameRule` se limita a las cadenas listadas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Ninguno*|Usar el nombre del atributo.|  
|*Contexto*|Usar el nombre de la relación entrante.|  
|*Mezcla*|Concatenar el nombre de la relación entrante y el del atributo siguiendo las reglas del lenguaje de la aplicación.|  
  
  