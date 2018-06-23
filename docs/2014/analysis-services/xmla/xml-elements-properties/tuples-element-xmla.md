---
title: Elemento Tuples (XMLA) | Documentos de Microsoft
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
- Tuples Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuples
- microsoft.xml.analysis.tuples
- urn:schemas-microsoft-com:xml-analysis#Tuples
helpviewer_keywords:
- Tuples element
ms.assetid: 5494bbaa-c1aa-43fa-b3e0-83befb2bccdd
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: da9614fb01620a3dec5bdff9f63d044652a4749b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199747"
---
# <a name="tuples-element-xmla"></a>Elemento Tuples (XMLA)
  Contiene un conjunto de [tupla](tuple-element-xmla.md) de objetos para un [eje](axis-element-xmla.md) elemento que usa el [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) tipo de datos, devuelto por la [Execute](../xml-elements-methods-execute.md) método.  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Axis](axis-element-xmla.md)|  
|Elementos secundarios|[tupla](tuple-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 Cuando una aplicación cliente establece el `AxisFormat` propiedad *TupleFormat*, un eje se representa como un conjunto de tuplas. Cada `Axis` elemento contiene un `Tuples` elemento que representa el conjunto de tuplas en ese eje. Cada tupla se representa mediante el uso de un `Tuple` elemento que contiene [miembro](member-element-xmla.md) elementos de cada jerarquía del eje.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra la estructura de la `Tuples` elemento cuando un cliente especifica *TupleFormat* o *CustomFormat* para el `AxisFormat` XML para la propiedad Analysis (XMLA) dados a los siguientes miembros para el eje:  
  
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
  
  