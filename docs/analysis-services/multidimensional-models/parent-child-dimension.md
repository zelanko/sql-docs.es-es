---
title: Dimensiones de elementos primarios y secundarios | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "42"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6835612c0b7ea9a6e42217366e8d745897300bfb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="parent-child-dimension"></a>Dimensión de elementos primarios y secundarios
  Una jerarquía de elementos primarios y secundarios es una jerarquía de una dimensión estándar que contiene un atributo primario. Un atributo primario describe una *relación que hace referencia a sí misma*o una *autocombinación*dentro de una tabla principal de dimensiones. Las jerarquías de elementos primarios y secundarios se construyen a partir de un único atributo primario. A una jerarquía de elementos primarios y secundarios solo se le asigna un nivel, puesto que los niveles presentes en la jerarquía se extraen de las relaciones de elementos primarios y secundarios entre los miembros asociados al atributo primario. La posición de un miembro en una jerarquía de elementos primarios y secundarios viene determinada por las propiedades **KeyColumns** y **RootMemberIf** del atributo primario, mientras que la posición de un miembro en un nivel viene determinada por la propiedad **OrderBy** del atributo primario. Para obtener más información sobre las propiedades de atributo, vea [Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
 Debido a las relaciones de elementos primarios y secundarios entre los niveles de una jerarquía de elementos primarios y secundarios, algunos miembros no hoja también pueden tener datos derivados de orígenes de datos subyacentes, además de los datos agregados de miembros secundarios.  
  
## <a name="dimension-schema"></a>Esquema de dimensiones  
 El esquema de dimensiones de una jerarquía de elementos primarios y secundarios depende de la relación que hace referencia a sí misma presente en la tabla principal de dimensiones. Por ejemplo, en el siguiente diagrama se muestra la tabla principal de dimensiones **DimOrganization** de la base de datos de ejemplo [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] .  
  
 ![Referencia a sí misma combinación en la tabla DimOrganization](../../analysis-services/multidimensional-models/media/dimorganization.gif "autorreferencia combinación en la tabla DimOrganization")  
  
 En esta tabla de dimensiones, la columna **ParentOrganizationKey** tiene una relación de clave externa con la columna de clave principal **OrganizationKey** . En otras palabras, cada registro de esta tabla puede relacionarse a través de una relación de elementos primarios y secundarios con otro registro de la tabla. Este tipo de autocombinación se utiliza generalmente para representar los datos de entidad de la organización, como la estructura de administración de los empleados de un departamento.  
  
## <a name="hierarchies-and-levels"></a>Jerarquías y niveles  
 Las dimensiones que no tienen una relación de elementos primarios y secundarios crean jerarquías agrupando y ordenando los atributos. Estas dimensiones derivan los nombres de los niveles de sus jerarquías a partir de los nombres de atributo.  
  
 Sin embargo, las dimensiones de elementos primarios y secundarios crean jerarquías de elementos primarios y secundarios al examinar los datos que contiene la tabla principal de dimensiones y, a continuación, evaluar las relaciones de elementos primarios y secundarios entre los registros de la tabla. Para obtener más información sobre las jerarquías de elementos primarios y secundarios, vea [Jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md).  
  
 Las jerarquías de elementos primarios y secundarios no derivan los nombres de los niveles de los atributos utilizados para crear la jerarquía. En cambio, estas dimensiones crean automáticamente nombres de nivel mediante una plantilla de asignación de nombres; es decir, una expresión de cadena que se puede especificar en el nivel del atributo primario que controla cómo genera el atributo la jerarquía de atributos. Para obtener más información sobre cómo establecer la plantilla de asignación de nombres para un atributo primario, vea [Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="data-members"></a>Miembros de datos  
 Normalmente, los miembros hoja de una dimensión contienen datos derivados directamente de los orígenes de datos subyacentes; mientras que los miembros no hoja contienen datos derivados de agregaciones realizadas en miembros secundarios.  
  
 No obstante, las jerarquías de elementos primarios y secundarios podrían tener algunos miembros no hoja cuyos datos se deriven de orígenes de datos subyacentes, además de los datos agregados de miembros secundarios. Para estos miembros no hoja de una jerarquía de elementos primarios y secundarios, se pueden crear miembros secundarios especiales generados por el sistema que contienen los datos de la tabla de hechos subyacente. Denominados *miembros de datos*, estos miembros secundarios especiales contienen un valor asociado directamente a un miembro no hoja independiente del valor de resumen calculado a partir de los descendientes del miembro no hoja. Para obtener más información sobre los miembros de datos, vea [Atributos en las jerarquías de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md).  
  
## <a name="see-also"></a>Vea también  
 [Atributos en las jerarquías de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension-attributes.md)   
 [Propiedades de la dimensión de base de datos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)  
  
  
