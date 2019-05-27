---
title: Jerarquía de elementos primarios y secundarios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Analysis Services], parent-child
- dimensions [Analysis Services], parent-child
- parent attributes [Analysis Services]
- data members [Analysis Services]
- hierarchies [Analysis Services], multilevel
- self-joins
- self-referencing relationships
- members [Analysis Services], data
- parent-child dimensions [Analysis Services]
ms.assetid: 4657f5dc-d88e-48d2-a448-08f79bc89546
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d0eac17d30d8a8870d03a0b5b81610fad1344333
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66073385"
---
# <a name="parent-child-hierarchy"></a>Jerarquía de elementos primarios y secundarios
  Una jerarquía de elementos primarios y secundarios es una jerarquía de una dimensión estándar que contiene un atributo primario. Un atributo primario describe una *relación que hace referencia a sí misma*o una *autocombinación*dentro de una tabla principal de dimensiones. Las jerarquías de elementos primarios y secundarios se construyen a partir de un único atributo primario. A una jerarquía de elementos primarios y secundarios solo se le asigna un nivel, puesto que los niveles presentes en la jerarquía se extraen de las relaciones de elementos primarios y secundarios entre los miembros asociados al atributo primario. La posición de un miembro en una jerarquía de elementos primarios y secundarios viene determinada por las propiedades `KeyColumns` y `RootMemberIf` del atributo primario, mientras que la posición de un miembro en un nivel viene determinada por la propiedad `OrderBy` del atributo primario. Para obtener más información sobre las propiedades de atributo, vea [Atributos y jerarquías de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
 Debido a las relaciones de elementos primarios y secundarios entre los niveles de una jerarquía de elementos primarios y secundarios, algunos miembros no hoja también pueden tener datos derivados de orígenes de datos subyacentes, además de los datos agregados de miembros secundarios.  
  
## <a name="dimension-schema"></a>Esquema de dimensiones  
 El esquema de dimensiones de una jerarquía de elementos primarios y secundarios depende de la relación que hace referencia a sí misma presente en la tabla principal de dimensiones. Por ejemplo, en el siguiente diagrama se muestra la tabla principal de dimensiones **DimOrganization** de la base de datos de ejemplo [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] .  
  
 ![Referencia a sí misma combinación en la tabla DimOrganization](../dev-guide/media/dimorganization.gif "autorreferencia combinación en la tabla DimOrganization")  
  
 En esta tabla de dimensiones, la columna **ParentOrganizationKey** tiene una relación de clave externa con la columna de clave principal **OrganizationKey** . En otras palabras, cada registro de esta tabla puede relacionarse a través de una relación de elementos primarios y secundarios con otro registro de la tabla. Este tipo de autocombinación se utiliza generalmente para representar los datos de entidad de la organización, como la estructura de administración de los empleados de un departamento.  
  
## <a name="hierarchies-and-levels"></a>Jerarquías y niveles  
 Las dimensiones que no tienen una relación de elementos primarios y secundarios crean jerarquías agrupando y ordenando los atributos. Estas dimensiones derivan los nombres de los niveles de sus jerarquías a partir de los nombres de atributo.  
  
 Sin embargo, las dimensiones de elementos primarios y secundarios crean jerarquías de elementos primarios y secundarios al examinar los datos que contiene la tabla principal de dimensiones y, a continuación, evaluar las relaciones de elementos primarios y secundarios entre los registros de la tabla. Para obtener más información sobre las jerarquías de elementos primarios y secundarios, vea [Jerarquías de usuario](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md).  
  
 Las jerarquías de elementos primarios y secundarios no derivan los nombres de los niveles de los atributos utilizados para crear la jerarquía. En su lugar, estas dimensiones crean nombres de nivel automáticamente mediante una expresión de cadena de una plantilla de nomenclatura puede especificar en el nivel del atributo primario que controla cómo genera el atributo de la jerarquía de atributo. Para obtener más información sobre cómo establecer la plantilla de asignación de nombres para un atributo primario, vea [Atributos y jerarquías de atributos](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="data-members"></a>Miembros de datos  
 Normalmente, los miembros hoja de una dimensión contienen datos derivados directamente de los orígenes de datos subyacentes; mientras que los miembros no hoja contienen datos derivados de agregaciones realizadas en miembros secundarios.  
  
 No obstante, las jerarquías de elementos primarios y secundarios podrían tener algunos miembros no hoja cuyos datos se deriven de orígenes de datos subyacentes, además de los datos agregados de miembros secundarios. Para estos miembros no hoja de una jerarquía de elementos primarios y secundarios, se pueden crear miembros secundarios especiales generados por el sistema que contienen los datos de la tabla de hechos subyacente. Denominados *miembros de datos*, estos miembros secundarios especiales contienen un valor asociado directamente a un miembro no hoja independiente del valor de resumen calculado a partir de los descendientes del miembro no hoja. Para obtener más información sobre los miembros de datos, vea [Atributos en las jerarquías de elementos primarios y secundarios](parent-child-dimension-attributes.md).  
  
## <a name="see-also"></a>Vea también  
 [Atributos en las jerarquías de elementos primarios y secundarios](parent-child-dimension-attributes.md)   
 [Propiedades de la dimensión de base de datos](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)  
  
  
