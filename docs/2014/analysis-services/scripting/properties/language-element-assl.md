---
title: Elemento Language (ASSL) | Microsoft Docs
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
- Language Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LANGUAGE
helpviewer_keywords:
- Language element
ms.assetid: 4d745d23-6b1f-4a85-97cf-d034cc41356f
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 738403bedd7a9da120e5ba706eabe4848f7e1e2b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293248"
---
# <a name="language-element-assl"></a>Elemento Language (ASSL)
  Contiene el identificador de lenguaje del elemento primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube> <!-- or Database, Dimension, MiningModel, MiningStructure, Translation -->  
   ...  
   <Language>...</Language>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Integer|  
|Valor predeterminado|None|  
  
 **Cardinalidad**  
  
|Antecesor o elemento primario|Cardinalidad|  
|------------------------|-----------------|  
|[Traducción](../objects/translation-element-assl.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|Todos las demás|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cubo](../objects/cube-element-assl.md), [base de datos](../objects/database-element-assl.md), [dimensión](../objects/dimension-element-assl.md), [MiningModel](../objects/miningmodel-element-assl.md), [MiningStructure](../objects/miningstructure-element-assl.md), [traducción](../objects/translation-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento `Language` contiene el identificador de idioma predeterminado que utiliza el elemento primario o el identificador de lenguaje específico de un elemento `Translation`. El idioma se debería definir utilizando los códigos del identificador de configuración regional (LCID). Por ejemplo, LCID 1033 se utiliza para indicar el idioma inglés (EE.UU.).  
  
 Los elementos que corresponden a los elementos primarios del elemento `Language` en el modelo de objetos Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningStructure> y <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
