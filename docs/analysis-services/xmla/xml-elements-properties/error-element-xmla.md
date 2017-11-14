---
title: Elemento error (XMLA) | Documentos de Microsoft
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
apiname:
- Error Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.error
- http://schemas.microsoft.com/analysisservices/2003/engine#Error
- urn:schemas-microsoft-com:xml-analysis#Error
helpviewer_keywords:
- Error element
ms.assetid: add670cb-cab2-42be-91a3-d0c385f29d16
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 214dc93af2f02f4bd47ac9d0199b0254fe2ab024
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="error-element-xmla"></a>Elemento Error (XMLA)
  Contiene información sobre un error devuelto por una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Message>  
   <Error   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
<!-- or -->  
<Cell><!-- or row -->  
   <!-- A child element -->  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception"  
         < ErrorCode>...</ErrorCode>  
         < Description>...</Description>  
         < Source>...</Source>  
         < HelpFile>...</HelpFile>  
      </Error>  
   <!-- /A child element -- >  
</Cell>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[de mensaje](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|Elementos secundarios|Vea la siguiente tabla.|  
  
|Ancestor|Elementos secundarios|  
|--------------|--------------------|  
|[de mensaje](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|Ninguno|  
|[Celda](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md), [filas](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Descripción](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md), [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md), [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md), [origen](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|ErrorCode|Requiere **UnsignedInt** atributo (solo cuando **mensaje** es el elemento primario.) Contiene el código de devolución numérico del error.|  
|Severity|Opcional **cadena** atributo (solo cuando **mensaje** es el elemento primario.) Contiene la gravedad del error.|  
|Description|Opcional **cadena** atributo (solo cuando **mensaje** es el elemento primario.) Contiene el texto descriptivo del error.|  
|Source|Opcional **cadena** atributo (solo cuando **mensaje** es el elemento primario.) Contiene el nombre del componente que generó el error.|  
|HelpFile|Opcional **cadena** atributo (solo cuando **mensaje** es el elemento primario.) Contiene la ruta de acceso o dirección URL del archivo de Ayuda o tema que describe el error.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Elemento Warning &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

