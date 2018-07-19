---
title: Elemento CubeInfo (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1e93de452634e0f97d648e6548357cc040b9aca
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38004577"
---
# <a name="cubeinfo-element-xmla"></a>Elemento CubeInfo (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene los metadatos del cubo contenidos por el elemento primario [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<OlapInfo>  
   ...  
   <CubeInfo>  
      <Cube>...</Cube>  
   </CubeInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|Elementos secundarios|[Cubo](../../../analysis-services/xmla/xml-elements-properties/cube-element-olapinfo-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El **CubeInfo** contiene un elemento **cubo** (elemento) para cada cubo al que hace referencia en el conjunto de datos multidimensional.  
  
> [!NOTE]  
>  Analysis Services devuelve una sola **cubo** elemento de esta colección porque [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite las instrucciones que hacen referencia a varios cubos en la cláusula FROM del lenguaje de expresiones multidimensionales (MDX).  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
