---
title: Elemento IsDefaultMeasure (XML) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 523cf3d7-9df0-4f9d-8486-9109de8d3cca
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: a4229507c856d511b805a249b162516d8b11feb6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106622"
---
# <a name="isdefaultmeasure-element-xml"></a>Elemento IsDefaultMeasure (XML)
  Indica que es posible obtener la medida predeterminada de esta entidad navegando por esta relación hasta la otra tabla y capturando el miembro que tiene el atributo, DefaultMeasure.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
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
 Para los elementos `RelationshipEndVisualizationProperties`, el elemento `IsDefaultMeasure` indica que es posible obtener la medida predeterminada de esta entidad navegando hasta el otro extremo de esta relación. El valor predeterminado `false` indica que no se va a obtener ninguna medida predeterminada.  
  
  