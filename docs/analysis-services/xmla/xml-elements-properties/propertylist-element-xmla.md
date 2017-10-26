---
title: Elemento PropertyList (XMLA) | Documentos de Microsoft
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
- PropertyList Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#PropertyList
- microsoft.xml.analysis.propertylist
- urn:schemas-microsoft-com:xml-analysis#PropertyList
helpviewer_keywords:
- PropertyList element
ms.assetid: 58e63bd9-8aac-438d-adba-1868b4d123f5
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d780b358d0d8d22ce5f71c5c90e87656a4cebee6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="propertylist-element-xmla"></a>Elemento PropertyList (XMLA)
  Contiene una colección de XML para las propiedades de Analysis (XMLA) usadas por el [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) y [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) métodos.  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Propiedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
|Elementos secundarios|Propiedades XMLA (vea la sección Notas)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento **PropertyList** contiene una colección de propiedades XMLA. Cada propiedad permite al usuario controlar algún aspecto del método **Discover** o **Execute** , como definir la información requerida para establecer conexión con el origen de datos, especificando el formato de devolución del conjunto de resultados o especificando la configuración regional en la que se debe dar formato a los datos. Cada propiedad XML del elemento **PropertyList** está definida por un elemento XML independiente. El valor de la propiedad XMLA son los datos contenidos en el elemento XML, y el nombre de la propiedad XMLA corresponde al nombre del elemento XML.  
  
 Las propiedades disponibles y sus valores se pueden obtener utilizando el tipo de solicitud DISCOVER_PROPERTIES con el método **Discover** . No existe ningún requerimiento acerca del orden de las propiedades que aparecen listadas en el elemento **PropertyList** .  
  
 Para obtener más información sobre las propiedades XMLA compatibles con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [admite propiedades XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
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
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

