---
title: Elemento Axis (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Axis Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.axis
- http://schemas.microsoft.com/analysisservices/2003/engine#Axis
helpviewer_keywords:
- Axis element
ms.assetid: 336895e1-4a57-4b43-9a53-e31569866e6c
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bb0538869453af24bd432a1d7f995e0007e79ec7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="axis-element-xmla"></a>Elemento Axis (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene un conjunto de tuplas utilizado para representar un eje único en un conjunto de datos multidimensional que contiene un [ejes](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md) elemento que usa el [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) tipo de datos, devuelto por la [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Axes>  
   ...  
   <Axis> <!-- when AxisFormat XMLA property is set to ClusterFormat -->  
      <CrossProduct>...</CrossProduct>  
   </Axis>  
   <Axis> <!-- when AxisFormat XMLA property is set to TupleFormat or CustomFormat -->  
      <Tuples>...</Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Ejes](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md)|  
|Elementos secundarios|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md) o [tuplas](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El contenido de la **eje** elemento varía dependiendo del valor de la **AxisFormat** propiedad XMLA utilizada por el **Execute** método.  
  
## <a name="tupleformat"></a>TupleFormat  
 Cuando una aplicación cliente establece la propiedad **AxisFormat** en *TupleFormat*, un eje se representa como un conjunto de tuplas. Cada **eje** elemento contiene un **tuplas** elemento que representa el conjunto de tuplas en ese eje. Cada tupla se representa usando un elemento **Tuple** que contiene elementos **Member** de cada jerarquía del eje.  
  
## <a name="clusterformat"></a>ClusterFormat  
 Cuando una aplicación cliente establece el **AxisFormat** propiedad *ClusterFormat*, los miembros en cada eje se dividen en clústeres en el que cada uno representa un producto cruzado entre los conjuntos ordenados de miembros de cada jerarquía. Cada **eje** elemento consta de uno o varios **CrossProduct** elementos. Cada **CrossProduct** elemento contiene un **miembros** (elemento) para cada jerarquía del eje.  
  
## <a name="customformat"></a>CustomFormat  
 Cuando una aplicación cliente establece el **AxisFormat** propiedad *CustomFormat*, el valor se trata igual que el *TupleFormat* valor por una instancia de Analysis Services.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Description  
 En el ejemplo siguiente se muestra la estructura de la **eje** elementos cuando un cliente especifica *TupleFormat* o *CustomFormat* para el **AxisFormat**  Propiedad XMLA, dado los siguientes miembros para el eje:  
  
|||||  
|-|-|-|-|  
|Jerarquía **Time**|1999|1999|2000|  
|Jerarquía **Category**|Real|Presupuesto|Presupuesto|  
  
### <a name="code"></a>código  
  
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
  
### <a name="description"></a>Description  
 En el ejemplo siguiente se muestra la estructura de la **eje** elementos cuando un cliente especifica *ClusterFormat* para el **AxisFormat** propiedad XMLA, dada la siguiente miembros para el eje:  
  
||||||  
|-|-|-|-|-|  
|Jerarquía **Time**|1999|1999|2000|2001|  
|Jerarquía **Category**|Real|Presupuesto|Presupuesto|Presupuesto|  
|Clusters|Clúster 1|Clúster 1|Clúster 1|Clúster 2|  
  
### <a name="code"></a>código  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size = "4">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
      <CrossProduct Size = "1">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[2001]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>Ver también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
