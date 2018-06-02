---
title: Elemento del lenguaje (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4b2e3a188a9681508473394a6323457cc4fa1726
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575437"
---
# <a name="language-element-xmla"></a>Elemento Language (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene el identificador de configuración regional (LCID) para el elemento primario [traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Translation>  
   ...  
   <Language>...</Language>  
   ...  
</Translation>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Integer|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El **lenguaje** elemento especifica el LCID utilizado por el elemento primario **traducción** elemento que se va a asignar la **nombre** elemento del elemento primario **traducción** elemento a un miembro de atributo para el idioma especificado, durante un **insertar** o **actualización** comando.  
  
## <a name="see-also"></a>Vea también
 [Insertar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Nombre de elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)   
 [Actualizar elemento &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
