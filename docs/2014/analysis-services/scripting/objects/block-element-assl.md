---
title: Bloquear elemento (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Block Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Block
helpviewer_keywords:
- Block element
ms.assetid: f45c32ae-e4e0-465a-9564-9ccfb10a858f
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e382ba38c41bc68b3d49b0397cdc3fe3f2dcf0ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196732"
---
# <a name="block-element-assl"></a>Elemento Block (ASSL)
  Contiene todo o parte del contenido binario de un [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Blocks>  
   <Block>...</Block>  
</Blocks>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Base64Binary|  
|Valor predeterminado|None|  
|Cardinalidad|1-n: Elemento necesario que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Bloques](../collections/blocks-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="see-also"></a>Vea también  
 [Assembly (elemento) &#40;ASSL&#41;](assembly-element-assl.md)   
 [Tipo de datos ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Archivos elemento &#40;ASSL&#41;](../collections/files-element-assl.md)   
 [Elemento file &#40;ASSL&#41;](file-element-assl.md)   
 [Tipo de datos ClrAssemblyFile &#40;ASSL&#41;](../data-type/clrassemblyfile-data-type-assl.md)   
 [Elemento de datos &#40;ASSL&#41;](data-element-assl.md)   
 [Tipo de datos DataBlock &#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  