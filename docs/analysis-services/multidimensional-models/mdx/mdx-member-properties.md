---
title: Usar las propiedades de miembro (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DIMENSION PROPERTIES keyword
- Properties function
- member properties [MDX]
- members [MDX], properties
ms.assetid: 26b5ad08-3799-4a5e-89f3-dca25e637d45
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1c3f560f0be83b17b31db8cfd46bc0b7939ee05d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdx-member-properties"></a>Propiedades de miembro MDX
  Las propiedades de miembro cubren la información básica de todos los miembros de cada tupla. Esta información básica incluye el nombre del miembro, el nivel primario, el número de secundarios, etc. Las propiedades de miembro están disponibles para todos los miembros de un determinado nivel. En términos de organización, las propiedades de miembro se tratan como datos organizados dimensionalmente, almacenados en una sola dimensión.  
  
> [!NOTE]  
>  En [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], las propiedades de miembro se conocen como relaciones de atributo. Para obtener más información, vea [Relaciones de atributo](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md).  
  
 Las propiedades de miembro pueden ser *intrínsecas* o *personalizadas*:  
  
 Propiedades de miembro intrínsecas  
 Todos los miembros admiten propiedades de miembro intrínsecas, como el valor con formato de un miembro, mientras que las dimensiones y los niveles proporcionan propiedades de miembro intrínsecas adicionales de nivel y dimensión, como el Id. de un miembro.  
  
 Para obtener más información, vea [Propiedades de miembro intrínsecas &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md).  
  
 Propiedades de miembro definidas por el usuario  
 Los miembros suelen tener propiedades adicionales asociadas. Por ejemplo, el nivel Products puede ofrecer las propiedades SKU, SRP, Weight y Volume para cada producto. Estas propiedades no son miembros, pero contienen información adicional sobre los miembros del nivel Products.  
  
 Para obtener más información, vea [Propiedades de miembro definidas por el usuario &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
 Tanto las propiedades de miembro intrínsecas como las definidas por el usuario pueden recuperarse mediante la palabra clave **PROPERTIES** o la función [Properties](../../../mdx/properties-mdx.md).  
  
## <a name="using-the-properties-keyword"></a>Usar la palabra clave PROPERTIES  
 La palabra clave **PROPERTIES** especifica las propiedades de miembro que deben utilizarse para una dimensión de eje determinada. La palabra clave **PROPERTIES** se incrusta en la cláusula `<axis specification>` de la instrucción [SELECT](../../../mdx/mdx-data-manipulation-select.md) MDX:  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
```  
  
 La cláusula `<axis_specification>` incluye una cláusula `<dim_props>` opcional, como se ilustra en la siguiente sintaxis:  
  
```  
<axis_specification> ::= <set> [<dim_props>] ON <axis_name>  
```  
  
> [!NOTE]  
>  Para obtener más información sobre los valores `<set>` y `<axis_name>`, vea [Especificar el contenido de un eje de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-specify-the-contents-of-a-query-axis.md).  
  
 La palabra clave `<dim_props>` permite realizar consultas sobre propiedades de dimensiones, niveles y miembros mediante la palabra clave **PROPERTIES** . En la siguiente sintaxis se muestra el formato de la cláusula `<dim_props>` :  
  
```  
<dim_props> ::= [DIMENSION] PROPERTIES <property> [,<property>...]  
```  
  
 El análisis detallado de la sintaxis `<property>` varía según la propiedad sobre la que se efectúe la consulta:  
  
-   Las propiedades de miembro intrínsecas contextuales deben ir precedidas del nombre de la dimensión o el nivel. Sin embargo, el nombre de las propiedades de miembro intrínsecas no contextuales no puede completarse con el de la dimensión o el nivel. Para obtener más información sobre cómo usar la palabra clave **PROPERTIES** con las propiedades de miembro intrínsecas, vea [Propiedades de miembro intrínsecas &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties.md).  
  
-   Las propiedades de miembro definidas por el usuario deben ir precedidas por el nombre del nivel en el que residen. Para obtener más información sobre cómo usar la palabra clave **PROPERTIES** con las propiedades de miembro definidas por el usuario, vea [Propiedades de miembro definidas por el usuario &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear y usar los valores de propiedad &#40;MDX&#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)  
  
  

