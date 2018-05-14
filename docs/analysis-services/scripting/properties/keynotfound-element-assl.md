---
title: Elemento KeyNotFound (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bfce07b37bd43b18c769212f7647ec311fec4fa3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="keynotfound-element-assl"></a>Elemento KeyNotFound (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Especifica cómo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] responde cuando encuentra un error de integridad referencial.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyNotFound>...</KeyNotFound>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*ReportAndContinue*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Los errores de integridad referencial tienen lugar cuando un valor de clave externa en una tabla dependiente no tiene una entrada correspondiente en la tabla primaria. Este error se produce cuando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procesa una dimensión en la que la tabla de hechos hace referencia a un valor de clave externa que no existe en la tabla de dimensiones para esa dimensión, o cuando [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procesa una partición cuando la tabla principal de dimensiones para una dimensión que está incluida en la partición hace referencia a un valor de clave que no existe en otra tabla de dimensiones asociada. (En cuanto a las dimensiones con jerarquías de elementos primarios y secundarios y atributos primarios, esto también puede ocurrir cuando la tabla principal de dimensiones que está incluida en la partición hace referencia a un valor de clave que no existe en la misma tabla de dimensiones asociada.)  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*IgnoreError*|El procesamiento debe omitir el error y continuar.|  
|*ReportAndContinue*|El procesamiento debe notificar el error y continuar.|  
|*ReportAndStop*|El procesamiento debe notificar el error y detenerse.|  
  
 La enumeración que corresponde a los valores permitidos para **KeyNotFound** en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ErrorOption>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
