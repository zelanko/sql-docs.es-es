---
title: Elemento Warning (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 73662315d294cade8b344f8967923fe15e94f886
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576737"
---
# <a name="warning-element-xmla"></a>Elemento Warning (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene información sobre una advertencia devuelta por una instancia de Analysis Services.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Message>  
   <Warning   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
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
|Elementos secundarios|None|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|ErrorCode|Atributo **UnsignedInt** requerido. Contiene el código de devolución numérico de la advertencia.|  
|Severity|Atributo **String** opcional. Contiene la gravedad de la advertencia.|  
|Descripción|Atributo **String** opcional. Contiene el texto descriptivo de la advertencia.|  
|Source|Atributo **String** opcional. Contiene el nombre del componente que generó la advertencia.|  
|HelpFile|Atributo **String** opcional. Contiene la ruta de acceso o dirección URL del archivo de Ayuda o tema que describe la advertencia.|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también
 [Elemento error &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
