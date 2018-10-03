---
title: Archivo de elemento (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- File Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- File
helpviewer_keywords:
- File element
ms.assetid: 21c70707-d2f8-4040-9acb-cbce23076bcc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef9527346b0627d6ba414f9535c00e22a4d59ea6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169825"
---
# <a name="file-element-assl"></a>Elemento File (ASSL)
  Define uno de los archivos que componen un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] [ClrAssembly](../data-type/assembly-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Files>  
   <File xsi:type="ClrAssemblyFile">...</File>  
</Files>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|1-n: Elemento necesario que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Archivos](../collections/files-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento que se corresponde con el elemento primario de `Files` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ClrAssemblyFile>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Server &#40;ASSL&#41;](server-element-assl.md)   
 [Elemento de la base de datos &#40;ASSL&#41;](database-element-assl.md)   
 [Elemento Assemblies &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Elemento Assembly &#40;ASSL&#41;](assembly-element-assl.md)   
 [Tipo de datos ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Elemento de datos &#40;ASSL&#41;](data-element-assl.md)   
 [Tipo de datos DataBlock &#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [Bloquea el elemento &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [Bloquear elemento &#40;ASSL&#41;](block-element-assl.md)   
 [Tipo de datos ComAssembly &#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
