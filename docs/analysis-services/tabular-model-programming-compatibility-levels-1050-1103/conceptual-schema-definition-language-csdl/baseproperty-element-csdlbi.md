---
title: BaseProperty, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b82b9b6f137b09768fbfdadb78d98f9cd293e81e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="baseproperty-element-csdlbi"></a>BaseProperty, elemento (CSDLBI)
  El elemento BaseProperty es un tipo complejo que actúa como base para otros elementos.  
  
 Sus atributos pueden aparecer en columnas y en medidas.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento BaseProperty.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Alignment|No|El nombre dado al miembro (una columna, medida, propiedad de navegación, jerarquía o un nivel) definido por la implementación del tipo Member|  
|FormatString|No|El nombre para mostrar del miembro.|  
|IsRightToLeft|No|Valor booleano que indica si el campo contiene texto que se puede leer de derecha a izquierda.<br /><br /> Si se omite este atributo, se utiliza el valor predeterminado (del modelo).|  
|SortDirection|No|Valor que indica cómo se suelen ordenar los valores de los campos. El contenido de este atributo lo define el tipo simple SortDirection.<br /><br /> Si se omite este atributo, se asigna una dirección de ordenación basándose en el tipo de datos del campo.|  
|Unidades|No|Símbolo que se aplica a los valores de los campos para expresar unidades.<br /><br /> Si se omite, las unidades son desconocidas.|  
  
## <a name="alignment-element"></a>Elemento Alignment  
 Este tipo simple define el formato de nombres utilizado para eliminar la ambigüedad de los miembros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Ninguno|Utiliza el nombre del atributo.|  
|Contexto|Utiliza el nombre de la relación entrante.|  
|Mezcla|Concatena el nombre de la relación entrante y el de la propiedad siguiendo las reglas de la gramática actual.|  
  
## <a name="sortdirection-element"></a>Elemento SortDirection  
 Este tipo simple define el formato de nombres utilizado para eliminar la ambigüedad de los miembros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Ninguno|Utiliza el nombre del atributo.|  
|Contexto|Utiliza el nombre de la relación entrante.|  
|Mezcla|Concatena el nombre de la relación de entrada y el nombre de la propiedad.|  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares en compatibilidad 1050 1103 a través de niveles](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  

