---
title: Elemento KeyErrorLimit (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- KeyErrorLimit Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyErrorLimit
helpviewer_keywords:
- KeyErrorLimit element
ms.assetid: c91d3bd8-2ad7-416f-a860-2599e4a4dbee
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42c796878560bdc905b40e61e18d67ec075810da
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225985"
---
# <a name="keyerrorlimit-element-assl"></a>Elemento KeyErrorLimit (ASSL)
  Contiene el número de errores aceptable durante el procesamiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyErrorLimit>...</KeyErrorLimit>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Long|  
|Valor predeterminado|`0`|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `KeyErrorLimit` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ErrorConfiguration>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
