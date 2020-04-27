---
title: Relaciones de atributo | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- member properties [Analysis Services], attribute relationships
- security [Analysis Services], properties
- PROPERTIES keyword
- storage [Analysis Services], attribute relationships
- natural hierarchies [Analysis Services]
- dimensions [Analysis Services], member properties
- queries [MDX], attribute relationships
- user-defined hierarchies [Analysis Services]
- attributes [Analysis Services], relationships
- member properties [Analysis Services]
- members [Analysis Services], attribute relationships
- storing data [Analysis Services], attribute relationships
- relationships [Analysis Services], attributes
ms.assetid: 2491422a-4cf5-4b23-b6ab-289222b22ce8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81d51c8778cfbc6e3891dfb3b6783db48f0c65a2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62728521"
---
# <a name="attribute-relationships"></a>Relaciones de atributo
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], los atributos de una dimensión siempre están relacionados directa o indirectamente con el atributo clave. Al definir una dimensión basada en un esquema en estrella, donde todos los atributos de la dimensión se derivan de la misma tabla relacional, se define automáticamente una relación de atributo entre el atributo clave y cada atributo no clave de la dimensión. Al definir una dimensión basada en un esquema de copo de nieve, donde los atributos de la dimensión se derivan de varias tablas relacionadas, se define automáticamente una relación de atributo del modo siguiente:  
  
-   Entre el atributo clave y cada atributo sin clave enlazado a columnas de la tabla principal de dimensiones.  
  
-   Entre el atributo clave y el atributo enlazado a la clave externa de la tabla secundaria que vincula las tablas de dimensiones subyacentes.  
  
-   Entre el atributo enlazado a la clave externa de la tabla secundaria y cada atributo no clave enlazado a las columnas de la tabla secundaria.  
  
 Sin embargo, hay una serie de razones por las que puede que desee cambiar estas relaciones de atributo predeterminadas. Por ejemplo quizás desee definir una jerarquía natural, un orden personalizado o una granularidad de dimensión basados en un atributo no clave. Para obtener más información, vea [referencia de propiedades de atributo de dimensión](../multidimensional-models/dimension-attribute-properties-reference.md).  
  
> [!NOTE]  
>  Las relaciones de atributo se conocen como propiedades de miembros en las Expresiones multidimensionales (MDX).  
  
## <a name="natural-hierarchy-relationships"></a>Relaciones de jerarquías naturales  
 Una jerarquía es natural cuando cada atributo incluido en la jerarquía definida por el usuario tiene una relación de uno a varios con el atributo situado inmediatamente debajo. Por ejemplo imagine una dimensión de cliente basada en una tabla de origen relacional con ocho columnas:  
  
-   CustomerKey  
  
-   CustomerName  
  
-   Age  
  
-   Sexo  
  
-   Correo electrónico  
  
-   City  
  
-   Country  
  
-   Region  
  
 La dimensión correspondiente de Analysis Services tiene siete atributos:  
  
-   Customer (basado en CustomerKey; CustomerName proporciona los nombres de miembro)  
  
-   Age, Gender, Email, City, Region, Country  
  
 Las relaciones que representan jerarquías naturales se aplican al crear una relación de atributo entre el atributo de un nivel y el atributo del nivel situado debajo. Para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], esto especifica una relación natural y una agregación potencial. En la dimensión de cliente, existe una jerarquía natural para los atributos Country, Region, City y Customer. La jerarquía natural de `{Country, Region, City, Customer}` se describe al agregar las siguientes relaciones de atributo:  
  
-   El atributo Country como una relación de atributo con el atributo Region.  
  
-   El atributo Region como una relación de atributo con el atributo City.  
  
-   El atributo City como una relación de atributo con el atributo Customer.  
  
 Para navegar por los datos del cubo, también puede crear una jerarquía definida por el usuario que no represente una jerarquía natural en los datos (que se denomina una jerarquía *ad hoc* o de *informes* ). Por ejemplo, podría crear una jerarquía definida por el usuario basada en `{Age, Gender}`. Los usuarios no ven ninguna diferencia en la forma en que se comportan las dos jerarquías, aunque la jerarquía natural se beneficia de las estructuras de agregación e indización (ocultas para el usuario) para las relaciones naturales en los datos de origen.  
  
 La propiedad `SourceAttribute` de un nivel determina qué atributo se utiliza para describir el nivel. La propiedad `KeyColumns` del atributo especifica la columna de la vista del origen de datos que proporciona los miembros. La propiedad `NameColumn` del atributo puede especificar una columna de nombre diferente para los miembros.  
  
 Para definir un nivel en una jerarquía definida por el usuario [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]mediante, el **Diseñador de dimensiones** permite seleccionar un atributo de dimensión, una columna de una tabla de dimensiones o una columna de una tabla relacionada incluida en la vista del origen de datos para el cubo. Para obtener más información sobre la creación de jerarquías definidas por el usuario, vea [Crear jerarquías definidas por el usuario](../multidimensional-models/user-defined-hierarchies-create.md).  
  
 En Analysis Services, se suele hacer una suposición acerca del contenido de los miembros. Los miembros hoja no tienen descendientes y contienen datos derivados de los orígenes de datos subyacentes. Los miembros no hoja tienen descendientes y contienen datos derivados de agregaciones realizadas en miembros secundarios. En los niveles agregados, los miembros se basan en agregaciones de niveles subordinados. Por lo tanto, cuando la propiedad `IsAggregatable` está establecida en `False` en un atributo de origen de un nivel, no se deben agregar atributos agregables como niveles por encima de él.  
  
## <a name="defining-an-attribute-relationship"></a>Definir una relación de atributo  
 La principal restricción al crear una relación de atributo consiste en asegurarse de que el atributo al que la relación de atributo hace referencia no tenga más de un valor para ningún miembro en el atributo al que pertenece la relación de atributo. Por ejemplo, si se define una relación entre un atributo City y uno State, cada ciudad solo puede relacionarse con un único estado.  
  
## <a name="attribute-relationship-queries"></a>Consultas de las relaciones de atributo  
 Puede usar las consultas MDX para recuperar datos de las relaciones de atributo, en formato de propiedades de miembro, por medio de la palabra clave `PROPERTIES` de la instrucción `SELECT` de MDX. Para obtener más información sobre cómo usar MDX para recuperar propiedades de miembro, vea [usar las propiedades de miembro &#40;&#41;MDX ](../multidimensional-models/mdx/mdx-member-properties.md).  
  
## <a name="see-also"></a>Consulte también  
 [Atributos y jerarquías de atributos](attributes-and-attribute-hierarchies.md)   
 [Referencia de propiedades de atributo de dimensión](../multidimensional-models/dimension-attribute-properties-reference.md)   
 [Jerarquías de usuario](user-hierarchies.md)   
 [Propiedades de jerarquía de usuario](user-hierarchies-properties.md)  
  
  
