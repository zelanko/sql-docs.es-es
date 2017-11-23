---
title: Tipo de datos EnumString (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
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
apiname: EnumString Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- EnumString
- urn:schemas-microsoft-com:xml-analysis#EnumString
- http://schemas.microsoft.com/analysisservices/2003/engine#EnumString
helpviewer_keywords: EnumString data type
ms.assetid: 9214195e-4539-419b-95ec-b7aa75e033ab
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7f3365cbe5ad69fb81ab1231b2d09fd593ada3ac
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="enumstring-data-type-xmla"></a>Tipo de datos EnumString (XMLA)
  Define un tipo de datos derivado que representa un conjunto de constantes con nombre para un enumerador determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<EnumString>...</EnumString>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|**string**|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|Ninguno|  
|Elementos derivados|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 XML for Analysis (XMLA) utiliza enumeraciones para limitar los valores de cadena a un conjunto de valores que se pueden comprobar. **EnumString** utiliza el tipo de datos XML estándar **string** . Los valores concretos para cada una de las constantes con nombre se especifican con la definición del enumerador. Los enumeradores se definen agregándolos a la [DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md) de filas de esquema y se pueden recuperar mediante el uso de la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) tipo de solicitud de método con el DISCOVER_ENUMERATORS.  
  
 En la tabla siguiente describe los enumeradores admitidos por una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Enumerador|Descripción|  
|----------------|-----------------|  
|ProviderType|Es compatible con la columna ProviderType en el [DISCOVER_DATASOURCES](../../../analysis-services/schema-rowsets/xml/discover-datasources-rowset.md) de filas de esquema, que determina el tipo de datos que pueden devolver un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.<br /><br /> Esta enumeración también admite la propiedad XMLA, **ProviderType**, que determina los tipos de proveedor admitidos por un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. Esta enumeración también se utiliza en el conjunto de filas de esquema DISCOVER_DATASOURCES.<br /><br /> Para obtener más información acerca de **ProviderType**, consulte [admite propiedades XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|AuthenticationMode|Admite la columna AuthenticationMode en el conjunto de filas de esquema DISCOVER_DATASOURCES, que determina las credenciales de seguridad que se deben pasar para tener acceso a una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|PropertyAccessType|Es compatible con la columna PropertyAccessType en el [DISCOVER_PROPERTIES](../../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md) de filas de esquema, que determina el tipo de acceso disponible para una propiedad XMLA.|  
|StateSupport|Admite la propiedad XMLA, **Soporteestado**, que determina el nivel de Estados admitido por un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.<br /><br /> Para obtener más información acerca de **Soporteestado**, consulte [admite propiedades XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|StateActionVerb|Contiene una lista de verbos admitida por XMLA en los encabezados SOAP y que se utilizan para iniciar, identificar y finalizar una sesión.<br /><br /> Para obtener más información acerca de las sesiones, consulte [administrar conexiones y sesiones &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).|  
|ResultsetFormat|Admite la propiedad XMLA, **formato**, que determina el tipo de datos devueltos en un [raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento.<br /><br /> Para obtener más información acerca de **formato**, consulte [admite propiedades XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetAxisFormat|Admite la propiedad XMLA **AxisFormat**, que determina el formato de la información de eje devuelta en un elemento **root** que contiene datos multidimensionales.<br /><br /> Para obtener más información acerca de **AxisFormat**, consulte [admite propiedades XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetContents|Admite la propiedad XMLA **Content**, que determina si se devuelven datos o metadatos en un elemento **root** .<br /><br /> Para obtener más información acerca de **contenido**, consulte [admite propiedades XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|MDXSupportLevel|Admite la propiedad XMLA, **MDXSupport**, lo que indica el nivel de compatibilidad de expresiones multidimensionales (MDX) disponible en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.<br /><br /> Para obtener más información acerca de **MDXSupport**, consulte [admite propiedades XMLA &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40; XMLA &#41;](../../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)  
  
  
