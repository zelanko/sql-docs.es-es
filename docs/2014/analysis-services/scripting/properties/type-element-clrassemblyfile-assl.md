---
title: Tipo de elemento (ClrAssemblyFile) (ASSL) | Documentos de Microsoft
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
- Type Element (ClrAssemblyFile)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ab9e1e2c-ab06-4cd1-b007-16d738dc5604
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c253b2975c5e4f4cbf27c5b2d655a09617d644de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103402"
---
# <a name="type-element-clrassemblyfile-assl"></a>Elemento Type (ClrAssemblyFile) (ASSL)
  Especifica el tipo de archivo de uno de los archivos que pertenecen a un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ensamblado de .NET Framework.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ClrAssemblyFile>  
      ...  
      <Type>...</Type>  
   ...  
</ClrAssemblyFile>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El valor de este elemento se limita a una de las cadenas siguientes:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Main*|El archivo especificado es el archivo principal del ensamblado.|  
|*Dependientes*|El archivo especificado es un archivo dependiente del ensamblado.|  
|*Depuración*|El archivo especificado contiene información de depuración.|  
  
 La enumeración que corresponde a los valores permitidos para `Type` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ClrAssemblyFileType>.  
  
 El elemento que corresponde al elemento primario de `Type` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.ClrAssemblyFile>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento file &#40;ASSL&#41;](../objects/file-element-assl.md)   
 [Archivos elemento &#40;ASSL&#41;](../collections/files-element-assl.md)   
 [Tipo de datos ClrAssembly &#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Assembly (elemento) &#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Elemento Assemblies &#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  