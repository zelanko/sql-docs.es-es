---
title: BaseProperty, elemento (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3dcea67deac28838f190947c0b890b86537536c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198815"
---
# <a name="baseproperty-element-csdlbi"></a>BaseProperty, elemento (CSDLBI)
  El elemento BaseProperty es un tipo complejo que actúa como base para otros elementos.  
  
 Sus atributos pueden aparecer en columnas y en medidas.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento BaseProperty.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Alignment|no|El nombre dado al miembro (una columna, medida, propiedad de navegación, jerarquía o un nivel) definido por la implementación del tipo Member|  
|FormatString|no|El nombre para mostrar del miembro.|  
|IsRightToLeft|no|Valor booleano que indica si el campo contiene texto que se puede leer de derecha a izquierda.<br /><br /> Si se omite este atributo, se utiliza el valor predeterminado (del modelo).|  
|SortDirection|no|Valor que indica cómo se suelen ordenar los valores de los campos. El contenido de este atributo lo define el tipo simple SortDirection.<br /><br /> Si se omite este atributo, se asigna una dirección de ordenación basándose en el tipo de datos del campo.|  
|Unidades|no|Símbolo que se aplica a los valores de los campos para expresar unidades.<br /><br /> Si se omite, las unidades son desconocidas.|  
  
## <a name="alignment-element"></a>Elemento Alignment  
 Este tipo simple define el formato de nombres utilizado para eliminar la ambigüedad de los miembros.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|None|Utiliza el nombre del atributo.|  
|Contexto|Utiliza el nombre de la relación entrante.|  
|Mezcla|Concatena el nombre de la relación entrante y el de la propiedad siguiendo las reglas de la gramática actual.|  
  
## <a name="sortdirection-element"></a>Elemento SortDirection  
 Este tipo simple define el formato de nombres utilizado para eliminar la ambigüedad de los miembros.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|None|Utiliza el nombre del atributo.|  
|Contexto|Utiliza el nombre de la relación entrante.|  
|Mezcla|Concatena el nombre de la relación de entrada y el nombre de la propiedad.|  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
