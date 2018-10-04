---
title: Elemento Parameters (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Parameters Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameters
- urn:schemas-microsoft-com:xml-analysis#Parameters
- microsoft.xml.analysis.parameters
helpviewer_keywords:
- Parameters element
ms.assetid: d46454a1-a1d1-4aa8-95ea-54be22a53e83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b9c3d0d642ad7248d87e7cc17aaa17953bf6aec
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134055"
---
# <a name="parameters-element-xmla"></a>Elemento Parameters (XMLA)
  Contiene una colección de [parámetro](parameter-element-xmla.md) elementos utilizados por el [Execute](../xml-elements-methods-execute.md) método.  
  
 **Namespace:** `urn:schemas-microsoft-com:xml-analysis`  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Execute>  
...  
   <Parameters>  
      <Parameter>...</Parameter>  
   </Parameters>  
...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Ejecutar](../xml-elements-methods-execute.md)|  
|Elementos secundarios|[Parámetro](parameter-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Alguna parte del código XML para los comandos de Analysis (XMLA), como el comando [Process](../xml-elements-commands/process-element-xmla.md) , puede requerir información adicional. El elemento `Parameters` proporciona un mecanismo para ofrecer información adicional, incluso información en lotes, para un comando XMLA.  
  
 Si el comando XMLA no utiliza el elemento `Parameters`, el elemento se puede omitir al llamar al método `Execute`.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
