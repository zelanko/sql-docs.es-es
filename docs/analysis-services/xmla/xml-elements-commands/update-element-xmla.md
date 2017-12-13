---
title: Elemento Update (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
apiname: Update Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Update
- microsoft.xml.analysis.update
- http://schemas.microsoft.com/analysisservices/2003/engine#Update
helpviewer_keywords: Update command [XMLA]
ms.assetid: 324dcc16-865d-4d0a-b393-2b06c18ac807
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0f093a53c2b5b69e734812de0e4e14bee5a32d96
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="update-element-xmla"></a>Elemento Update (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Actualiza los miembros de una dimensión de atributo.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Update>  
      <Object>...</Object>  
      <MoveWithDescendants>...</MoveWithDescendants>  
      <Attributes>...</Attributes>  
      <Where>...</Where>  
   </Update>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Atributos](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md), [MoveWithDescendants](../../../analysis-services/xmla/xml-elements-properties/movewithdescendants-element-xmla.md), [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md), [donde](../../../analysis-services/xmla/xml-elements-properties/where-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El comando **Update** mueve los miembros de atributo dentro de una dimensión habilitada para escritura.  
  
 Para obtener más información acerca de cómo actualizar los miembros, vea [Insertar, actualizar y quitar miembros &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Eliminar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)   
 [Insertar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
