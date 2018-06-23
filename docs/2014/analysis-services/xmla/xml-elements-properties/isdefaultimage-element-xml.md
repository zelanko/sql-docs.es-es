---
title: Elemento IsDefaultImage (XML) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e29cd137-af82-4753-a681-0d3e705513f3
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: c4d15ea9048c83b1579b688f6848e48deb1dffe4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107719"
---
# <a name="isdefaultimage-element-xml"></a>Elemento IsDefaultImage (XML)
  Indica que es posible obtener la imagen predeterminada de esta entidad navegando por esta relación hasta la otra tabla y capturando el miembro que tiene el atributo, IsDefaultImage.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultImage>...</IsDefaultImage>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|false|  
|Cardinalidad|0-1: elemento opcional que aparece una y solo una.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para los elementos `RelationshipEndVisualizationProperties`, el elemento `IsDefaultImage` indica que la imagen predeterminada para esta entidad puede obtenerse navegando al otro extremo de esta relación. El valor predeterminado `false` indica que no se va a obtener ninguna imagen predeterminada.  
  
  