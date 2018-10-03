---
title: Elemento Exception (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Exception Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Exception
- urn:schemas-microsoft-com:xml-analysis#Exception
- microsoft.xml.analysis.exception
helpviewer_keywords:
- Exception element
ms.assetid: 0be4cc2f-c03e-490a-a6f7-8b1ede5d09ba
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e447bda3d52ac63125f3a96769fcee2c0158494c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178545"
---
# <a name="exception-element-xmla"></a>Elemento Exception (XMLA)
  Indica que se devolvió una excepción desde una [Discover](../xml-elements-methods-discover.md) o [Execute](../xml-elements-methods-execute.md) llamada al método.  
  
 **Namespace** http://schemas.microsoft.com/analysisservices/2003/exception  
  
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Raíz](root-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Si se produce un error durante la ejecución de una llamada al método  `Discover` o un comando XMLA único en una llamada al método `Execute` que impide la finalización del método o del comando, el elemento `root` para ese método o el comando contiene un elemento `Exception` y un elemento `Messages`. El elemento `Exception` indica que se ha producido un error que ha impedido la correcta ejecución del método o del comando, y que el elemento `Messages` contiene la lista de errores o mensajes de advertencia relacionados con el error.  
  
## <a name="see-also"></a>Vea también  
 [Mensajes elemento &#40;XMLA&#41;](messages-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
