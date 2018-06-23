---
title: Tipo de elemento (PerspectiveCalculation) (ASSL) | Documentos de Microsoft
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
api_name:
- Type Element (PerspectiveCalculation)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: d7b87aea-3265-4f3c-a7ee-4f3e90f9a0b7
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 242d4d779da87c155371047fd2bb21128da51abf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108186"
---
# <a name="type-element-perspectivecalculation-assl"></a>Elemento Type (PerspectiveCalculation) (ASSL)
  Indica el tipo de la [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<PerspectiveCalculation>  
   ...  
   <Type>...</Type>  
   ...  
</PerspectiveCalculation>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Miembro*|miembro calculado|  
|*conjunto*|Conjunto con nombre|  
  
 La enumeración que corresponde a los valores permitidos para `Type` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.PerspectiveCalculationType>.  
  
 El elemento que corresponde al elemento primario de `Type` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.PerspectiveCalculation>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  