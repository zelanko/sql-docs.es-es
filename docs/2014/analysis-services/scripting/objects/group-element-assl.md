---
title: Grupo de elemento (ASSL) | Documentos de Microsoft
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
api_name:
- Group Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- GROUP
helpviewer_keywords:
- Group element
ms.assetid: 7df4ba90-b39f-4d8a-8db1-b73639a522a6
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6b10e557c91a27305ca0b9bff1d989e327b3b6f7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106201"
---
# <a name="group-element-assl"></a>Elemento Group (ASSL)
  Define un grupo de miembros enlazados a un atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Groups>  
   <Group>  
      <Name>...</Name>  
      <Members>...</Members>  
   </Group>  
<Groups/>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-n: Elemento necesario que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Grupos](../collections/groups-element-assl.md)|  
|Elementos secundarios|[Members](../collections/members-element-assl.md), [Name](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Group>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos UserDefinedGroupBinding &#40;ASSL&#41;](../data-type/binding-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  