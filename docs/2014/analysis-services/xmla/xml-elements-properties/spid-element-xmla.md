---
title: Elemento SPID (XMLA) | Microsoft Docs
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
- SPID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#SPID
- microsoft.xml.analysis.spid
- urn:schemas-microsoft-com:xml-analysis#SPID
helpviewer_keywords:
- SPID element
ms.assetid: c4a54dcb-a0cd-4255-9e0f-a34eb990854f
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 27244dab841ac4793d66c6b177d5382ca7cdc7a7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167026"
---
# <a name="spid-element-xmla"></a>Elemento SPID (XMLA)
  Identifica un identificador de proceso de servidor activo (SPID) en el que se va a ejecutar el elemento primario [cancelar](../xml-elements-commands/cancel-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cancel>  
   ...  
   <SPID>...</SPID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Integer|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cancelar](../xml-elements-commands/cancel-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El `SPID` elemento representa el Id. (SPID) utilizado para una sesión determinada en una instancia de proceso de servidor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Elemento CancelAssociated &#40;XMLA&#41;](cancelassociated-element-xmla.md)   
 [Elemento ConnectionID &#40;XMLA&#41;](id-element-xmla.md)   
 [Elemento SessionID &#40;XMLA&#41;](sessionid-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
