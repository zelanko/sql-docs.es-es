---
title: Dar formato a elementos (ASSL) | Documentos de Microsoft
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
- Format Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Format
helpviewer_keywords:
- Format element
ms.assetid: 881ea707-52a7-46f7-ba16-ac2ec44eca22
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b7434ba5d6e2db8d2a2e665fa333799b6b2e9eb8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201693"
---
# <a name="format-element-assl"></a>Elemento Format (ASSL)
  Contiene el formato requerido de la [DataItem](../data-type/dataitem-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataItem>  
   ...  
   <Format>...</Format>  
      ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Elemento de datos](../data-type/dataitem-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Valores permitidos para el `Format` elemento son los formatos de Microsoft Office Excel así como las cadenas *TrimRight*, *TrimLeft*, *TrimAll*, y  *TrimNone*. *TrimRight* es el valor predeterminado para el proceso de recorte.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|Cualquier cadena de formato de Excel|Se da formato a los datos de acuerdo con la cadena de formato con nombre o personalizada que se haya especificado. Es posible especificar cualquier cadena de formato que admita Excel.|  
|*TrimAll*|Los datos se recortan por la izquierda y por la derecha.|  
|*TrimLeft*|Los datos se recortan por la izquierda.|  
|*TrimNone*|No se recortan los datos.|  
|*TrimRight*|Los datos se recortan por la derecha.|  
  
 El elemento que corresponde al elemento primario de `Format` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DataItem>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  