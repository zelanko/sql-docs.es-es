---
title: Elemento ErrorConfiguration (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ErrorConfiguration Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ErrorConfiguration
helpviewer_keywords:
- ErrorConfiguration element
ms.assetid: e8363ec2-fbbf-48f6-a55d-01793afa759c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 07b55794f3e5de70d4f515ed8f905e02a04787ee
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225071"
---
# <a name="errorconfiguration-element-assl"></a>Elemento ErrorConfiguration (ASSL)
  Especifica los valores para administrar errores que se pueden producir cuando se procesa el elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube> <!-- or Dimension, MeasureGroup, MiningStructure, Partition -->  
   ...  
   <ErrorConfiguration>  
      <KeyErrorLimit>...</KeyErrorLimit>  
      <KeyErrorLogFile>...</KeyErrorLogFile>  
      <KeyErrorAction>...</KeyErrorAction>  
      <KeyErrorLimitAction>...</KeyErrorLimitAction>  
      <KeyNotFound>...</KeyNotFound>  
      <KeyDuplicate>...</KeyDuplicate>  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
      <NullKeyNotAllowed>...<NullKeyNotAllowed>  
   </ErrorConfiguration>  
   ...  
</Cube >  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cubo](cube-element-assl.md), [dimensión](dimension-element-assl.md), [MeasureGroup](group-element-assl.md), [MiningStructure](miningstructure-element-assl.md), [partición](partition-element-assl.md)|  
|Elementos secundarios|[KeyDuplicate](../properties/keyduplicate-element-assl.md), [KeyErrorAction](action-element-assl.md), [KeyErrorLimit](../properties/keyerrorlimit-element-assl.md), [KeyErrorLimitAction](../properties/keyerrorlimitaction-element-assl.md), [KeyErrorLogFile](file-element-assl.md), [ KeyNotFound](../properties/keynotfound-element-assl.md), [NullKeyConvertedToUnknown](../properties/nullkeyconvertedtounknown-element-assl.md), [NullKeyNotAllowed](../properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ErrorConfiguration>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
