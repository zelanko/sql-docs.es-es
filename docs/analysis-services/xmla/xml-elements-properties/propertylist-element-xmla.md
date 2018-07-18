---
title: Elemento PropertyList (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3e773de16e65aa9c7f1be521214088aa9f06b369
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38036713"
---
# <a name="propertylist-element-xmla"></a>Elemento PropertyList (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene una colección de XML para las propiedades de Analysis (XMLA) utilizadas por el [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) y [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) métodos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Properties>  
   <PropertyList>  
      <!-- Zero or more XMLA properties -->  
   </PropertyList>  
</Properties>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Propiedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
|Elementos secundarios|Propiedades XMLA (vea la sección Notas)|  
  
## <a name="remarks"></a>Notas  
 El elemento **PropertyList** contiene una colección de propiedades XMLA. Cada propiedad permite al usuario controlar algún aspecto del método **Discover** o **Execute** , como definir la información requerida para establecer conexión con el origen de datos, especificando el formato de devolución del conjunto de resultados o especificando la configuración regional en la que se debe dar formato a los datos. Cada propiedad XML del elemento **PropertyList** está definida por un elemento XML independiente. El valor de la propiedad XMLA son los datos contenidos en el elemento XML, y el nombre de la propiedad XMLA corresponde al nombre del elemento XML.  
  
 Las propiedades disponibles y sus valores se pueden obtener utilizando el tipo de solicitud DISCOVER_PROPERTIES con el método **Discover** . No existe ningún requerimiento acerca del orden de las propiedades que aparecen listadas en el elemento **PropertyList** .  
  
 Para obtener más información sobre las propiedades XMLA admitidas por Analysis Services, consulte [propiedades XMLA compatibles &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
## <a name="example"></a>Ejemplo  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
