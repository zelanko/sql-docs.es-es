---
title: Definir un miembro predeterminado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 959645223eacec6c000ddbfa23615b7949d10d5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077419"
---
# <a name="define-a-default-member"></a>Definir un miembro predeterminado
  El miembro predeterminado de una jerarquía de atributo se usa para evaluar expresiones cuando una jerarquía de atributo no se incluye en una consulta. El miembro predeterminado se omite cuando una consulta incluye una jerarquía de atributo o una jerarquía de usuario que contiene el atributo que da origen a la jerarquía de atributo. Esto se debe a que se utiliza el miembro especificado en la consulta.  
  
 El miembro predeterminado de una jerarquía de atributo se establece especificando un miembro de atributo como el valor de propiedad `DefaultMember` para la jerarquía de atributo. Puede establecer esta propiedad en la pestaña Estructura de dimensión en el Diseñador de dimensiones, o bien en el script de cálculo del cubo en la pestaña Cálculo en el Diseñador de cubos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. También puede especificar la propiedad `DefaultMember` para un rol de seguridad (reemplazando el miembro predeterminado establecido en la dimensión) en la pestaña Datos de dimensiones al definir la seguridad de dimensión. Para evitar problemas de resolución de nombres, defina el miembro predeterminado en el script MDX del cubo en las siguientes situaciones: si el cubo hace referencia a una dimensión de base de datos más de una vez, si la dimensión en el cubo tiene un nombre distinto al de la dimensión en la base de datos, o bien si desea tener miembros predeterminados diferentes en distintos cubos.  
  
 El miembro predeterminado de un atributo se utiliza para evaluar expresiones cuando un atributo no está incluido en una consulta. El miembro predeterminado de un atributo se especifica mediante la propiedad `DefaultMember` del atributo. Siempre que se incluya una jerarquía de una dimensión en una consulta, se omiten todos los miembros predeterminados de los atributos correspondientes a los niveles de la jerarquía. Si no se incluye ninguna jerarquía de una dimensión en una consulta, se usan los miembros predeterminados para todos los atributos de la dimensión.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>Resolver el miembro predeterminado cuando no se especifica ningún miembro predeterminado  
 Si no se especifica ningún miembro predeterminado para una jerarquía de atributo, y la jerarquía de atributo es agregable (la propiedad `IsAggregatable` del atributo está establecida como `True`), el miembro (All) es el miembro predeterminado. Si no se especifica ningún miembro predeterminado y la jerarquía de atributo no es agregable, (la propiedad `IsAggregatable` del atributo está establecida como `False`), se selecciona un miembro predeterminado del nivel superior de la jerarquía de atributo.  
  
## <a name="specifying-the-default-member"></a>Especificar el miembro predeterminado  
 Todos los atributos de una dimensión [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de tienen un miembro predeterminado, que se puede especificar mediante la `DefaultMember` propiedad de un atributo. Esta configuración se utiliza para evaluar expresiones si no se incluye un atributo en una consulta. Si una consulta especifica una jerarquía en una dimensión, se omiten los miembros predeterminados de los atributos de la jerarquía. Si una consulta no especifica una jerarquía en una dimensión, la configuración `DefaultMember` de los atributos de la dimensión surte efecto.  
  
 Si el `DefaultMember` valor de un atributo está en blanco y `IsAggregatable` su propiedad está establecida `True`en, el miembro predeterminado es el miembro ALL. Si la `IsAggregatable` propiedad se establece en `False`, el miembro predeterminado es el primer miembro del primer nivel visible.  
  
 La `DefaultMember` configuración de un atributo se aplica a todas las jerarquías en las que participa el atributo. No puede utilizar configuraciones diferentes para jerarquías distintas de una dimensión. Por ejemplo, si el miembro [1998] es el miembro predeterminado para el atributo [Year], esta configuración se aplica en todas las jerarquías de la dimensión. En `DefaultMember` este caso, la configuración no puede ser [1998] en una jerarquía y [1997] en una jerarquía diferente.  
  
 Si se define un miembro predeterminado en un nivel específico de una jerarquía que no se agrega de forma natural, deberán definirse los miembros predeterminados de todos los niveles superiores a dicho nivel de la jerarquía. Por ejemplo, en la jerarquía All-countries-clima, no se puede definir un miembro predeterminado para clima a menos que defina un miembro predeterminado para países. En caso contrario se producirían errores en tiempo de consulta.  
  
 Si los niveles de una jerarquía se agregan de forma natural, podrá definirse un miembro predeterminado para los atributos de la jerarquía con independencia de los demás atributos de la jerarquía. Por ejemplo, en la jerarquía Country-provincia-City, puede definir un miembro predeterminado para City, como [City]. [Montreal] sin definir el miembro predeterminado para el estado o para el país.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar el nivel de&#41; &#40;para las jerarquías de atributo](database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
