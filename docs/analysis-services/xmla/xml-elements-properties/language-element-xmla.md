---
title: Elemento del lenguaje (XMLA) | Documentos de Microsoft
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
apiname: Language Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Language
- microsoft.xml.analysis.language
- http://schemas.microsoft.com/analysisservices/2003/engine#Language
helpviewer_keywords: Language element
ms.assetid: cd998202-e43f-4c6c-8727-a15a76a520ea
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 3ab4266ed5d65bf4adbc4ce626024b650c46de9b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="language-element-xmla"></a>Elemento Language (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene el identificador de configuración regional (LCID) para el elemento primario [traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md) elemento.  
  
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
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Traducción](../../../analysis-services/xmla/xml-elements-properties/translation-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **lenguaje** elemento especifica el LCID utilizado por el elemento primario **traducción** elemento que se va a asignar la **nombre** elemento del elemento primario **traducción** elemento a un miembro de atributo para el idioma especificado, durante un **insertar** o **actualización** comando.  
  
## <a name="see-also"></a>Vea también  
 [Insertar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)   
 [Name, elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/name-element-xmla.md)   
 [Actualizar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
