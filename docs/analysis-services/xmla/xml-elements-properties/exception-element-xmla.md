---
title: Elemento Exception (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- Exception Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Exception
- urn:schemas-microsoft-com:xml-analysis#Exception
- microsoft.xml.analysis.exception
helpviewer_keywords:
- Exception element
ms.assetid: 0be4cc2f-c03e-490a-a6f7-8b1ede5d09ba
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0c83900d85d698c5f9b2c0bdca2c197ab4ce05b1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="exception-element-xmla"></a>Elemento Exception (XMLA)
  Indica que se devolvió una excepción desde una [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) llamada al método.  
  
 **Namespace**`http://schemas.microsoft.com/analysisservices/2003/exception`  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<root>  
   ...  
   <Exception />  
   ...  
</root>  
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
|Elementos primarios|[raíz](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Si se produce un error durante la ejecución de una llamada al método **Discover** o un comando XMLA único en una llamada al método **Execute** que impide la finalización del método o del comando, el elemento **root** para ese método o el comando contiene un elemento **Exception** y un elemento **Messages** . El elemento **Exception** indica que se ha producido un error que ha impedido la correcta ejecución del método o del comando, y que el elemento **Messages** contiene la lista de errores o mensajes de advertencia relacionados con el error.  
  
## <a name="see-also"></a>Vea también  
 [Messages, elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

