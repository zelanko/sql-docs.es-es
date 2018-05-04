---
title: Elemento Members (XMLA) | Documentos de Microsoft
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
- Members Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords:
- Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 20da0d8bcd7a651047b10736d829074265203fa0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="members-element-xmla"></a>Elemento Members (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una colección de [miembro](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) elementos contenidos por el elemento primario [CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md) elemento.  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)|  
|Elementos secundarios|[Miembro](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|Jerarquía|Atributo **String** requerido. El nombre de la jerarquía a la que los miembros incluidos en el **miembros** el elemento pertenece.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando una aplicación cliente establece el **AxisFormat** propiedad *ClusterFormat*, los miembros en cada eje se dividen en clústeres en el que cada uno representa un producto cruzado entre los conjuntos ordenados de miembros de cada jerarquía. Cada **eje** elemento consta de uno o varios **CrossProduct** elementos. Cada **CrossProduct** elemento contiene un **miembros** (elemento) para cada jerarquía del eje. El **miembros** elemento, a su vez, contiene un **miembro** elemento por cada miembro de la jerarquía especificada que se incluyen en el producto cruzado.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra la estructura de la **miembros** elemento cuando un cliente especifica *ClusterFormat* para el **AxisFormat** propiedad XMLA, dado el siguientes miembros para el eje:  
  
||||||  
|-|-|-|-|-|  
|Jerarquía **Time**|1999|1999|2000|2001|  
|Jerarquía **Category**|Real|Presupuesto|Presupuesto|Presupuesto|  
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
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
