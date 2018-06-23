---
title: Tipo de datos TimeAttributeBinding (ASSL) | Documentos de Microsoft
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
- TimeAttributeBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TimeAttributeBinding
helpviewer_keywords:
- TimeAttributeBinding data type
ms.assetid: e8317b1c-a83a-4074-9538-400792500985
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7422bc4f3101b4ecbbb004583fed61801c9dfad7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108432"
---
# <a name="timeattributebinding-data-type-assl"></a>Tipo de datos TimeAttributeBinding (ASSL)
  Define un tipo de datos derivado que representa un enlace "marcador de posición" para los elementos de datos generados en una dimensión de tiempo del servidor, como pueden ser las columnas de clave de un atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TimeAttributeBinding>  
   <!-- TimeAttributeBinding has no child elements other than those inherited from Binding -->  
</TimeAttributeBinding>  
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
|Elementos secundarios|None|  
|Elementos derivados|Vea [enlace](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información sobre la `Binding` tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la `Binding` tipo y la jerarquía de herencia de `Binding` tipos, consulte [tipo de datos de enlace &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 Para obtener información general de enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;SSAS multidimensionales&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TimeAttributeBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  