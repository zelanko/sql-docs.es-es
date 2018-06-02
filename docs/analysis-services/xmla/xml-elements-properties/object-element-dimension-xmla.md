---
title: Objeto de elemento (Dimension) (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b321a6c26edb4f569b4174d64a0a50b8ac23ae6
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575767"
---
# <a name="object-element-dimension-xmla"></a>Elemento Object (Dimension) (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una referencia de objeto para la dimensión en la que el elemento primario [insertar](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [actualización](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), o [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) se ejecuta el comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Insert> <!-- or any of the parent elements in the Element relationships table -->  
...  
   <Object>  
      <Database>...</Database>  
      <Cube>...</Cube>  
      <Dimension>...</Dimension>  
   </Object>  
...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Quitar](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [insertar](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [actualización](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|Elementos secundarios|[Cubo](../../../analysis-services/xmla/xml-elements-properties/cube-element-xmla.md), [base de datos](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md), [dimensión](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
