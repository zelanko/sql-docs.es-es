---
title: Dimensión de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Dimension Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Dimension
- urn:schemas-microsoft-com:xml-analysis#Dimension
- microsoft.xml.analysis.dimension
helpviewer_keywords:
- Dimension element
ms.assetid: 85093468-e971-4b8e-9ee4-7b264ad01711
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1f20dfb338f1dd03923f8f71968f6c6f9f31bf80
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091135"
---
# <a name="dimension-element-xmla"></a>Elemento Dimension (XMLA)
  Identifica la dimensión de cubo representada por el elemento primario [objeto](object-element-dimension-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Object>  
   ...  
   <Dimension>...</Dimension>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Objeto](object-element-dimension-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El elemento `Dimension` es un identificador de objeto que contiene el nombre de la dimensión de cubo representada por el elemento `Object`.  
  
## <a name="see-also"></a>Vea también  
 [Elemento de la base de datos &#40;XMLA&#41;](database-element-xmla.md)   
 [Elemento Dimension (XMLA)](dimension-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
