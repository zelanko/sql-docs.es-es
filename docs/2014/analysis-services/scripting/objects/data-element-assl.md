---
title: Elemento Data (ASSL) | Microsoft Docs
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
- Data Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Data
helpviewer_keywords:
- Data element
ms.assetid: e52b1961-7e11-4029-8ab1-84d275845067
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b31922593446e7d8aafd88cdb5667bef8b109ba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218285"
---
# <a name="data-element-assl"></a>Elemento Data (ASSL)
  Contiene (en la colección del elemento secundario [elemento Block &#40;ASSL&#41; ](block-element-assl.md) elementos) el contenido binario de un [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<File xsi:type="ClrAssemblyFile">  
   ...  
   <Data xsi:type="DataBlock">...</Data>  
   ...  
</ClrAssemblyFile>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|[DataBlock](../data-type/datablock-data-type-assl.md)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Archivo](file-element-assl.md) typu [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento que se corresponde con el elemento primario de `Data` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ClrAssemblyFile>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Assembly &#40;ASSL&#41;](assembly-element-assl.md)   
 [Tipo de datos ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Archivos elemento &#40;ASSL&#41;](../collections/files-element-assl.md)   
 [Bloquea el elemento &#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [Objetos &#40;ASSL&#41;](objects-assl.md)  
  
  
