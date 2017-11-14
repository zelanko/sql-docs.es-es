---
title: Elemento CellInfo (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- CellInfo Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords:
- CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3a7b38201d5ba5c051cfacfb139ea52a6b93fb09
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="cellinfo-element-xmla"></a>Elemento CellInfo (XMLA)
  Representa los metadatos de celda contenidos por el elemento primario [OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<OlapInfo>  
   ...  
   <CellInfo>  
      <!-- One or more cell property definitions -->  
   </CellInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|Elementos secundarios|Una o más definiciones de propiedades de la celda|  
  
## <a name="remarks"></a>Comentarios  
 El **CellInfo** elemento contiene una colección de propiedades de celda de las celdas incluidas en el conjunto de datos multidimensional devuelto por un **raíz** elemento utilizando el **MDDataSet**tipo de datos. Cada propiedad de celda en el **CellInfo** está definida por un elemento XML diferente, cada uno con un **nombre** atributo y un **tipo** atributo. El **nombre** atributo de la propiedad de celda se corresponde con el nombre de OLE DB para la propiedad de celda OLAP representada por el elemento XML y el **tipo** atributo representa el tipo de datos XML de la celda propiedad. El nombre del elemento XML se usa para identificar el valor de la propiedad de celda para aquellas celdas contenidas en el **CellData** elemento de la **raíz** elemento.  
  
 La sintaxis siguiente describe la definición de una propiedad de celda:  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 Las propiedades disponibles y sus valores se pueden obtener utilizando el tipo de solicitud DISCOVER_PROPERTIES con el método **Discover** . No existe ningún requerimiento acerca del orden de las propiedades que aparecen listadas en el elemento **PropertyList** .  
  
 Un proveedor, opcionalmente, puede especificar valores predeterminados para las propiedades de miembro o una celda individuales en el **AxisInfo** o **CellInfo** sección. Los valores predeterminados pueden proporcionar menos resultados si la propiedad tiene siempre o casi siempre el mismo valor. Para indicar un valor predeterminado para una propiedad, el**predeterminado** elemento si lo desea puede especificarse como un elemento secundario de uno de los elementos de definición de la propiedad de celda. Por consiguiente, la ausencia de un miembro o de una propiedad de la celda en el resultado indica que el valor predeterminado expresado es el valor para la propiedad de la celda.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo se representan las propiedades de celda VALUE, FORMATTED_VALUE y FORMAT_STRING en el **CellInfo** elemento.  
  
```  
<OlapInfo>  
   ...  
      <CellInfo>  
         <Value name="VALUE"></Value>  
         <FmtValue name="FORMATTED_VALUE"></FmtValue>  
         <FormatString name="FORMAT_STRING"></FormatString>  
      </CellInfo>  
</OlapInfo>  
```  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

