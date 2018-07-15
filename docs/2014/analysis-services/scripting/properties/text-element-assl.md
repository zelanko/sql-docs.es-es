---
title: Elemento Text (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Text Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- text
helpviewer_keywords:
- Text element
ms.assetid: 0edece73-236f-4661-8102-3fcc29326bf4
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26eebe93b7bdf9662011363a2023aaf9e4fe0efa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328425"
---
# <a name="text-element-assl"></a>Elemento Text (ASSL)
  Contiene el texto de un [comando](../objects/command-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Text>...</Text>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Command](../objects/command-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento que se corresponde con el elemento primario de `Text` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Command>.  
  
## <a name="see-also"></a>Vea también  
 [Comandos de elemento &#40;ASSL&#41;](../collections/commands-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
