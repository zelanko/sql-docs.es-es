---
title: Elemento error (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f223bff2dced01c2b3f954ca14242b1a35c93813
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576557"
---
# <a name="error-element-xmla"></a>Elemento Error (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene información sobre un error devuelto por una instancia de Analysis Services.  
  
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
|Elementos primarios|[de mensaje](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|Elementos secundarios|Vea la tabla siguiente.|  
  
|Ancestor|Elementos secundarios|  
|--------------|--------------------|  
|[de mensaje](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|None|  
|[Celda](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md), [filas](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Descripción](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md), [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md), [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md), [origen](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|ErrorCode|Requiere **UnsignedInt** atributo (solo cuando **mensaje** es el elemento primario.) Contiene el código de devolución numérico del error.|  
|Severity|Opcional **cadena** atributo (solo cuando **mensaje** es el elemento primario.) Contiene la gravedad del error.|  
|Descripción|Opcional **cadena** atributo (solo cuando **mensaje** es el elemento primario.) Contiene el texto descriptivo del error.|  
|Source|Opcional **cadena** atributo (solo cuando **mensaje** es el elemento primario.) Contiene el nombre del componente que generó el error.|  
|HelpFile|Opcional **cadena** atributo (solo cuando **mensaje** es el elemento primario.) Contiene la ruta de acceso o dirección URL del archivo de Ayuda o tema que describe el error.|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también
 [Elemento Warning &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
