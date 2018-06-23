---
title: Elemento NullKeyConvertedToUnknown (ASSL) | Documentos de Microsoft
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
- NullKeyConvertedToUnknown Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullKeyConvertedToUnknown
helpviewer_keywords:
- NullKeyConvertedToUnknown element
ms.assetid: 1a6cde33-01ba-4095-b464-16d1ad3c6905
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8e11f7de1b3fa7b11774a960351a1b3c974ce4f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204264"
---
# <a name="nullkeyconvertedtounknown-element-assl"></a>Elemento NullKeyConvertedToUnknown (ASSL)
  Especifica la acción que se ha de llevar a cabo si se encuentra un error de conversión nulo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*IgnoreError*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Los errores de conversión nulos tienen lugar cuando se detecta un valor nulo en una columna de clave que se interpreta como el miembro `Unknown`. Sin embargo, este error se produce solo si la [NullProcessing](nullprocessing-element-assl.md) (elemento) para la [DataItem](../data-type/dataitem-data-type-assl.md) antecesor de la `ErrorConfiguration` elemento primario se establece en *UnknownMember*.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*IgnoreError*|El procesamiento omite el error y continúa.|  
|*ReportAndContinue*|El procesamiento notifica el error y continúa.|  
|*ReportAndStop*|El procesamiento informa del error y se detiene.|  
  
 La enumeración que corresponde a los valores permitidos para `NullKeyConvertedToUnknown` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento ErrorConfiguration &#40;ASSL&#41;](../objects/errorconfiguration-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  