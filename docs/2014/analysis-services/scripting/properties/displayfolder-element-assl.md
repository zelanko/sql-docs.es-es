---
title: Elemento DisplayFolder (ASSL) | Microsoft Docs
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
- DisplayFolder Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DisplayFolder
helpviewer_keywords:
- DisplayFolder element
ms.assetid: 55184c02-03e7-4d6c-b87a-d4d34bc11d0e
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 646a98170e24c36841ab445bf87897a0b4e9686f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293205"
---
# <a name="displayfolder-element-assl"></a>Elemento DisplayFolder (ASSL)
  Especifica la carpeta en la que se enumerará el elemento primario. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] las aplicaciones para desarrolladores y administradores pueden admitir el uso de carpetas para mostrar a fin de categorizar visualmente múltiples elementos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CalculationProperty](../objects/calculationproperty-element-assl.md), [jerarquía](../objects/hierarchy-element-assl.md), [Kpi](../objects/kpi-element-assl.md), [medida](../objects/measure-element-assl.md), [traducción](../objects/translation-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 En los cubos más grandes, puede haber cientos de medidas y jerarquías. La propiedad `DisplayFolder` define la apariencia del usuario en el cliente. El valor de la propiedad `DisplayFolder` puede contener cualquiera de las opciones siguientes:  
  
-   Puede estar vacío, lo que indica que la medida no pertenece a una carpeta.  
  
-   Puede contener un único nombre de carpeta, lo que indica que la medida debería representarse como perteneciente a una carpeta con el mismo nombre.  
  
-   Contener varios nombres de carpetas separados por una barra diagonal inversa (\\), que indica una jerarquía de carpetas incrustada.  
  
 El `DisplayFolder` propiedad se aplica a `CalculationProperty` solo si de elementos del valor de [CalculationType](calculationtype-element-assl.md) está establecido en *miembro*.  
  
 Los elementos que corresponden a los elementos primarios de `DisplayFolder` en el modelo de objetos de Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Hierarchy>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.Measure> y <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento CalculationProperties &#40;ASSL&#41;](../collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../collections/mdxscripts-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
