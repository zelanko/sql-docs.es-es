---
title: Tipo de datos UserDefinedGroupBinding (ASSL) | Microsoft Docs
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
- UserDefinedGroupBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- UserDefinedGroupBinding
helpviewer_keywords:
- UserDefinedGroupBinding data type
ms.assetid: 70149929-0ff7-4a67-84bf-e94908ae7611
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a31c1867296ff00d8000b24640dfb44bef034a00
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194325"
---
# <a name="userdefinedgroupbinding-data-type-assl"></a>Tipo de datos UserDefinedGroupBinding (ASSL)
  Define un tipo de datos derivado que representa un agrupamiento definido por el usuario de un atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<UserDefinedGroupBinding>  
   <!-- The following elements extend Binding -->  
      <AttributeID>...</AttributeID>  
      <Groups>...</Groups>  
</UserDefinedGroupBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Enlace](binding-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[AttributeID](../properties/id-element-assl.md), [grupos](../collections/groups-element-assl.md)|  
|Elementos derivados|Consulte [enlace](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Notas  
 `UserDefinedGroupBinding` se trata automáticamente como un [AttributeBinding](attributebinding-data-type-assl.md), cuya [tipo](../properties/type-element-binding-assl.md) elemento está establecido en *todas*.  
  
 Para obtener más información sobre la `Binding` tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la `Binding` tipo y la jerarquía de herencia de `Binding` tipos, vea [tipo de enlace de datos &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para obtener información general de los enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.UserDefinedGroupBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
