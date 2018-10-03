---
title: Tipo de datos DataBlock (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataBlock Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataBlock
helpviewer_keywords:
- DataBlock data type
ms.assetid: 4192b388-613a-472b-881c-f9c02215aa81
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 706b934c51d280ec588bedf3752d61a4cc46697d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082595"
---
# <a name="datablock-data-type-assl"></a>Tipo de datos DataBlock (ASSL)
  Define un tipo de datos primitivo que representa una colección de bloques de datos que se usa para almacenar el contenido binario de un [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataBlock>  
   <Blocks>...</Blocks>  
</DataBlock>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos básicos|None|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[Bloques](../collections/blocks-element-assl.md)|  
|Elementos derivados|[Datos](../objects/data-element-assl.md) elemento de [ClrAssemblyFile](clrassemblyfile-data-type-assl.md) tipo ([archivos](../collections/files-element-assl.md) colección de [ClrAssembly](assembly-data-type-assl.md) tipo)|  
  
## <a name="see-also"></a>Vea también  
 [Elemento Assembly &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Elemento file &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [Bloquear elemento &#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
