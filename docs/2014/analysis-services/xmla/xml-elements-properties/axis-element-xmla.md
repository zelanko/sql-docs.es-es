---
title: Elemento Axis (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Axis Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.axis
- http://schemas.microsoft.com/analysisservices/2003/engine#Axis
helpviewer_keywords:
- Axis element
ms.assetid: 336895e1-4a57-4b43-9a53-e31569866e6c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8587e1cdb0105d72d2bc0219c8d038ca0bd03ca4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48153475"
---
# <a name="axis-element-xmla"></a>Elemento Axis (XMLA)
  Contiene un conjunto de tuplas utilizado para representar un eje único en un conjunto de datos multidimensional que contiene un [ejes](axes-element-xmla.md) elemento que usa el [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) tipo de datos devuelto por la [Execute](../xml-elements-methods-execute.md) método.  
  
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Ejes](axes-element-xmla.md)|  
|Elementos secundarios|[CrossProduct](crossproduct-element-xmla.md) o [tuplas](tuples-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El contenido del elemento `Axis` varía, dependiendo del valor de la propiedad XMLA `AxisFormat` usada por el método `Execute`.  
  
## <a name="tupleformat"></a>TupleFormat  
 Cuando una aplicación cliente establece el `AxisFormat` propiedad *TupleFormat*, un eje se representa como un conjunto de tuplas. Cada elemento `Axis` contiene un elemento `Tuples` que representa el conjunto de tuplas de ese eje. Cada tupla se representa utilizando un elemento `Tuple` que contiene elementos `Member` de cada jerarquía del eje.  
  
## <a name="clusterformat"></a>ClusterFormat  
 Cuando una aplicación cliente establece el `AxisFormat` propiedad *ClusterFormat*, los miembros en cada eje se dividen en clústeres en el que cada clúster representa un producto cruzado entre los conjuntos ordenados de miembros de cada jerarquía. Cada elemento `Axis` consta de uno o varios elementos `CrossProduct`. Cada elemento `CrossProduct` contiene un elemento `Members` para cada jerarquía del eje.  
  
## <a name="customformat"></a>CustomFormat  
 Cuando una aplicación cliente establece el `AxisFormat` propiedad *CustomFormat*, el valor se trata igual que el *TupleFormat* valor por una instancia de Analysis Services.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="description"></a>Descripción  
 El ejemplo siguiente muestra la estructura de la `Axis` elementos cuando un cliente especifica *TupleFormat* o *CustomFormat* para el `AxisFormat` propiedad XMLA, dada la siguiente miembros para el eje:  
  
|||||  
|-|-|-|-|  
|Jerarquía `Time`|1999|1999|2000|  
|Jerarquía `Category`|Real|Presupuesto|Presupuesto|  
  
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
  
### <a name="description"></a>Descripción  
 El ejemplo siguiente muestra la estructura de la `Axis` elementos cuando un cliente especifica *ClusterFormat* para el `AxisFormat` propiedad XMLA, dado los siguientes miembros para el eje:  
  
||||||  
|-|-|-|-|-|  
|Jerarquía `Time`|1999|1999|2000|2001|  
|Jerarquía `Category`|Real|Presupuesto|Presupuesto|Presupuesto|  
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
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
