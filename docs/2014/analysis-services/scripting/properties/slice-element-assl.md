---
title: Slice (ASSL) del elemento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Slice Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Slice
helpviewer_keywords:
- Slice element
ms.assetid: 2c8c4107-c641-4724-bfa5-0c47e0ec8888
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84bcab815ec93feae3b997c0341bb8c59012cb17
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169735"
---
# <a name="slice-element-assl"></a>Elemento Slice (ASSL)
  Contiene una expresión MDX (Expresiones multidimensionales) que define el segmento incluido en una partición.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Partition>  
      ...  
   <Slice>...</Slice>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Partición](../objects/partition-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `Slice` contiene una expresión de tupla de MDX o expresión de conjunto que identifica la parte del cubo para la que la partición almacena información. La expresión MDX es similar a la [StrToSet](/sql/mdx/strtoset-mdx) función MDX con la palabra clave CONSTRAINED, en que la expresión no puede incluir MDX o funciones definidas por el usuario.  
  
 El elemento que se corresponde con el elemento primario de `Slice` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
