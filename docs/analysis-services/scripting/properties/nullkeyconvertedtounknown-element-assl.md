---
title: Elemento NullKeyConvertedToUnknown (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 95f8a31e4600b73901d692ca7472759a681d9006
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="nullkeyconvertedtounknown-element-assl"></a>Elemento NullKeyConvertedToUnknown (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Especifica la acción que se ha de llevar a cabo si se encuentra un error de conversión nulo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*IgnoreError*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Los errores de conversión nulos tienen lugar cuando se detecta un valor nulo en una columna de clave que se interpreta como el miembro **Unknown** . Sin embargo, este error se produce solo si la [NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md) (elemento) para la [DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md) antecesor de la **ErrorConfiguration** elemento primario se establece en  *UnknownMember*.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*IgnoreError*|El procesamiento omite el error y continúa.|  
|*ReportAndContinue*|El procesamiento notifica el error y continúa.|  
|*ReportAndStop*|El procesamiento informa del error y se detiene.|  
  
 La enumeración que corresponde a los valores permitidos para **NullKeyConvertedToUnknown** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Vea también  
 [ErrorConfiguration, elemento & #40; ASSL & #41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
