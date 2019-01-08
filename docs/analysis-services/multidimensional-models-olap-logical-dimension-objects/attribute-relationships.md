---
title: Relaciones de atributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9eddac84f4db92770daa2bbf32b51597f84eb3f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542763"
---
# <a name="attribute-relationships"></a>Relaciones de atributo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], atributos dentro de una dimensión siempre se relacionan con directa o indirectamente con el atributo clave. Al definir una dimensión basada en un esquema en estrella, donde todos los atributos de la dimensión se derivan de la misma tabla relacional, se define automáticamente una relación de atributo entre el atributo clave y cada atributo no clave de la dimensión. Al definir una dimensión basada en un esquema de copo de nieve, donde los atributos de la dimensión se derivan de varias tablas relacionadas, se define automáticamente una relación de atributo del modo siguiente:  
  
-   Entre el atributo clave y cada atributo sin clave enlazado a columnas de la tabla principal de dimensiones.  
  
-   Entre el atributo clave y el atributo enlazado a la clave externa de la tabla secundaria que vincula las tablas de dimensiones subyacentes.  
  
-   Entre el atributo enlazado a la clave externa de la tabla secundaria y cada atributo no clave enlazado a las columnas de la tabla secundaria.  
  
 Sin embargo, hay una serie de razones por las que puede que desee cambiar estas relaciones de atributo predeterminadas. Por ejemplo quizás desee definir una jerarquía natural, un orden personalizado o una granularidad de dimensión basados en un atributo no clave. Para obtener más información, consulte [Dimension Attribute Properties Reference](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md).  
  
> [!NOTE]  
>  Las relaciones de atributo se conocen como propiedades de miembros en las Expresiones multidimensionales (MDX).  
  
## <a name="natural-hierarchy-relationships"></a>Relaciones de jerarquías naturales  
 Una jerarquía es natural cuando cada atributo incluido en la jerarquía definida por el usuario tiene una relación de uno a varios con el atributo situado inmediatamente debajo. Por ejemplo imagine una dimensión de cliente basada en una tabla de origen relacional con ocho columnas:  
  
-   CustomerKey  
  
-   CustomerName  
  
-   Age  
  
-   Sexo  
  
-   Email  
  
-   City  
  
-   País  
  
-   Region  
  
 La dimensión correspondiente de Analysis Services tiene siete atributos:  
  
-   Customer (basado en CustomerKey; CustomerName proporciona los nombres de miembro)  
  
-   Age, Gender, Email, City, Region, Country  
  
 Las relaciones que representan jerarquías naturales se aplican al crear una relación de atributo entre el atributo de un nivel y el atributo del nivel situado debajo. Para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], esto especifica una relación natural y una agregación potencial. En la dimensión de cliente, existe una jerarquía natural para los atributos Country, Region, City y Customer. La jerarquía natural de `{Country, Region, City, Customer}` se describe al agregar las siguientes relaciones de atributo:  
  
-   El atributo Country como una relación de atributo con el atributo Region.  
  
-   El atributo Region como una relación de atributo con el atributo City.  
  
-   El atributo City como una relación de atributo con el atributo Customer.  
  
 Para navegar por los datos del cubo, también puede crear una jerarquía definida por el usuario que no representa una jerarquía natural en los datos (que se denomina un *ad hoc* o *reporting* jerarquía). Por ejemplo, podría crear una jerarquía definida por el usuario basada en `{Age, Gender}`. Los usuarios no ven ninguna diferencia en cómo se comportan las dos jerarquías, aunque la jerarquía natural se beneficia de agregación e indizado estructuras - ocultas al usuario - esa cuenta para las relaciones naturales de los datos de origen.  
  
 El **SourceAttribute** propiedad de un nivel determina qué atributo se utiliza para describir el nivel. El **KeyColumns** propiedad del atributo especifica la columna de la vista del origen de datos que proporciona los miembros. El **NameColumn** propiedad del atributo puede especificar una columna de nombre diferente para los miembros.  
  
 Para definir un nivel en una jerarquía definida por el usuario mediante [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], **Diseñador de dimensiones** le permite seleccionar un atributo de dimensión, una columna en una tabla de dimensiones o una columna de una tabla relacionada incluidos en la vista del origen de datos para el cubo. Para obtener más información acerca de cómo crear jerarquías definidas por el usuario, consulte [jerarquías definidas por el usuario](../../analysis-services/multidimensional-models/user-defined-hierarchies-create.md).  
  
 En Analysis Services, se suele hacer una suposición acerca del contenido de los miembros. Los miembros hoja no tienen descendientes y contienen datos derivados de los orígenes de datos subyacentes. Los miembros no hoja tienen descendientes y contienen datos derivados de agregaciones realizadas en miembros secundarios. En los niveles agregados, los miembros se basan en agregaciones de niveles subordinados. Por lo tanto, cuando el **IsAggregatable** propiedad está establecida en **False** en un atributo de origen para un nivel, no deben agregarse los atributos agregables como niveles por encima de él.  
  
## <a name="defining-an-attribute-relationship"></a>Definir una relación de atributo  
 La principal restricción al crear una relación de atributo consiste en asegurarse de que el atributo al que la relación de atributo hace referencia no tenga más de un valor para ningún miembro en el atributo al que pertenece la relación de atributo. Por ejemplo, si se define una relación entre un atributo City y uno State, cada ciudad solo puede relacionarse con un único estado.  
  
## <a name="attribute-relationship-queries"></a>Consultas de las relaciones de atributo  
 Puede usar las consultas MDX para recuperar datos de las relaciones de atributo, en forma de propiedades de miembro, con el **propiedades** palabra clave de MDX **seleccione** instrucción. Para obtener más información acerca de cómo utilizar MDX para recuperar las propiedades de miembro, vea [mediante propiedades de miembro &#40;MDX&#41;](../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md).  
  
## <a name="see-also"></a>Vea también  
 [Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Referencia de las propiedades de los atributos de dimensión](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)   
 [Jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies.md)   
 [Propiedades de jerarquía de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
