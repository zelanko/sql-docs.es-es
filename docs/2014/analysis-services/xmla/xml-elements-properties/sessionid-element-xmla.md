---
title: Elemento SessionID (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- SessionID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#SessionID
- http://schemas.microsoft.com/analysisservices/2003/engine#SessionID
- microsoft.xml.analysis.sessionid
helpviewer_keywords:
- SessionID element
ms.assetid: 18220e00-76cf-48f6-9465-200465a0c553
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 00f89635ae8415c0c5172ed212686dade890510a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48211415"
---
# <a name="sessionid-element-xmla"></a>Elemento SessionID (XMLA)
  Identifica una sesión activa en el que se va a ejecutar el elemento primario [cancelar](../xml-elements-commands/cancel-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cancel>  
   ...  
   <SessionID>...</SessionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cancelar](../xml-elements-commands/cancel-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Elemento CancelAssociated &#40;XMLA&#41;](cancelassociated-element-xmla.md)   
 [Elemento ConnectionID &#40;XMLA&#41;](id-element-xmla.md)   
 [Elemento SPID &#40;XMLA&#41;](spid-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
