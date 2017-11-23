---
title: Elemento KeyNotFound (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: KeyNotFound Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: KeyNotFound
helpviewer_keywords: KeyNotFound element
ms.assetid: 2a93bbfa-2409-4e94-8b68-926532895a4c
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 72ebb26afc343b771e32087e9d68f4978cdaedc8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="keynotfound-element-assl"></a>Elemento KeyNotFound (ASSL)
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
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
