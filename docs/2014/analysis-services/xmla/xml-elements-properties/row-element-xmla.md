---
title: Elemento Row (XMLA) | Documentos de Microsoft
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
- row Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#row
- microsoft.xml.analysis.row
- http://schemas.microsoft.com/analysisservices/2003/engine#row
helpviewer_keywords:
- row element
ms.assetid: 4d9977a0-c396-44c7-9fd4-97f4c3d643aa
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: de6460bc6d51c4205752b7db186412e420438145
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108660"
---
# <a name="row-element-xmla"></a>Elemento row (XMLA)
  Contiene una sola fila de datos para un [raíz](root-element-xmla.md) elemento que contiene datos tabulares devueltos por un [Discover](../xml-elements-methods-discover.md) o [Execute](../xml-elements-methods-execute.md) llamada al método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <row>  
      <!-- One or more column elements -->  
   </row>  
</root>  
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
|Elementos primarios|[raíz](root-element-xmla.md) (mediante el [conjunto de filas](../xml-data-types/rowset-data-type-xmla.md) tipo de datos)|  
|Elementos secundarios|Uno o más elementos de columna.|  
  
## <a name="remarks"></a>Notas  
 Cada fila devuelta por un elemento `root` que contiene datos tabulares tiene un elemento `row` correspondiente. Cada columna del elemento `root` está representada por un elemento XML diferente. El valor de la columna del elemento `row` es el dato que contiene el elemento XML y el nombre de la columna corresponde al nombre del elemento XML.  
  
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
  
 Si hay un elemento de columna que contiene un error, un elemento `Error` proporciona información sobre el error, tal y como se muestra en el siguiente ejemplo:  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 Para obtener más información sobre la nomenclatura de columna e información de esquema para los datos tabulares, vea [tipo de datos del conjunto de filas &#40;XMLA&#41;](../xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  