---
title: Elemento CellInfo (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CellInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords:
- CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 803640fe83ccc3137b4597b8c1b78850abeb55c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114324"
---
# <a name="cellinfo-element-xmla"></a>Elemento CellInfo (XMLA)
  Representa los metadatos de celda contenidos por el elemento primario [OlapInfo](olapinfo-element-xmla.md) elemento.  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[OlapInfo](olapinfo-element-xmla.md)|  
|Elementos secundarios|Una o más definiciones de propiedades de la celda|  
  
## <a name="remarks"></a>Notas  
 El elemento `CellInfo` contiene una colección de propiedades para las celdas incluidas dentro del conjunto de datos multidimensional devuelto por un elemento `root` que utiliza el tipo de datos `MDDataSet`. Cada propiedad de celda incluida en el elemento `CellInfo` queda definida por un elemento XML separado, cada uno de los cuales posee un atributo `name` y un atributo `type`. El atributo `name` de la propiedad de celda se corresponde con el nombre del OLE DB para la propiedad de celda OLAP representada por el elemento XML y el atributo `type` representa el tipo de datos XML de la propiedad de celda. El nombre del elemento XML se utiliza para identificar el valor de la propiedad para aquellas celdas contenidas en el elemento `CellData` del elemento `root`.  
  
 La sintaxis siguiente describe la definición de una propiedad de celda:  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 Las propiedades disponibles y sus valores pueden obtenerse mediante el tipo de solicitud DISCOVER_PROPERTIES con el `Discover` método. No existe ningún requerimiento acerca del orden de las propiedades que aparecen listadas en el elemento `PropertyList`.  
  
 Opcionalmente, un proveedor puede especificar los valores predeterminados para ciertos miembros o para propiedades de la celda en la sección `AxisInfo` o `CellInfo`. Los valores predeterminados pueden proporcionar menos resultados si la propiedad tiene siempre o casi siempre el mismo valor. Para indicar un valor predeterminado para una propiedad, el`Default` , opcionalmente, se puede especificar el elemento como un elemento secundario de uno de los elementos de definición de la propiedad de celda. Por consiguiente, la ausencia de un miembro o de una propiedad de la celda en el resultado indica que el valor predeterminado expresado es el valor para la propiedad de la celda.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo muestra cómo se representan las propiedades de celda VALUE, FORMATTED_VALUE y FORMAT_STRING en el elemento `CellInfo`.  
  
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
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  