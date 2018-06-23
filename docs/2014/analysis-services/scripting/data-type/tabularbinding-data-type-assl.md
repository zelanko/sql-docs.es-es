---
title: Tipo de datos TabularBinding (ASSL) | Documentos de Microsoft
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
- TabularBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TabularBinding
helpviewer_keywords:
- TabularBinding data type
ms.assetid: 24587e34-20be-4693-81d8-038a6fc4e8ee
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 59206b9dd0d9f61ee0915076cd76fc36bdab9322
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108194"
---
# <a name="tabularbinding-data-type-assl"></a>Tipo de datos TabularBinding (ASSL)
  Define un tipo de datos derivado abstracto que representa un enlace con un elemento tabular, como una tabla o una dimensión de cubo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TabularBinding>  
   <!-- The TabularBinding element has no child elements other than those inherited from Binding -->  
</TabularBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Enlace](binding-data-type-assl.md)|  
|Tipos de datos derivados|[DSVTableBinding](tablebinding-data-type-assl.md), [QueryBinding](querybinding-data-type-assl.md), [TableBinding](tablebinding-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|None|  
|Elementos derivados|Vea [enlace](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Notas  
 Para obtener información adicional sobre la `Binding` tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) de la `Binding` tipo y la jerarquía de herencia de `Binding` tipos, consulte [tipo de enlace de datos &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para obtener información general de enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;SSAS multidimensionales&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TabularBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  