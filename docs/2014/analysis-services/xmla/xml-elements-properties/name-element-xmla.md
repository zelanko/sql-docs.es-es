---
title: Nombre de elemento (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Name
- urn:schemas-microsoft-com:xml-analysis#Name
- microsoft.xml.analysis.name
helpviewer_keywords:
- Name element
ms.assetid: cc1a93df-0b1b-4c38-9183-4f11c26fea6a
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 088dd6aa9ce8d9ecae3e3a8f293f64b3ddc93c70
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37194235"
---
# <a name="name-element-xmla"></a>Elemento Name (XMLA)
  Contiene el nombre de un miembro de atributo para el elemento primario [atributo](attribute-element-xmla.md) o [traducción](translation-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attribute> <!-- or Translation -->  
   ...  
   <Name>...</Name>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Antecesor o elemento primario:|Cardinalidad|  
|[Atributo](attribute-element-xmla.md)|1-1: Elemento necesario que se produce una vez y solo una vez.|  
|[Traducción](translation-element-xmla.md)|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Atributo](attribute-element-xmla.md), [traducción](translation-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Para los elementos `Attribute`, el elemento `Name` contiene el nombre del miembro de atributo que se va a insertar o actualiza durante el comando `Insert` o el comando `Update`, respectivamente.  
  
 Para los elementos `Translation`, el elemento `Name` contiene el título del miembro de atributo, en el idioma especificado por el elemento `Language` del objeto `Translation` primario. Si el elemento `Name` no se especifica o contiene una cadena vacía, se utiliza el valor del elemento `Name` del elemento `Attribute` que contiene el elemento `Translation`.  
  
## <a name="see-also"></a>Vea también  
 [Insertar elemento &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Elemento de lenguaje &#40;XMLA&#41;](language-element-xmla.md)   
 [Actualizar elemento &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
