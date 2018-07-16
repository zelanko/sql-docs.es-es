---
title: Tipo de datos AttributeBinding (ASSL) | Microsoft Docs
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
- AttributeBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AttributeBinding
helpviewer_keywords:
- AttributeBinding data type
ms.assetid: 24d511a9-d0eb-4150-9f78-541e03963d67
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e475cb0ecb867daec6864fb5d078835e8fe95688
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279751"
---
# <a name="attributebinding-data-type-assl"></a>Tipo de datos AttributeBinding (ASSL)
  Define un tipo de datos derivado que representa un enlace para un [atributo](../objects/attribute-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<AttributeBinding>  
   <AttributeID>...</AttributeID>  
      <Type>...</Type>  
   <Ordinal>...</Ordinal>  
</AttributeBinding>  
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
|Elementos secundarios|[AttributeID](../properties/id-element-assl.md), [Ordinal](../properties/ordinal-element-assl.md), [tipo](../properties/type-element-binding-assl.md)|  
|Elementos derivados|Consulte [enlace](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información sobre la `Binding` tipo de datos, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) derivados de la `Binding` tipo de datos, vea [tipo de datos de enlace &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para obtener información general de los enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.AttributeBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
