---
title: Elemento ConnectionString (XMLA) | Documentos de Microsoft
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
- ConnectionString Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.connectionstring
- urn:schemas-microsoft-com:xml-analysis#ConnectionString
- http://schemas.microsoft.com/analysisservices/2003/engine#ConnectionString
helpviewer_keywords:
- ConnectionString element
ms.assetid: 3b0575aa-79ed-4f14-ae7e-dd587af4cdb1
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 12d69bfe2b8dc8bda91bc873167bb3208203d728
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104788"
---
# <a name="connectionstring-element-xmla"></a>Elemento ConnectionString (XMLA)
  Contiene una cadena de conexión utilizada por el elemento primario [ubicación](location-element-xmla.md) o [origen](source-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Location> <!-- or Source -->  
   ...  
   <ConnectionString>...</ConnectionString>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad - antecesor o elemento primario|Cardinalidad|  
|[Ubicación](location-element-xmla.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|[Source](source-element-xmla.md)|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Ubicación](location-element-xmla.md), [origen](source-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para los elementos `Location`, el elemento `ConnectionString` contiene la cadena de conexión que utiliza el comando `Restore` o `Synchronize` para actualizar un origen de datos local o conectarse a una instancia remota.  
  
 Para los elementos `Source`, el elemento `ConnectionString` contiene la cadena de conexión utilizada por el comando `Synchronize` para conectarse a la instancia de origen.  
  
 Para obtener más información acerca de la copia de seguridad y restauración de objetos, consulte [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento restore &#40;XMLA&#41;](../xml-elements-commands/restore-element-xmla.md)   
 [Elemento Synchronize &#40;XMLA&#41;](../xml-elements-commands/synchronize-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  