---
title: Donde el elemento (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Where Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords: Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 50050fc4845161f18568aeb92e8bc4bb1ab49026
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="where-element-xmla"></a>Elemento Where (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Define una condición de filtro utilizada por el elemento primario [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md) o [actualización](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Drop> <!-- or Update -->  
   ...  
   <Where>  
      <Attributes>...</Attributes>  
   </Where>  
   ...  
</Insert>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|Elementos secundarios|[Atributos](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para los comandos **Drop**, el elemento **Where**, combinado con el elemento [DeleteWithDescendants](../../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md), identifica el ámbito de los miembros de atributo que se van a quitar.  
  
 Para los comandos **Update** , el elemento **Where** identifica el ámbito de los miembros de atributo que se van a actualizar. Es posible actualizar varios miembros de atributo utilizando una combinación de atributos incluidos en la colección **Attributes** del comando primario **Update** y la colección **Attributes** del elemento **Where** .  
  
 Para más información sobre cómo eliminar y actualizar miembros de atributos, vea [Insertar, actualizar y quitar miembros &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
