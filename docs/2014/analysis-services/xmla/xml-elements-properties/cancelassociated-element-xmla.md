---
title: Elemento CancelAssociated (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CancelAssociated Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cancelassociated
- urn:schemas-microsoft-com:xml-analysis#CancelAssociated
- http://schemas.microsoft.com/analysisservices/2003/engine#CancelAssociated
helpviewer_keywords:
- CancelAssociated element
ms.assetid: fd890440-d1a7-4c05-9e81-c81e6b8c274c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 294f1060c0a52c357e791d5b3db7ad87d0d98309
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126595"
---
# <a name="cancelassociated-element-xmla"></a>Elemento CancelAssociated (XMLA)
  Indica si el elemento primario [Cancel](../xml-elements-commands/cancel-element-xmla.md) debería cancelar todos los comandos asociados.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cancel>  
   ...  
   <ConnectionID>...</ConnectionID>  
   ...  
</Cancel>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|False|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cancelar](../xml-elements-commands/cancel-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Si se especifica este elemento y se establece en `True`, cada conexión correspondiente, sesiones y comando identificado en el elemento primario `Cancel` se cancela el comando.  
  
## <a name="see-also"></a>Vea también  
 [Elemento ConnectionID &#40;XMLA&#41;](id-element-xmla.md)   
 [Elemento SessionID &#40;XMLA&#41;](sessionid-element-xmla.md)   
 [Elemento SPID &#40;XMLA&#41;](spid-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
