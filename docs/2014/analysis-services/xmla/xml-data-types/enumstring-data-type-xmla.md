---
title: Tipo de datos EnumString (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- EnumString Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- EnumString
- urn:schemas-microsoft-com:xml-analysis#EnumString
- http://schemas.microsoft.com/analysisservices/2003/engine#EnumString
helpviewer_keywords:
- EnumString data type
ms.assetid: 9214195e-4539-419b-95ec-b7aa75e033ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fb075a8c659fe264dbed7dd68654d1fb84fdf7a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210250"
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
|Tipos de datos base|`string`|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|None|  
|Elementos derivados|None|  
  
## <a name="remarks"></a>Comentarios  
 XML for Analysis (XMLA) utiliza enumeraciones para limitar los valores de cadena a un conjunto de valores que se pueden comprobar. `EnumString` utiliza el tipo de datos XML estándar `string`. Los valores concretos para cada una de las constantes con nombre se especifican con la definición del enumerador. Los enumeradores se definen agregándolos a la [DISCOVER_ENUMERATORS](../../schema-rowsets/xml/discover-enumerators-rowset.md) de filas de esquema y se pueden recuperar mediante el uso de la [Discover](../xml-elements-methods-discover.md) tipo de solicitud de método con el DISCOVER_ENUMERATORS.  
  
 En la tabla siguiente describe los enumeradores admitidos por una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
|Enumerador|Descripción|  
|----------------|-----------------|  
|ProviderType|Es compatible con la columna ProviderType en el [DISCOVER_DATASOURCES](../../schema-rowsets/xml/discover-datasources-rowset.md) de filas de esquema, que determina el tipo de datos que pueden devolver un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.<br /><br /> Esta enumeración también admite la propiedad XMLA, `ProviderType`, que determina los tipos de proveedor admitidos por una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Esta enumeración también se utiliza en el conjunto de filas de esquema DISCOVER_DATASOURCES.<br /><br /> Para obtener más información acerca de `ProviderType`, consulte [propiedades XMLA compatibles &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|AuthenticationMode|Admite la columna AuthenticationMode en el conjunto de filas de esquema DISCOVER_DATASOURCES, que determina las credenciales de seguridad que se deben pasar para tener acceso a una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|PropertyAccessType|Es compatible con la columna PropertyAccessType en el [DISCOVER_PROPERTIES](../../schema-rowsets/xml/discover-properties-rowset.md) de filas de esquema, que determina el tipo de acceso a una propiedad XMLA.|  
|StateSupport|Admite la propiedad XMLA `StateSupport`, que determina el nivel de disponibilidad de estados admitido por una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Para obtener más información acerca de `StateSupport`, consulte [propiedades XMLA compatibles &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|StateActionVerb|Contiene una lista de verbos admitida por XMLA en los encabezados SOAP y que se utilizan para iniciar, identificar y finalizar una sesión.<br /><br /> Para obtener más información acerca de las sesiones, vea [administrar conexiones y sesiones &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md).|  
|ResultsetFormat|Admite la propiedad XMLA, `Format`, que determina el tipo de datos devueltos en una [raíz](../xml-elements-properties/root-element-xmla.md) elemento.<br /><br /> Para obtener más información acerca de `Format`, consulte [propiedades XMLA compatibles &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetAxisFormat|Admite la propiedad XMLA `AxisFormat`, que determina el formato de la información de eje devuelta en un elemento `root` que contiene datos multidimensionales.<br /><br /> Para obtener más información acerca de `AxisFormat`, consulte [propiedades XMLA compatibles &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|ResultsetContents|Admite la propiedad XMLA `Content`, que determina si se devuelven datos o metadatos en un elemento `root`.<br /><br /> Para obtener más información acerca de `Content`, consulte [propiedades XMLA compatibles &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
|MDXSupportLevel|Admite la propiedad XMLA `MDXSupport`, que indica el nivel de compatibilidad con las Expresiones multidimensionales (MDX) disponible en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].<br /><br /> Para obtener más información acerca de `MDXSupport`, consulte [propiedades XMLA compatibles &#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md).|  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  
