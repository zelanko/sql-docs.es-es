---
title: Elemento Usage (MiningModelColumn) (ASSL) | Documentos de Microsoft
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
- Usage Element (MiningModelColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Usage
helpviewer_keywords:
- Usage element
ms.assetid: 435a857e-37a9-434e-9de1-354f1ff2993f
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4a4e4c2b11a9a9281f64062390257bf5ddf3145b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199440"
---
# <a name="usage-element-miningmodelcolumn-assl"></a>Elemento Usage (MiningModelColumn) (ASSL)
  Describe cómo la columna asociada en el elemento primario [MiningStructure](../objects/miningstructure-element-assl.md) se utiliza.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<MiningModelColumn>  
   ...  
   <Usage>...</Usage>  
   ...  
</MiningModelColumn>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Key*|La columna es una columna de clave.|  
|*Entrada*|La columna es una columna de entrada.|  
|*Predict*|La columna es una columna de predicción.|  
|*PredictOnly*|La columna es solo una columna de predicción.|  
|*Ninguno*|El modelo no utiliza la columna. **Advertencia:** cuando el valor de uso es "None", Analysis Services no envía ningún valor para el servidor de forma predeterminada; por lo tanto, el atributo de uso no está incluido en la solicitud/respuesta.|  
  
 La enumeración que corresponde a los valores permitidos para `Usage` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.MiningModelColumnUsages>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  