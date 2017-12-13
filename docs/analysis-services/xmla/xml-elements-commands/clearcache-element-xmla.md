---
title: Elemento ClearCache (XMLA) | Documentos de Microsoft
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
apiname: ClearCache Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ClearCache
- urn:schemas-microsoft-com:xml-analysis#ClearCache
- microsoft.xml.analysis.clearcache
helpviewer_keywords: ClearCache command
ms.assetid: e154b489-e443-469a-9490-43c62da62e11
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d037f022f5235c0fdfe600f0295a2d053208787a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="clearcache-element-xmla"></a>Elemento ClearCache (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Borra la memoria caché para el objeto especificado en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <ClearCache>  
      <Object>...</Object>  
   </ClearCache>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Object](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **ClearCache** comando vacía la memoria caché para una base de datos especificada, dimensión, cubo, grupo de medida o partición en una [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. Si un objeto distinto de una base de datos, dimensión, cubo, grupo de medida o partición se especifica en el elemento **Object** , se produce un error.  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
