---
title: Elemento IsDefaultImage (XML) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e29cd137-af82-4753-a681-0d3e705513f3
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed09bbccf5bb5aa399fbab0c9e6a58c7f58c7ecd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

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
|Tipo y longitud de los datos|Booleano|  
|Valor predeterminado|false|  
|Cardinalidad|0-1: elemento opcional que aparece una y solo una.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para **RelationshipEndVisualizationProperties** elementos, el **IsDefaultImage** elemento indica que la imagen predeterminada para esta entidad puede obtenerse navegando al otro extremo de este relación. El valor predeterminado de **false** indica que no hay ninguna imagen predeterminada va a obtener.  
  
  

