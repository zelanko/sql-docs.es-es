---
title: Elemento IsDefaultImage (XML) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: e29cd137-af82-4753-a681-0d3e705513f3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0821c2dfaa25f3d9a557663046db0405aca0cb24
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201375"
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
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
  
## <a name="remarks"></a>Comentarios  
 Para los elementos `RelationshipEndVisualizationProperties`, el elemento `IsDefaultImage` indica que la imagen predeterminada para esta entidad puede obtenerse navegando al otro extremo de esta relación. El valor predeterminado `false` indica que no se va a obtener ninguna imagen predeterminada.  
  
  
