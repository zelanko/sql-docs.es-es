---
title: Member, elemento (CSDLBI) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 351cd8c622454626b8caa7547a4e8c73c4c49438
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="member-element-csdlbi"></a>Member, elemento (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]El elemento de miembro es un tipo complejo que actúa como base para otros elementos.  
  
 Sus atributos pueden aparecer en columnas, medidas, propiedades de navegación, jerarquías y niveles.  
  
## <a name="elements-and-attributes"></a>Atributos y elementos  
 En la tabla siguiente se enumeran los elementos y atributos que definen el elemento Member.  
  
|Nombre|Es obligatorio|Descripción|  
|----------|-----------------|-----------------|  
|Nombre||El nombre dado al miembro (una columna, medida, propiedad de navegación, jerarquía o un nivel) definido por la implementación del tipo TMember|  
|Caption|Sí|El nombre para mostrar del miembro.|  
|ContextualNameRule|Sí|El formato de nombres utilizado para eliminar la ambigüedad de los miembros. El contenido de este atributo lo define el tipo simple ContextualNameRule.|  
|Oculto||Valor booleano que indica si el miembro estará oculto al cliente.<br /><br /> El valor predeterminado es false, lo que significa que las columnas están visibles en el cliente.|  
|ReferenceName||El identificador utilizado para hacer referencia al miembro en una consulta de DAX. Si se omite este atributo, se usa el nombre del campo.|  
  
## <a name="contextualnamerule-element"></a>Elemento ContextualNameRule  
 Este tipo simple define el formato de nombres utilizado para eliminar la ambigüedad de los miembros.  
  
|Valor|Description|  
|-----------|-----------------|  
|Ninguno|Utiliza el nombre del atributo.|  
|Contexto|Utiliza el nombre de la relación entrante.|  
|Mezcla|Concatena el nombre de la relación de entrada y el nombre de la propiedad.|  
  
## <a name="see-also"></a>Vea también  
 [Descripción del modelo de objetos tabulares en compatibilidad 1050 1103 a través de niveles](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
