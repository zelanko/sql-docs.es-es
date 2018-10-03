---
title: Elemento Members (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Members Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords:
- Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fa1a418c0dc131f02c1afc2f2dd67810ebf90ea2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083510"
---
# <a name="members-element-xmla"></a>Elemento Members (XMLA)
  Contiene una colección de [miembro](member-element-xmla.md) elementos contenidos por el elemento primario [CrossProduct](crossproduct-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CrossProduct>  
   <Members Hierarchy="string">  
      <Member>...</Member>  
   </Members>  
   ...  
</CrossProduct>  
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
|Elementos primarios|[CrossProduct](crossproduct-element-xmla.md)|  
|Elementos secundarios|[Miembro](member-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|Hierarchy|Requiere `String` atributo. El nombre de la jerarquía a la que pertenecen los miembros incluidos en el elemento `Members`.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando una aplicación cliente establece el `AxisFormat` propiedad *ClusterFormat*, los miembros en cada eje se dividen en clústeres en el que cada clúster representa un producto cruzado entre los conjuntos ordenados de miembros de cada jerarquía. Cada elemento `Axis` consta de uno o varios elementos `CrossProduct`. Cada elemento `CrossProduct` contiene un elemento `Members` para cada jerarquía del eje. El elemento `Members`, a su vez, contiene un elemento `Member` para cada miembro de la jerarquía especificada que se incluye en el producto cruzado.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra la estructura de la `Members` elemento cuando un cliente especifica *ClusterFormat* para el `AxisFormat` propiedad XMLA, dado los siguientes miembros para el eje:  
  
||||||  
|-|-|-|-|-|  
|Jerarquía `Time`|1999|1999|2000|2001|  
|Jerarquía `Category`|Real|Presupuesto|Presupuesto|Presupuesto|  
|Clusters|Clúster 1|Clúster 1|Clúster 1|Clúster 2|  
  
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
  
  
