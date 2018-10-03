---
title: Elemento error (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Error Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.error
- http://schemas.microsoft.com/analysisservices/2003/engine#Error
- urn:schemas-microsoft-com:xml-analysis#Error
helpviewer_keywords:
- Error element
ms.assetid: add670cb-cab2-42be-91a3-d0c385f29d16
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5b9b961a0d8d5a33cb0869b72e0250dee5456ca7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210155"
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[de mensaje](message-element-xmla.md)|  
  
## <a name="child-elements"></a>Elementos secundarios  
  
|Ancestor|Elementos secundarios|  
|--------------|--------------------|  
|[de mensaje](message-element-xmla.md)|None|  
|[Celda](cell-element-mddataset-xmla.md), [fila](description-element-xmla.md), [ErrorCode](errorcode-element-xmla.md), [HelpFile](file-element-xmla.md), [origen](source-element-error-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|ErrorCode|Requiere `UnsignedInt` atributo (solo cuando `Message` es el elemento primario.) Contiene el código de devolución numérico del error.|  
|Severity|Opcional `String` atributo (solo cuando `Message` es el elemento primario.) Contiene la gravedad del error.|  
|Descripción|Opcional `String` atributo (solo cuando `Message` es el elemento primario.) Contiene el texto descriptivo del error.|  
|Source|Opcional `String` atributo (solo cuando `Message` es el elemento primario.) Contiene el nombre del componente que generó el error.|  
|HelpFile|Opcional `String` atributo (solo cuando `Message` es el elemento primario.) Contiene la ruta de acceso o dirección URL del archivo de Ayuda o tema que describe el error.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Elemento Warning &#40;XMLA&#41;](warning-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
