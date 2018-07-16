---
title: Celda de elemento (MDDataSet) (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Cell Element (MDDataSet)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords:
- Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3f07798a28c59597575de08bf5d0f3ea1d7087c8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37269511"
---
# <a name="cell-element-mddataset-xmla"></a>Elemento Cell (MDDataSet) (XMLA)
  Contiene información acerca de una sola celda que contiene un elemento primario [CellData](celldata-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CellData>  
   <Cell CellOrdinal="unsignedInt">  
      <!-- Zero or more cell property values -->  
      <!-- or -->  
      <Error>...</Error>  
   </Cell>  
</CellData>  
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
|Elementos primarios|[CellData](celldata-element-xmla.md)|  
|Elementos secundarios|Cero o más valores de propiedad de celda o [Error](error-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|CellOrdinal|Requiere `unsignedInt` atributo. Posición ordinal de la celda dentro del conjunto de datos multidimensional.|  
  
## <a name="remarks"></a>Notas  
 En el elemento `root` primario, el elemento `Axes` va seguido del elemento `CellData`, una colección de elementos `Cell` que contienen los valores de propiedad para cada celda devuelta en un conjunto de datos multidimensional. El elemento `Cell` contiene el atributo `CellOrdinal`, que indica la posición ordinal basada en cero de la celda dentro del conjunto de datos multidimensional, y un elemento para cada valor de propiedad de la celda asociado a la celda. Un elemento XML independiente define cada valor de propiedad de la celda en el elemento `Cell`. El valor de la propiedad de la celda es los datos que se encuentran en el elemento XML; el nombre de la propiedad de la celda, definido en el elemento `CellInfo` del elemento raíz primario, corresponde al nombre del elemento XML.  
  
 La sintaxis siguiente describe un valor de propiedad de la celda:  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 El tipo de datos de un valor de propiedad de celda solamente se especifica para la propiedad de celda VALUE. La definición de la propiedad de la celda incluida en el elemento `CellInfo` determina los tipos de datos de las demás propiedades de la celda. Se puede excluir un elemento de valor de propiedad de celda si se ha especificado un valor predeterminado (mediante la inclusión de un elemento `Default` para una definición de propiedad de celda contenida en el elemento `CellInfo`) para una propiedad de celda, o si no se ha especificado ningún valor predeterminado y el valor de la propiedad de celda es nulo.  
  
## <a name="cell-property-errors"></a>Errores de propiedades de celda  
 Si no se puede devolver una propiedad de celda debido a un error que se produce en la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], por ejemplo, un error de cálculo que impide que el valor que se devuelve para una celda determinada, un `Error` elemento reemplaza el contenido de la propiedad de celda en cuestión. El ejemplo de XML siguiente describe un error de propiedad de celda:  
  
```  
<Cell CellOrdinal="0">  
   <Value xsi:type="xsd:double">  
      <Error>  
         <ErrorCode>2148497527</ErrorCode>  
         <Description>Unknown error</Description>  
      </Error>  
   </Value>  
</Cell>  
```  
  
## <a name="calculating-cell-ordinal-values"></a>Calcular los valores ordinales de celdas  
 La referencia de eje de una celda se puede calcular en función de un valor de atributo `CellOrdinal`. Conceptualmente, las celdas se numeran en un conjunto de datos como si el conjunto de datos fuera una *p*-matriz dimensional, donde *p* es el número de ejes. Las celdas se ordenan por importancia de fila.  
  
 Suponga que una consulta solicita cuatro medidas en las columnas y una combinación cruzada de dos estados con cuatro trimestres en las filas. En el siguiente resultado de conjunto de datos, la propiedad `CellOrdinal` para la parte del resultado del conjunto de datos mostrada en negrita es el conjunto {9, 10, 11, 13, 14, 15, 17, 18, 19}. Éste es el conjunto porque las celdas se numeran en orden de importancia de fila, iniciándose con un `CellOrdinal` de 0 para la celda superior izquierda.  
  
|State|Trimestre|Unit sales|Store cost|Store sales|Sales count|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|Q1|16890|14431.09|36175.2|5498|  
||2 º TRIMESTRE|18052|15332.02|38396.75|5915|  
||P3|18370|**15672.83**|**39394.05**|**6014**|  
||P4|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|Q1|19287|**16081.07**|**40170.29**|**6184**|  
||2 º TRIMESTRE|15079|12678.96|31772.88|4799|  
||P3|16940|14273.78|35880.46|5432|  
||P4|16353|13738.68|34453.44|5196|  
|Washington|Q1|30114|25240.08|63282.86|9906|  
||2 º TRIMESTRE|29479|24953.25|62496.64|9654|  
||P3|30538|25958.26|64997.38|10007|  
||P4|34235|29172.72|73016.34|11217|  
  
 Si se aplica la fórmula de la figura, el eje k = 0 tiene Uk = 4 miembros, y el eje k = 1 tiene Uk = 8 tuplas. P = 2 es el número total de ejes de la consulta. Si se toma la celda que es {California, Q3, Store Cost} como S0, la suma inicial es i = 0 a 1. Para i = 0, la tupla ordinal del eje 0 de {Store Cost} es 1. Para i = 1, la tupla ordinal de {CA, Q3} es 2.  
  
 Para = 0, Ei = 1, por lo que para = 0 la suma es 1 * 1 = 1 y para = 1, la suma es 2 (tupla ordinal) veces 4 (el valor de Ei calculado como 1 \* 4), u 8. La suma de 1 + 8 es 9, el ordinal de celda de esa celda.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra la estructura del elemento `Cell`, con los valores de propiedad de celda VALUE, FORMATTED_VALUE y FORMAT_STRING para cada celda.  
  
```  
<CellData>  
   <Cell CellOrdinal="0">  
      <Value xsi:type="xsd:double">16890</Value>  
      <FmtValue>16,890.00</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="1">  
      <Value xsi:type="xsd:int">50</Value>  
      <FmtValue>50</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="2">  
      <Value xsi:type="xsd:double">36175.2</Value>  
      <FmtValue>$36,175.20</FmtValue>  
      <FormatString>Currency</FormatString>  
   </Cell>  
</CellData>  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos MDDataSet &#40;XMLA&#41;](../xml-data-types/mddataset-data-type-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
