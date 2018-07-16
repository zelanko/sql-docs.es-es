---
title: Definir un miembro predeterminado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6899b40cd317db9d74a426038e7f0201223d9993
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37263691"
---
# <a name="define-a-default-member"></a>Definir un miembro predeterminado
  El miembro predeterminado de una jerarquía de atributo se usa para evaluar expresiones cuando una jerarquía de atributo no se incluye en una consulta. El miembro predeterminado se omite cuando una consulta incluye una jerarquía de atributo o una jerarquía de usuario que contiene el atributo que da origen a la jerarquía de atributo. Esto se debe a que se utiliza el miembro especificado en la consulta.  
  
 El miembro predeterminado de una jerarquía de atributo se establece mediante la especificación de un miembro de atributo como el `DefaultMember` valor de propiedad para la jerarquía de atributo. Puede establecer esta propiedad en la pestaña Estructura de dimensión en el Diseñador de dimensiones, o bien en el script de cálculo del cubo en la pestaña Cálculo en el Diseñador de cubos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. También puede especificar la propiedad `DefaultMember` para un rol de seguridad (reemplazando el miembro predeterminado establecido en la dimensión) en la pestaña Datos de dimensiones al definir la seguridad de dimensión. Para evitar problemas de resolución de nombres, defina el miembro predeterminado en el script MDX del cubo en las siguientes situaciones: si el cubo hace referencia a una dimensión de base de datos más de una vez, si la dimensión en el cubo tiene un nombre distinto al de la dimensión en la base de datos, o bien si desea tener miembros predeterminados diferentes en distintos cubos.  
  
 El miembro predeterminado de un atributo se utiliza para evaluar expresiones cuando un atributo no está incluido en una consulta. El miembro predeterminado para un atributo especificado por el `DefaultMember` propiedad del atributo. Siempre que se incluya una jerarquía de una dimensión en una consulta, se omiten todos los miembros predeterminados de los atributos correspondientes a los niveles de la jerarquía. Si no se incluye ninguna jerarquía de una dimensión en una consulta, se usan los miembros predeterminados para todos los atributos de la dimensión.  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>Resolver el miembro predeterminado cuando no se especifica ningún miembro predeterminado  
 Si no se especifica ningún miembro predeterminado para una jerarquía de atributo y la jerarquía de atributo es agregable (la `IsAggregatable` propiedad en el atributo se establece en `True`), el miembro (All) es el miembro predeterminado. Si no se especifica ningún miembro predeterminado y la jerarquía de atributo no es agregable (la `IsAggregatable` propiedad en el atributo se establece en `False`), se selecciona un miembro predeterminado de nivel superior de la jerarquía de atributo.  
  
## <a name="specifying-the-default-member"></a>Especificar el miembro predeterminado  
 Todos los atributos de una dimensión en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tiene un miembro predeterminado, que se puede especificar mediante el uso de la `DefaultMember` propiedad para un atributo. Esta configuración se utiliza para evaluar expresiones si no se incluye un atributo en una consulta. Si una consulta especifica una jerarquía en una dimensión, se omiten los miembros predeterminados de los atributos de la jerarquía. Si una consulta no especifica una jerarquía en una dimensión, el `DefaultMember` aplicará la configuración para los atributos de dimensión.  
  
 Si el `DefaultMember` configuración de un atributo está vacío y su `IsAggregatable` propiedad está establecida en `True`, el miembro predeterminado es el miembro All. Si el `IsAggregatable` propiedad está establecida en `False`, el miembro predeterminado es el primer miembro del primer nivel visible.  
  
 El `DefaultMember` configuración para un atributo se aplica a todas las jerarquías en las que interviene el atributo. No puede utilizar configuraciones diferentes para jerarquías distintas de una dimensión. Por ejemplo, si el miembro [1998] es el miembro predeterminado para el atributo [Year], esta configuración se aplica en todas las jerarquías de la dimensión. El `DefaultMember` configuración en este caso no puede ser [1998] en una jerarquía y [1997] en una jerarquía distinta.  
  
 Si se define un miembro predeterminado en un nivel específico de una jerarquía que no se agrega de forma natural, deberán definirse los miembros predeterminados de todos los niveles superiores a dicho nivel de la jerarquía. Por ejemplo, en la jerarquía All-Countries–Climate, no puede definirse un miembro predeterminado para Climate a menos que defina un miembro predeterminado para Countries. En caso contrario se producirían errores en tiempo de consulta.  
  
 Si los niveles de una jerarquía se agregan de forma natural, podrá definirse un miembro predeterminado para los atributos de la jerarquía con independencia de los demás atributos de la jerarquía. Por ejemplo, en la jerarquía Country–Province–City, puede definirse un miembro predeterminado para City, como [City].[Montreal] sin definir el miembro predeterminado para Province o Country.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la &#40;todas&#41; nivel para las jerarquías de atributo](database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
