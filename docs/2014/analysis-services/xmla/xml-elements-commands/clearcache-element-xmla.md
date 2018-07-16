---
title: Elemento ClearCache (XMLA) | Microsoft Docs
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
- ClearCache Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ClearCache
- urn:schemas-microsoft-com:xml-analysis#ClearCache
- microsoft.xml.analysis.clearcache
helpviewer_keywords:
- ClearCache command
ms.assetid: e154b489-e443-469a-9490-43c62da62e11
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 37b43439705b3288530a919f77da7b0ead461b35
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188972"
---
# <a name="clearcache-element-xmla"></a>Elemento ClearCache (XMLA)
  Borra la memoria caché para el objeto especificado en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <ClearCache>  
      <Object>...</Object>  
   </ClearCache>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Objeto](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El `ClearCache` comando vacia la caché de una base de datos especificada, dimensión, cubo, grupo de medida o partición en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. Si un objeto distinto de una base de datos, dimensión, cubo, grupo de medida o partición se especifica en el elemento `Object`, se produce un error.  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
