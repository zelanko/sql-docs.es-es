---
title: Elemento Statement (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- Statement Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Statement
- microsoft.xml.analysis.statement
- urn:schemas-microsoft-com:xml-analysis#Statement
helpviewer_keywords:
- Statement command
ms.assetid: bfedc03c-d476-4d55-b5fd-36169f01351a
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 172e9961945bceca25e7826d5035f4b33ae797a5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="statement-element-xmla"></a>Elemento Statement (XMLA)
  Contiene una consulta o instrucción que se envíe mediante la **Execute** método a una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Statement>...</Statement>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **instrucción** comando ejecuta una consulta o instrucción en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite los lenguajes siguientes:  
  
-   Expresiones multidimensionales (MDX)  
  
-   Extensiones de minería de datos (MDX)  
  
-   Un subconjunto de Lenguaje de consulta estructurado (SQL)  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

