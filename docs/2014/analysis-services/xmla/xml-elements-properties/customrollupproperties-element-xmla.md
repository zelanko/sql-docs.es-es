---
title: Elemento CustomRollupProperties (XMLA) | Microsoft Docs
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
- CustomRollupProperties Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.customrollupproperties
- urn:schemas-microsoft-com:xml-analysis#CustomRollupProperties
- http://schemas.microsoft.com/analysisservices/2003/engine#CustomRollupProperties
helpviewer_keywords:
- CustomRollupProperties element
ms.assetid: 4abf0129-e529-4355-b8d5-6f4e6a88e796
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a564296dd022dece7ff20a7187c2c80bba9c6b7f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37233705"
---
# <a name="customrollupproperties-element-xmla"></a>Elemento CustomRollupProperties (XMLA)
  Contiene las propiedades de resumen personalizado para un miembro de atributo representado por el elemento primario [atributo](attribute-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Attribute>  
   ...  
   <CustomRollupProperties>...</CustomRollupProperties>  
   ...  
</Attribute>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Atributo](attribute-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento `CustomRollupProperties` contiene una expresión de Expresiones multidimensionales (MDX) que define las propiedades de resumen personalizado del miembro del atributo definido por el elemento primario `Attribute`.  
  
 Para obtener más información sobre las expresiones MDX, vea [expresiones &#40;MDX&#41;](/sql/mdx/expressions-mdx).  
  
## <a name="see-also"></a>Vea también  
 [Insertar elemento &#40;XMLA&#41;](../xml-elements-commands/insert-element-xmla.md)   
 [Actualizar elemento &#40;XMLA&#41;](../xml-elements-commands/update-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
