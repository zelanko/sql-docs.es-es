---
title: Valor de elemento (Parameter) (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cbd4dd56bedf53d4f0bc7374e9389221acb092d7
ms.sourcegitcommit: cfe5b2af733e7801558b441b4b9427cfe4c26435
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34576757"
---
# <a name="value-element-parameter-xmla"></a>Elemento Value (Parameter) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene el valor de un parámetro representado por la [parámetro](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Parameter>  
   ...  
   <Value>...</Value>  
   ...  
</Parameter>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cualquiera|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Parámetro](../../../analysis-services/xmla/xml-elements-properties/parameter-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El **valor** elemento puede almacenar cualquier tipo XML sencillo, así como el XML for Analysis (XMLA) **conjunto de filas** tipo de datos, para los parámetros utilizados por comandos XMLA en el [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
