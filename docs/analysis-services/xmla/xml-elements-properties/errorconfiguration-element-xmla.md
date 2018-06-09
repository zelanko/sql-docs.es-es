---
title: Elemento ErrorConfiguration (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 68d5b3a5e1e381b1fb65a12c0aa77adf318a36b8
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34575167"
---
# <a name="errorconfiguration-element-xmla"></a>Elemento ErrorConfiguration (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Especifica la configuración para controlar los errores que pueden producirse durante un [lote](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) o [proceso](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md) operación.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Batch> <!-- or Process -->  
   ...  
   <ErrorConfiguration>  
      <KeyErrorLimit>...</KeyErrorLimit>  
      <KeyErrorLogFile>...</KeyErrorLogFile>  
      <KeyErrorAction>...</KeyErrorAction>  
      <KeyErrorLimitAction>...</KeyErrorLimitAction>  
      <KeyNotFound>...</KeyNotFound>  
      <KeyDuplicate>...</KeyDuplicate>  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
      <NullKeyNotAllowed>...<NullKeyNotAllowed>  
   </ErrorConfiguration>  
   ...  
</Batch>  
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
|Elementos primarios|[Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md), [Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|Elementos secundarios|[KeyDuplicate](../../../analysis-services/scripting/properties/keyduplicate-element-assl.md), [KeyErrorAction](../../../analysis-services/scripting/properties/keyerroraction-element-assl.md), [KeyErrorLimit](../../../analysis-services/scripting/properties/keyerrorlimit-element-assl.md), [KeyErrorLimitAction](../../../analysis-services/scripting/properties/keyerrorlimitaction-element-assl.md), [KeyErrorLogFile](../../../analysis-services/scripting/properties/keyerrorlogfile-element-assl.md), [ KeyNotFound](../../../analysis-services/scripting/properties/keynotfound-element-assl.md), [NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md), [NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md)|  
  
## <a name="remarks"></a>Notas  
 La estructura de este elemento es idéntica a la del elemento **ErrorConfiguration** en el lenguaje de scripting de Analysis Services (ASSL). Para obtener más información sobre la **ErrorConfiguration** elemento, vea [elemento ErrorConfiguration &#40;ASSL&#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md).  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
