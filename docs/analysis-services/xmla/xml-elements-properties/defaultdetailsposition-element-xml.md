---
title: Elemento DefaultDetailsPosition (XML) | Documentos de Microsoft
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
ms.assetid: 851ad331-aefd-4277-a5e5-e32a8f5c5e22
caps.latest.revision: 6
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e72d34abbe3291010d568d6a7fa7d4bfb23e774d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="defaultdetailsposition-element-xml"></a>Elemento DefaultDetailsPosition (XML)
  Contiene información sobre la posición del elemento en una colección de elementos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <DefaultDetailsPosition>...</DefaultDetailsPosition>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Integer|  
|Valor predeterminado|-1|  
|Cardinalidad|0-1: elemento opcional que aparece una y solo una.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[RelationshipEndVisualizationProperties](../../../analysis-services/scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para **RelationshipEndVisualizationProperties** elementos, el **DefaultDetailsPosition** elemento contiene la posición del elemento de detalle predeterminado de una colección de detalles. El valor predeterminado de **false** indica que no hay ningún detalle predeterminado que se usará.  
  
  

