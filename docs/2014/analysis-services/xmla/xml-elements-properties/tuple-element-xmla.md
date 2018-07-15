---
title: Elemento Tuple (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Tuple Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.tuple
- urn:schemas-microsoft-com:xml-analysis#Tuple
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuple
helpviewer_keywords:
- Tuple element
ms.assetid: d65aba10-55e1-49c1-81bc-0756c39c0da2
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5db226260852207fbcfeb4dc0a071d03d0def7c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233695"
---
# <a name="tuple-element-xmla"></a>Elemento Tuple (XMLA)
  Contiene una colección de elementos [Member](member-element-xmla.md) contenida por el elemento [Tuples](tuples-element-xmla.md) primario.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Tuples>  
   <Tuple>  
      <Member>...</Member>  
   </Tuple>  
   ...  
</Tuples>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Tuplas](tuples-element-xmla.md)|  
|Elementos secundarios|[Miembro](member-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 Cuando una aplicación cliente establece el `AxisFormat` propiedad *TupleFormat*, un eje se representa como un conjunto de tuplas. Cada `Axis` elemento contiene un `Tuples` elemento que representa el conjunto de tuplas de ese eje. Cada tupla se representa utilizando un elemento `Tuple` que contiene elementos `Member` de cada jerarquía del eje.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra la estructura de la `Tuple` elemento cuando un cliente especifica *TupleFormat* o *CustomFormat* para el `AxisFormat` propiedad XMLA, dada la siguiente miembros para el eje:  
  
|||||  
|-|-|-|-|  
|Jerarquía `Time`|1999|1999|2000|  
|Jerarquía `Category`|Real|Presupuesto|Presupuesto|  
  
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
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
