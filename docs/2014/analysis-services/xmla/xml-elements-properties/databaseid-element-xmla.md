---
title: Elemento DatabaseID (XMLA) | Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce90874f5b6e0328434bf5f10f755fe0cfa65ddf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259321"
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
  
  
