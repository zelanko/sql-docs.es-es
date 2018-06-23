---
title: Elemento Warning (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Warning Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Warning
- microsoft.xml.analysis.warning
- http://schemas.microsoft.com/analysisservices/2003/engine#Warning
helpviewer_keywords:
- Warning element
ms.assetid: a34a6caa-4b68-486b-8f50-cdc124c65888
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 398fb36522144ec52b8c47fec4c2d4b2b3c87909
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106614"
---
# <a name="warning-element-xmla"></a>Elemento Warning (XMLA)
  Contiene información sobre una advertencia devuelta por una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[de mensaje](message-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|ErrorCode|Necesario `UnsignedInt` atributo. Contiene el código de devolución numérico de la advertencia.|  
|Severity|Opcional `String` atributo. Contiene la gravedad de la advertencia.|  
|Descripción|Opcional `String` atributo. Contiene el texto descriptivo de la advertencia.|  
|Source|Opcional `String` atributo. Contiene el nombre del componente que generó la advertencia.|  
|Helpfile|Opcional `String` atributo. Contiene la ruta de acceso o dirección URL del archivo de Ayuda o tema que describe la advertencia.|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Elemento error &#40;XMLA&#41;](error-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  