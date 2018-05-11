---
title: Elemento Tuples (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f308894ac5c530253ccbbc389cbf466ac3ab859
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="tuples-element-xmla"></a>Elemento Tuples (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene un conjunto de [tupla](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md) de objetos para un [eje](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) elemento que usa el [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) tipo de datos, devuelto por la [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Axis>  
   ...  
   <Tuples>  
      <Tuple>...</Tuple>  
   </Tuples>  
   ...  
</Axis>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Eje](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|Elementos secundarios|[Tupla](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Cuando una aplicación cliente establece la propiedad **AxisFormat** en *TupleFormat*, un eje se representa como un conjunto de tuplas. Cada elemento **Axis** contiene un elemento **Tuples** que representa el conjunto de tuplas de ese eje. Cada tupla se representa usando un elemento **Tuple** que contiene elementos [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) de cada jerarquía del eje.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra la estructura de la **tuplas** elemento cuando un cliente especifica *TupleFormat* o *CustomFormat* para el **AxisFormat**  XML para la propiedad Analysis (XMLA), dado los siguientes miembros para el eje:  
  
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
  
  
