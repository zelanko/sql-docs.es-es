---
title: Elemento DatabaseID (XMLA) | Documentos de Microsoft
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
- DatabaseID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.databaseid
- urn:schemas-microsoft-com:xml-analysis#DatabaseID
- http://schemas.microsoft.com/analysisservices/2003/engine#DatabaseID
helpviewer_keywords:
- DatabaseID element
ms.assetid: 2df720dd-9b42-449a-9df6-0d12930603f0
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: fec0d96ac6bb69868e5bab389033ffd975219182
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198516"
---
# <a name="databaseid-element-xmla"></a>Elemento DatabaseID (XMLA)
  Identifica una base de datos dentro de un elemento primario que contiene una referencia de objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Object> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <DatabaseID>...</DatabaseID>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
  
 **Cardinalidad**  
  
|Antecesor o elemento primario|Cardinalidad|  
|------------------------|-----------------|  
|[Source](source-element-xmla.md), [Target](../xml-elements-properties/target-element-xmla.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|Todos las demás|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Object](object-element-xmla.md), [ParentObject](parentobject-element-xmla.md), [Source](source-element-xmla.md), [Target](../xml-elements-properties/target-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  