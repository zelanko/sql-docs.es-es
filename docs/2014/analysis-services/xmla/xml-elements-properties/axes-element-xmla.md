---
title: Axes (XMLA) del elemento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Axes Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Axes
- http://schemas.microsoft.com/analysisservices/2003/engine#Axes
- microsoft.xml.analysis.axes
- urn:schemas-microsoft-com:xml-analysis#Axes
helpviewer_keywords:
- Axes element
ms.assetid: 2005d06a-f8a2-4b4f-8c0d-2f7f73eb6f5c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdb5aa48dd3a65f99b424274fdb89b3aee8c9591
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094915"
---
# <a name="axes-element-xmla"></a>Elemento Axes (XMLA)
  Contiene una colección de [eje](axis-element-xmla.md) elementos que representan datos de eje contenidos por un [raíz](root-element-xmla.md) elemento que usa el [MDDataSet](../xml-data-types/mddataset-data-type-xmla.md) tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <Axes>  
      <Axis>...</Axis>  
   </Axes>  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cualquiera|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Raíz](root-element-xmla.md)|  
|Elementos secundarios|[Axis](axis-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 En el elemento `Axes`, los elementos `Axis` se enumeran en el orden que tienen lugar en el conjunto de datos bajo, empezando desde cero. El valor de la propiedad XMLA de `AxisFormat` determina cómo se da formato a los elementos `Axis`. Para obtener más información sobre la `AxisFormat` propiedad, vea [propiedades XMLA compatibles &#40;XMLA&#41;](propertylist-element-supported-xmla-properties.md).  
  
 Un eje representa un conjunto de tuplas, en las que todas las tuplas del conjunto tienen la misma dimensionalidad. Un conjunto se puede representar de maneras diferentes con ventajas diferentes. Por ejemplo, el conjunto siguiente de cuatro tuplas se puede representar como una colección de tuplas bidimensionales o un producto cartesiano de dos conjuntos unidimensionales.  
  
|1999|1999|2000|2000|  
|----------|----------|----------|----------|  
|Real|Presupuesto|Real|Presupuesto|  
  
 Este conjunto de tuplas se puede representar como una colección de tuplas bidimensionales:  
  
```  
{ ( 1999, Actual ), ( 1999, Budget ), ( 2000, Actual ), ( 2000, Budget ) }  
```  
  
 Este conjunto también se puede representar como un producto cartesiano de dos conjuntos unidimensionales:  
  
```  
{ 1999, 2000 } x { Actual, Budget }  
```  
  
 Para las herramientas cliente es más fácil usar la primera representación, la colección de tuplas bidimensionales. La segunda representación, un producto cartesiano de conjuntos unidimensionales, utiliza menos espacio y conserva la naturaleza multidimensional del conjunto.  
  
 La tabla siguiente enumera las operaciones que se pueden usar para definir y caracterizar la estructura y los miembros de un eje.  
  
|Operación|Descripción|  
|---------------|-----------------|  
|Miembro|La unidad más pequeña de un eje que representa el miembro de una jerarquía de la dimensión.|  
|Miembros|Una colección de los objetos `Member` de la misma jerarquía de la dimensión.|  
|Tuple|Una colección de miembros de diferentes jerarquías de la dimensión.|  
|Tuplas|Colección de objetos `Tuple` con la misma dimensionalidad.|  
|Union|Una unión de conjuntos.|  
|CrossJoin|Un producto cartesiano de conjuntos.|  
  
 Estas operaciones traducen las tuplas bidimensionales y el producto cartesiano de conjuntos unidimensionales como sigue.  
  
## <a name="two-dimensional-tuples"></a>Tuplas bidimensionales  
  
```  
Tuples (  
   Tuple( Member(1999), Member(Actual) ),  
   Tuple( Member(1999), Member(Budget) ),  
   Tuple( Member(2000), Member(Actual) ),  
   Tuple( Member(2000), Member(Budget) )  
```  
  
## <a name="cartesian-product-of-one-dimensional-sets"></a>Producto cartesiano de conjuntos unidimensionales  
  
```  
CrossProduct (  
   Members( Member(1999), Member(2000) ),  
   Members( Member(Actual), Member(Budget) )  
```  
  
 Un cliente puede usar la propiedad `AxisFormat` para solicitar una representación concreta.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos MDDataSet &#40;XMLA&#41;](../xml-data-types/mddataset-data-type-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
