---
title: Elemento DisplayFolder (ASSL) | Documentos de Microsoft
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6986e1dc728591f9540b533052ef8fd135aca1b0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="displayfolder-element-assl"></a>Elemento DisplayFolder (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Especifica la carpeta en la que se enumerará el elemento primario. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] las aplicaciones para desarrolladores y administradores pueden admitir el uso de carpetas para mostrar para categorizar visualmente múltiples elementos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<CalculationProperty> <!-- or Hierarchy, Kpi, Measure, Translation -->  
   ...  
   <DisplayFolder>...</DisplayFolder>  
   ...  
</CalculationProperty>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[CalculationProperty](../../../analysis-services/scripting/objects/calculationproperty-element-assl.md), [jerarquía](../../../analysis-services/scripting/objects/hierarchy-element-assl.md), [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md), [medida](../../../analysis-services/scripting/objects/measure-element-assl.md), [traducción](../../../analysis-services/scripting/objects/translation-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 En los cubos más grandes, puede haber cientos de medidas y jerarquías. La propiedad **DisplayFolder** define la apariencia del usuario en el cliente. El valor de la propiedad **DisplayFolder** puede contener cualquiera de las opciones siguientes:  
  
-   Puede estar vacío, lo que indica que la medida no pertenece a una carpeta.  
  
-   Puede contener un único nombre de carpeta, lo que indica que la medida debería representarse como perteneciente a una carpeta con el mismo nombre.  
  
-   Contienen varios nombres de carpeta separados por una barra diagonal inversa (\\), lo que indica una jerarquía de carpetas incrustada.  
  
 El **DisplayFolder** propiedad se aplica a **CalculationProperty** if solo elementos el valor de [CalculationType](../../../analysis-services/scripting/properties/calculationtype-element-assl.md) está establecido en *miembro* .  
  
 Los elementos que corresponden a los elementos primarios de **DisplayFolder** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.CalculationProperty>, <xref:Microsoft.AnalysisServices.Hierarchy>, <xref:Microsoft.AnalysisServices.Kpi>, <xref:Microsoft.AnalysisServices.Measure>, y <xref:Microsoft.AnalysisServices.Translation>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento CalculationProperties &#40;ASSL&#41;](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)   
 [Elemento MdxScript &#40;ASSL&#41;](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)   
 [Elemento MdxScripts &#40;ASSL&#41;](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)   
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
