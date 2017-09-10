---
title: Elemento Row (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- row Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#row
- microsoft.xml.analysis.row
- http://schemas.microsoft.com/analysisservices/2003/engine#row
helpviewer_keywords:
- row element
ms.assetid: 4d9977a0-c396-44c7-9fd4-97f4c3d643aa
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 52bc6d400340375163fd9ae8b285c071249a88f7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="row-element-xmla"></a>Elemento row (XMLA)
  Contiene una sola fila de datos para un [raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento que contiene datos tabulares devueltos por un [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <row>  
      <!-- One or more column elements -->  
   </row>  
</root>  
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
|Elementos primarios|[raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) (mediante el [conjunto de filas](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) tipo de datos)|  
|Elementos secundarios|Uno o más elementos de columna.|  
  
## <a name="remarks"></a>Comentarios  
 Cada fila devuelta por un elemento **root** que contiene datos tabulares tiene un elemento **row** correspondiente. Cada columna del elemento **root** está representada por un elemento XML diferente. El valor de la columna del elemento **row** es el dato que contiene el elemento XML y el nombre de la columna corresponde al nombre del elemento XML.  
  
 Hay dos maneras de expresar un valor nulo para una columna dentro de una fila:  
  
-   Un elemento de columna que falta implica que la columna es nula.  
  
-   El elemento de columna puede utilizar el atributo `xsi:nil='true'` para indicar que tiene un valor nulo.  
  
 Por ejemplo, si una fila tiene una única columna llamada Store_Name y su valor es NULL, se puede representar como:  
  
```  
<row>  
</row>  
```  
  
 O bien:  
  
```  
<row>  
   <Store_name xsi:nil='true'/>  
</row>  
```  
  
 Si hay un elemento de columna que contiene un error, un elemento **Error** proporciona información sobre el error, tal y como se muestra en el siguiente ejemplo:  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 Para obtener más información sobre la nomenclatura de columna e información de esquema para los datos tabulares, vea [tipo de conjunto de filas de datos &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
