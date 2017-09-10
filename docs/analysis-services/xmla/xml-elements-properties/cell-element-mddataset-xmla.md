---
title: (MDDataSet) (XMLA) del elemento de celda | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Cell Element (MDDataSet)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords:
- Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4d8e85ec05fa6fd8b3c05ee0f27f46b0a28a867
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="cell-element-mddataset-xmla"></a>Elemento Cell (MDDataSet) (XMLA)
  Contiene información acerca de una sola celda que contiene un elemento primario [CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md) elemento.  
  
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)|  
|Elementos secundarios|Cero o más valores de propiedad de celda o [Error](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|CellOrdinal|Requiere **unsignedInt** atributo. Posición ordinal de la celda dentro del conjunto de datos multidimensional.|  
  
## <a name="remarks"></a>Comentarios  
 En el elemento primario **raíz** elemento, el **ejes** elemento va seguido del **CellData** elemento, una colección de **celda** elementos que contienen los valores de propiedad para cada celda devuelta en el conjunto de datos multidimensional. El **celda** elemento contiene el **CellOrdinal** atributo, que indica la posición ordinal de base cero de la celda dentro del conjunto de datos multidimensional y un elemento para cada valor de propiedad de celda asociado a la celda. Cada valor de propiedad de celda en el **celda** está definida por un elemento XML independiente. El valor de la propiedad de celda es los datos contenidos en el elemento XML y el nombre de la propiedad de celda, como se define en el **CellInfo** elemento del elemento raíz primario, corresponde al nombre del elemento XML.  
  
 La sintaxis siguiente describe un valor de propiedad de la celda:  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 El tipo de datos de un valor de propiedad de celda solamente se especifica para la propiedad de celda VALUE. Los tipos de datos de otras propiedades de celda se determinan mediante la definición de propiedad de celda incluida en la **CellInfo** elemento. Puede excluir un elemento de valor de propiedad de celda si se ha especificado un valor predeterminado (mediante la inclusión de un **predeterminado** , elemento de una definición de propiedad de celda contenida en el **CellInfo** elemento) para una propiedad de celda o si no se ha especificado ningún valor predeterminado y el valor de la propiedad de celda es null.  
  
## <a name="cell-property-errors"></a>Errores de propiedades de celda  
 Si no se puede devolver una propiedad de celda debido a un error que se produce en la instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], por ejemplo, un error de cálculo que impide que el valor que se devuelve para una celda determinada, un **Error** elemento reemplaza el contenido de la propiedad de celda en cuestión. El ejemplo de XML siguiente describe un error de propiedad de celda:  
  
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
 La referencia de eje de una celda se puede calcular en función de un **CellOrdinal** valor de atributo. Conceptualmente, las celdas se numeran en un conjunto de datos como si el conjunto de datos fuera una *p*-matriz unidimensional, donde *p* es el número de ejes. Las celdas se ordenan por importancia de fila.  
  
 Suponga que una consulta solicita cuatro medidas en las columnas y una combinación cruzada de dos estados con cuatro trimestres en las filas. En el resultado de conjunto de datos, como resultado la **CellOrdinal** propiedad para la parte del resultado de conjunto de datos mostrado en negrita es el conjunto {9, 10, 11, 13, 14, 15, 17, 18, 19}. Éste es el conjunto porque las celdas se numeran en orden de importancia de filas, a partir de un **CellOrdinal** de 0 para la celda superior izquierda.  
  
|State|Trimestre|Unit sales|Store cost|Store sales|Sales count|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|Q1|16890|14431.09|36175.2|5498|  
||Q2|18052|15332.02|38396.75|5915|  
||Q3|18370|**15672.83**|**39394.05**|**6014**|  
||T4|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|Q1|19287|**16081.07**|**40170.29**|**6184**|  
||Q2|15079|12678.96|31772.88|4799|  
||Q3|16940|14273.78|35880.46|5432|  
||T4|16353|13738.68|34453.44|5196|  
|Washington|Q1|30114|25240.08|63282.86|9906|  
||Q2|29479|24953.25|62496.64|9654|  
||Q3|30538|25958.26|64997.38|10007|  
||T4|34235|29172.72|73016.34|11217|  
  
 Si se aplica la fórmula de la figura, el eje k = 0 tiene Uk = 4 miembros, y el eje k = 1 tiene Uk = 8 tuplas. P = 2 es el número total de ejes de la consulta. Si se toma la celda que es {California, Q3, Store Cost} como S0, la suma inicial es i = 0 a 1. Para i = 0, la tupla ordinal del eje 0 de {Store Cost} es 1. Para i = 1, la tupla ordinal de {CA, Q3} es 2.  
  
 Para = 0, Ei = 1, por = 0 la suma es 1 * 1 = 1 y para = 1, la suma es 2 (ordinal de tupla) veces 4 (el valor de Ei calculado como 1 \* 4), u 8. La suma de 1 + 8 es 9, el ordinal de celda de esa celda.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra la estructura de la **celda** valores de propiedad para cada celda de la celda de elemento, incluidos el valor, FORMATTED_VALUE y FORMAT_STRING.  
  
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
 [Tipo de datos MDDataSet &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
