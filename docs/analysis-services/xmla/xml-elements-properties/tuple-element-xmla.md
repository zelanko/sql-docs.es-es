---
title: Elemento Tuple (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f7f7d21f64c502e60ee0f6c95d2b6cbfd09c1b7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="tuple-element-xmla"></a>Elemento Tuple (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una colección de elementos [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) contenida por el elemento [Tuples](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md) primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Tuples>  
   <Tuple>  
      <Member>...</Member>  
   </Tuple>  
   ...  
</Tuples>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Tuplas](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
|Elementos secundarios|[Miembro](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Cuando una aplicación cliente establece la propiedad **AxisFormat** en *TupleFormat*, un eje se representa como un conjunto de tuplas. Cada elemento **Axis** contiene un elemento **Tuples** que representa el conjunto de tuplas de ese eje. Cada tupla se representa usando un elemento **Tuple** que contiene elementos **Member** de cada jerarquía del eje.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra la estructura del elemento **Tuple** cuando un cliente especifica *TupleFormat* o *CustomFormat* para la propiedad XMLA **AxisFormat**, dados los siguientes miembros para el eje:  
  
|||||  
|-|-|-|-|  
|Jerarquía **Time**|1999|1999|2000|  
|Jerarquía **Category**|Real|Presupuesto|Presupuesto|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <Tuples>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
      </Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
