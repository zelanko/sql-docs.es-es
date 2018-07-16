---
title: Elemento LogFileRollover (ASSL) | Microsoft Docs
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
- LogFileRollover Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileRollover
helpviewer_keywords:
- LogFileRollover element
ms.assetid: 5484e167-b891-431a-bbae-946ea6eb4a3c
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12ed8df0217baeb5f760273ad6998e2344f4fbb8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299025"
---
# <a name="logfilerollover-element-assl"></a>Elemento LogFileRollover (ASSL)
  Especifica si el registro de [seguimiento](../objects/trace-element-assl.md) salida debería escribirse en un archivo nuevo o debería detenerse en el archivo de registro máximo tamaño especificado en [LogFileSize](logfilesize-element-assl.md) se alcanza.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Trace>  
   ...  
   <LogFileRollover>...</LogFileRollover>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|False|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Seguimiento](../objects/trace-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Si el valor del elemento `LogFileRollover` está establecido en True, se inicia un nuevo archivo cuando el tamaño del archivo de registro supera el valor especificado en el elemento `LogFileSize` del elemento primario `Trace`; de lo contrario, se detiene el registro.  
  
 El elemento que se corresponde con el elemento primario de `LogFileRollover` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Trace>.  
  
## <a name="see-also"></a>Vea también  
 [Realiza un seguimiento de elemento &#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
