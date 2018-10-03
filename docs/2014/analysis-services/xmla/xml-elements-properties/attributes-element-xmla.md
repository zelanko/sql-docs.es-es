---
title: Atributos de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Attributes Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Attributes
- microsoft.xml.analysis.attributes
- urn:schemas-microsoft-com:xml-analysis#Attributes
helpviewer_keywords:
- Attributes element
ms.assetid: c0393de8-44e8-46de-af78-1fd66c218521
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d2d5b29116a2ad248540f51ed84d677048352c2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140415"
---
# <a name="attributes-element-xmla"></a>Elemento Attributes (XMLA)
  Contiene una colección de elementos [Attribute](attribute-element-xmla.md) utilizada por los comandos primarios [Insert](../xml-elements-commands/insert-element-xmla.md) o [Update](../xml-elements-commands/update-element-xmla.md) , o por el elemento primario [Where](where-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Insert > <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Attributes>  
      <Attribute>...</Attribute>  
   </Attributes>  
   ...  
</Insert>  
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
|Elementos primarios|[Insert](../xml-elements-commands/insert-element-xmla.md), [Update](../xml-elements-commands/update-element-xmla.md), [Where](where-element-xmla.md)|  
|Elementos secundarios|[Atributo](attribute-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
