---
title: Elemento Row (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 78745ed581642092c17190c4b81eb3f9ab6df853
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="row-element-xmla"></a>Elemento row (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una fila única de datos para un elemento [root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) que contiene datos tabulares devueltos por una llamada al método [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) .  
  
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
|Elementos primarios|[root](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) (con el tipo de datos [Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) )|  
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
  
 Para obtener más información sobre la nomenclatura de columna e información de esquema para los datos tabulares, vea [tipo de conjunto de filas de datos & #40; XMLA & #41; ](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
