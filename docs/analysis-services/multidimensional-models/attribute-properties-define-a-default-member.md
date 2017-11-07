---
title: Definir un miembro predeterminado | Documentos de Microsoft
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
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 642c8ceb45d5a756f8fad396d0fb1bf48138afb0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---define-a-default-member"></a>Propiedades de atributo: definir a un miembro predeterminado
  El miembro predeterminado de una jerarquía de atributo se usa para evaluar expresiones cuando una jerarquía de atributo no se incluye en una consulta. El miembro predeterminado se omite cuando una consulta incluye una jerarquía de atributo o una jerarquía de usuario que contiene el atributo que da origen a la jerarquía de atributo. Esto se debe a que se utiliza el miembro especificado en la consulta.  
  
 El miembro predeterminado de una jerarquía de atributo se establece especificando un miembro de atributo como el valor de propiedad **DefaultMember** para la jerarquía de atributo. Puede establecer esta propiedad en la pestaña Estructura de dimensión en el Diseñador de dimensiones, o bien en el script de cálculo del cubo en la pestaña Cálculo en el Diseñador de cubos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. También puede especificar la propiedad **DefaultMember** para un rol de seguridad (reemplazando el miembro predeterminado establecido en la dimensión) en la pestaña Datos de dimensiones al definir la seguridad de dimensión. Para evitar problemas de resolución de nombres, defina el miembro predeterminado en el script MDX del cubo en las siguientes situaciones: si el cubo hace referencia a una dimensión de base de datos más de una vez, si la dimensión en el cubo tiene un nombre distinto al de la dimensión en la base de datos, o bien si desea tener miembros predeterminados diferentes en distintos cubos.  
  
 El miembro predeterminado de un atributo se utiliza para evaluar expresiones cuando un atributo no está incluido en una consulta. El miembro predeterminado de un atributo se especifica mediante la propiedad **DefaultMember** del atributo. Siempre que se incluya una jerarquía de una dimensión en una consulta, se omiten todos los miembros predeterminados de los atributos correspondientes a los niveles de la jerarquía. Si no se incluye ninguna jerarquía de una dimensión en una consulta, se usan los miembros predeterminados para todos los atributos de la dimensión.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>Resolver el miembro predeterminado cuando no se especifica ningún miembro predeterminado  
 Si no se especifica ningún miembro predeterminado para una jerarquía de atributo y la jerarquía de atributo es agregable (la propiedad **IsAggregatable** del atributo está establecida como **True**), el miembro (All) es el miembro predeterminado. Si no se especifica ningún miembro predeterminado y la jerarquía de atributo no es agregable, (la propiedad **IsAggregatable** del atributo está establecida como **False**), se selecciona un miembro predeterminado del nivel superior de la jerarquía de atributo.  
  
## <a name="specifying-the-default-member"></a>Especificar el miembro predeterminado  
 Todos los atributos de una dimensión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tienen un miembro predeterminado, que se puede especificar mediante la propiedad **DefaultMember** de un atributo. Esta configuración se utiliza para evaluar expresiones si no se incluye un atributo en una consulta. Si una consulta especifica una jerarquía en una dimensión, se omiten los miembros predeterminados de los atributos de la jerarquía. Si una consulta no especifica una jerarquía en una dimensión, tendrá efecto la configuración **DefaultMember** de los atributos de la dimensión.  
  
 Si la configuración **DefaultMember** de un atributo está vacía y su propiedad **IsAggregatable** se establece en **True**, el miembro predeterminado es el miembro All. Si la propiedad **IsAggregatable** se establece en **False**, el miembro predeterminado es el primer miembro del primer nivel visible.  
  
 La configuración **DefaultMember** de un atributo se aplica en todas las jerarquías en las que interviene el atributo. No puede utilizar configuraciones diferentes para jerarquías distintas de una dimensión. Por ejemplo, si el miembro [1998] es el miembro predeterminado para el atributo [Year], esta configuración se aplica en todas las jerarquías de la dimensión. En este caso, la configuración **DefaultMember** no puede ser [1998] en una jerarquía y [1997] en otra.  
  
 Si se define un miembro predeterminado en un nivel específico de una jerarquía que no se agrega de forma natural, deberán definirse los miembros predeterminados de todos los niveles superiores a dicho nivel de la jerarquía. Por ejemplo, en la jerarquía All-Countries–Climate, no puede definirse un miembro predeterminado para Climate a menos que defina un miembro predeterminado para Countries. En caso contrario se producirían errores en tiempo de consulta.  
  
 Si los niveles de una jerarquía se agregan de forma natural, podrá definirse un miembro predeterminado para los atributos de la jerarquía con independencia de los demás atributos de la jerarquía. Por ejemplo, en la jerarquía Country–Province–City, puede definirse un miembro predeterminado para City, como [City].[Montreal] sin definir el miembro predeterminado para Province o Country.  
  
## <a name="see-also"></a>Vea también  
 [Configurar el nivel &#40;All&#41; para las jerarquías de atributo](../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  

