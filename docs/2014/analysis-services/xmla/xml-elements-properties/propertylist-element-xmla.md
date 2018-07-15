---
title: Elemento PropertyList (XMLA) | Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b3fdd7f6d59ef6a2523bada292dfb2b8f17a4a8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37323045"
---
# <a name="propertylist-element-xmla"></a>Elemento PropertyList (XMLA)
  Contiene una colección de XML para las propiedades de Analysis (XMLA) utilizadas por el [Discover](../xml-elements-methods-discover.md) y [Execute](../xml-elements-methods-execute.md) métodos.  
  
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
 El `PropertyList` elemento contiene una colección de propiedades XMLA. Cada propiedad permite al usuario controlar algún aspecto del método `Discover` o `Execute`, como definir la información requerida para establecer conexión con el origen de datos, especificando el formato de devolución del conjunto de resultados o especificando la configuración regional en la que se debe dar formato a los datos. Cada propiedad en el `PropertyList` elemento está definido por un elemento XML diferente. El valor de la propiedad XMLA son los datos contenidos en el elemento XML, y el nombre de la propiedad XMLA corresponde al nombre del elemento XML.  
  
 Se pueden obtener las propiedades disponibles y sus valores con el tipo de solicitud DISCOVER_PROPERTIES con el `Discover` método. No existe ningún requerimiento acerca del orden de las propiedades que aparecen listadas en el elemento `PropertyList`.  
  
 Para obtener más información sobre las propiedades XMLA admitidas por [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [propiedades XMLA compatibles &#40;XMLA&#41;](propertylist-element-supported-xmla-properties.md).  
  
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
  
  
