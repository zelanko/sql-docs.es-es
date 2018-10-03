---
title: Elemento (ASSL) del comando | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Command Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Command
helpviewer_keywords:
- Command element
ms.assetid: 277598b5-9939-4d7f-8c75-06470c3fabdd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 67b66d4492660cdc17e5e26801b6ef4e03488981
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48063175"
---
# <a name="command-element-assl"></a>Elemento Command (ASSL)
  Define un comando que está disponible para su uso dentro del contexto del elemento primario de la [comandos](../collections/commands-element-assl.md) colección.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Commands>  
   <Command>  
      <Text>...</Text>  
   </Command>  
</Commands >  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Comandos](../collections/commands-element-assl.md)|  
|Elementos secundarios|[Texto](../properties/text-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.Command>.  
  
## <a name="see-also"></a>Vea también  
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
