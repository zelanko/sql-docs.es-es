---
title: Bloquea el elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Blocks Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Blocks
helpviewer_keywords:
- Blocks element
ms.assetid: d6fd4e6b-b5bd-43cd-9c28-48af57cf977c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b1030bf5efbfb86319d83a19913f58d834f85fc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082725"
---
# <a name="blocks-element-assl"></a>Elemento Blocks (ASSL)
  Contiene la colección de bloques de datos binarios que representan el contenido binario de un [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Data xsi:type="DataBlock">  
   ...  
   <Blocks>  
      <Block>...</Block>  
   </Blocks>  
   ...  
</File>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Datos](../objects/data-element-assl.md) typu [DataBlock](../data-type/datablock-data-type-assl.md)|  
|Elementos secundarios|[Bloque](../objects/block-element-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `Blocks` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ClrAssemblyFile>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Assembly &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Tipo de datos ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Archivos elemento &#40;ASSL&#41;](files-element-assl.md)   
 [Elemento file &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [Tipo de datos ClrAssemblyFile &#40;ASSL&#41;](../data-type/clrassemblyfile-data-type-assl.md)   
 [Elemento de datos &#40;ASSL&#41;](../objects/data-element-assl.md)   
 [Tipo de datos DataBlock &#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [Elemento Blocks](blocks-element-assl.md)   
 [Bloquear elemento &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Colecciones &#40;ASSL&#41;](collections-assl.md)  
  
  
