---
title: Ejes elemento (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
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
- Axes Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Axes
- http://schemas.microsoft.com/analysisservices/2003/engine#Axes
- microsoft.xml.analysis.axes
- urn:schemas-microsoft-com:xml-analysis#Axes
helpviewer_keywords:
- Axes element
ms.assetid: 2005d06a-f8a2-4b4f-8c0d-2f7f73eb6f5c
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c12c3d3e4f64ee0be203d676753a00cc002cf11b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="axes-element-xmla"></a>Elemento Axes (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una colección de [eje](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md) elementos que representan datos de eje contenidos por un [raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento que usa el [MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) tipo de datos.  
  
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
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|Elementos secundarios|[Eje](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 En el **ejes** elemento, el **eje** elementos se muestran en el orden en que aparecen en el conjunto de datos, empezando por cero. El **AxisFormat** configuración de la propiedad XMLA determina cómo **eje** se da formato a los elementos. Para obtener más información sobre la **AxisFormat** propiedad, vea [admite propiedades XMLA &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
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
  
|Operación|Description|  
|---------------|-----------------|  
|Miembro|La unidad más pequeña de un eje que representa el miembro de una jerarquía de la dimensión.|  
|Miembros|Una colección de **miembro** objetos de la misma jerarquía de la dimensión.|  
|Tuple|Una colección de miembros de diferentes jerarquías de la dimensión.|  
|Tuplas|Una colección de **tupla** objetos con la misma dimensionalidad.|  
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
  
 Un cliente puede utilizar el **AxisFormat** propiedad para solicitar una representación concreta.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos MDDataSet & #40; XMLA & #41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
