---
title: Elemento Warning (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
apiname: Warning Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Warning
- microsoft.xml.analysis.warning
- http://schemas.microsoft.com/analysisservices/2003/engine#Warning
helpviewer_keywords: Warning element
ms.assetid: a34a6caa-4b68-486b-8f50-cdc124c65888
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d4962988a5c21183ac6e4f841c43a422eb48528e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="warning-element-xmla"></a>Elemento Warning (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene información sobre una advertencia devuelta por una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[de mensaje](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|ErrorCode|Atributo **UnsignedInt** requerido. Contiene el código de devolución numérico de la advertencia.|  
|Gravedad|Atributo **String** opcional. Contiene la gravedad de la advertencia.|  
|Descripción|Atributo **String** opcional. Contiene el texto descriptivo de la advertencia.|  
|Origen|Atributo **String** opcional. Contiene el nombre del componente que generó la advertencia.|  
|HelpFile|Atributo **String** opcional. Contiene la ruta de acceso o dirección URL del archivo de Ayuda o tema que describe la advertencia.|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Error de elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
