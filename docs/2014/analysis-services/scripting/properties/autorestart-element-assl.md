---
title: Elemento AutoRestart (ASSL) | Microsoft Docs
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
- AutoRestart Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AutoRestart
helpviewer_keywords:
- AutoRestart element
ms.assetid: 4c6a0e40-8e13-4d63-bf98-9470ffe95d02
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecb6893c7c3e87c9e96890a917bbe8aad540433d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159106"
---
# <a name="autorestart-element-assl"></a>Elemento AutoRestart (ASSL)
  Determina si un [seguimiento](../objects/trace-element-assl.md) elemento debe reiniciarse automáticamente si el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] servicio se detiene y reinicia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Trace>  
   ...  
   <AutoRestart>...</AutoRestart>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|`False`|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Seguimiento](../objects/trace-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento que se corresponde con el elemento primario de `AutoRestart` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Vea también  
 [Realiza un seguimiento de elemento &#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
