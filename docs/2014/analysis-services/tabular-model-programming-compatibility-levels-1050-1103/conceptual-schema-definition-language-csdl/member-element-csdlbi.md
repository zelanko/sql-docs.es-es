---
title: Member, elemento (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f193cb746b8df43c33aa65ea3d69d87ab7c36655
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218835"
---
# <a name="member-element-csdlbi"></a>Member, elemento (CSDLBI)
  El elemento Member es un tipo complejo que actúa como base para otros elementos.  
  
 Sus atributos pueden aparecer en columnas, medidas, propiedades de navegación, jerarquías y niveles.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento Member.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Nombre||El nombre dado al miembro (una columna, medida, propiedad de navegación, jerarquía o un nivel) definido por la implementación del tipo TMember|  
|Caption|Sí|El nombre para mostrar del miembro.|  
|ContextualNameRule|Sí|El formato de nombres utilizado para eliminar la ambigüedad de los miembros. El contenido de este atributo lo define el tipo simple ContextualNameRule.|  
|Hidden||Valor booleano que indica si el miembro estará oculto al cliente.<br /><br /> El valor predeterminado es false, lo que significa que las columnas están visibles en el cliente.|  
|ReferenceName||El identificador utilizado para hacer referencia al miembro en una consulta de DAX. Si se omite este atributo, se usa el nombre del campo.|  
  
## <a name="contextualnamerule-element"></a>Elemento ContextualNameRule  
 Este tipo simple define el formato de nombres utilizado para eliminar la ambigüedad de los miembros.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|None|Utiliza el nombre del atributo.|  
|Contexto|Utiliza el nombre de la relación entrante.|  
|Mezcla|Concatena el nombre de la relación de entrada y el nombre de la propiedad.|  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
