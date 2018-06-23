---
title: Elemento PropertyList (XMLA) | Documentos de Microsoft
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
- PropertyList Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#PropertyList
- microsoft.xml.analysis.propertylist
- urn:schemas-microsoft-com:xml-analysis#PropertyList
helpviewer_keywords:
- PropertyList element
ms.assetid: 58e63bd9-8aac-438d-adba-1868b4d123f5
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4b49ad0cf03ce331a00a7eefc9f1302176d89e74
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103907"
---
# <a name="propertylist-element-xmla"></a>Elemento PropertyList (XMLA)
  Contiene una colección de XML para las propiedades de Analysis (XMLA) usadas por el [Discover](../xml-elements-methods-discover.md) y [Execute](../xml-elements-methods-execute.md) métodos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Properties>  
   <PropertyList>  
      <!-- Zero or more XMLA properties -->  
   </PropertyList>  
</Properties>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Propiedades](properties-element-xmla.md)|  
|Elementos secundarios|Propiedades XMLA (vea la sección Notas)|  
  
## <a name="remarks"></a>Notas  
 El `PropertyList` elemento contiene una colección de propiedades XMLA. Cada propiedad permite al usuario controlar algún aspecto del método `Discover` o `Execute`, como definir la información requerida para establecer conexión con el origen de datos, especificando el formato de devolución del conjunto de resultados o especificando la configuración regional en la que se debe dar formato a los datos. Cada propiedad en el `PropertyList` está definida por un elemento XML independiente. El valor de la propiedad XMLA son los datos contenidos en el elemento XML, y el nombre de la propiedad XMLA corresponde al nombre del elemento XML.  
  
 Las propiedades disponibles y sus valores pueden obtenerse mediante el tipo de solicitud DISCOVER_PROPERTIES con el `Discover` método. No existe ningún requerimiento acerca del orden de las propiedades que aparecen listadas en el elemento `PropertyList`.  
  
 Para obtener más información sobre las propiedades XMLA compatibles con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [admite propiedades XMLA &#40;XMLA&#41;](propertylist-element-supported-xmla-properties.md).  
  
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
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  