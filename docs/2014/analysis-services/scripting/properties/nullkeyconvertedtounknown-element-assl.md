---
title: Elemento NullKeyConvertedToUnknown (ASSL) | Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cebeef3421533b429a38f6c5696780cb008eca69
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37316925"
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
 Los errores de conversión nulos tienen lugar cuando se detecta un valor nulo en una columna de clave que se interpreta como el miembro `Unknown`. Sin embargo, este error se produce solo si el [NullProcessing](nullprocessing-element-assl.md) (elemento) para el [DataItem](../data-type/dataitem-data-type-assl.md) antecesor de la `ErrorConfiguration` elemento primario se establece en *UnknownMember*.  
  
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
  
  
