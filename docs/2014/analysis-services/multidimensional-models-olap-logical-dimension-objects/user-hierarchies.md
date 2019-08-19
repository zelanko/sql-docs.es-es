---
title: Jerarquías de usuario | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- members [Analysis Services], hierarchies
- dimensions [Analysis Services], hierarchies
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], multilevel
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], hierarchies
- parent-child hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
- ragged hierarchies [Analysis Services]
- balanced hierarchies [Analysis Services]
- hierarchies [Analysis Services]
- OLAP objects [Analysis Services], hierarchies
- multilevel hierarchies [Analysis Services]
- unbalanced hierarchies [Analysis Services]
ms.assetid: 9394e9a3-2242-4f0e-85e0-25d499d2d3b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1192deaa556dd8546d0d9fbf17d5ff79335173a
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887828"
---
# <a name="user-hierarchies"></a>Jerarquías de usuario
  Las jerarquías definidas por el usuario son jerarquías definidas por el usuario de atributos que [!INCLUDE[msCoName](../../includes/msconame-md.md)] se utilizan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para organizar los miembros de una dimensión en estructuras jerárquicas y proporcionar rutas de navegación en un cubo. Por ejemplo, en la tabla siguiente se define una tabla de dimensiones para una dimensión de tiempo. La tabla de dimensiones admite tres atributos denominados Year, Quarter y Month.  
  
|Year|Trimestre|Mes|  
|----------|-------------|-----------|  
|1999|Trimestre 1|Jan|  
|1999|Trimestre 1|Feb|  
|1999|Trimestre 1|Mar|  
|1999|Trimestre 2|Apr|  
|1999|Trimestre 2|May|  
|1999|Trimestre 2|Jun|  
|1999|Trimestre 3|Jul|  
|1999|Trimestre 3|Aug|  
|1999|Trimestre 3|Sep|  
|1999|Quarter 4|Oct|  
|1999|Quarter 4|Nov|  
|1999|Quarter 4|Dec|  
  
 Los atributos Year, Quarter y Month se utilizan para construir una jerarquía definida por el usuario llamada Calendar en la dimensión de tiempo. La relación entre los niveles y los miembros de la dimensión Calendar (una dimensión regular) se muestra en el siguiente diagrama.  
  
 ![Jerarquía de nivel y miembro de una dimensión de tiempo](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/as-levelconcepts.gif "Jerarquía de nivel y miembro de una dimensión de tiempo")  
  
> [!NOTE]  
>  Cualquier jerarquía que no sea la jerarquía de atributos de dos niveles predeterminada se denomina jerarquía definida por el usuario. Para obtener más información sobre las jerarquías de atributo, vea [atributos y jerarquías](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)de atributos.  
  
## <a name="member-structures"></a>Estructuras de miembros  
 A excepción de las jerarquías de elementos primarios y secundarios, las posiciones de los miembros de la jerarquía se controlan mediante el orden de los atributos en la definición de la jerarquía. Cada atributo de la definición de la jerarquía constituye un nivel en la jerarquía. La posición de un miembro en un nivel está determinada por la ordenación del atributo utilizado para crear el nivel. Las estructuras de miembros de las jerarquías definidas por el usuario pueden adoptar una de cuatro formas básicas, dependiendo de cómo se relacionen entre sí los miembros.  
  
### <a name="balanced-hierarchies"></a>Jerarquías equilibradas  
 En una jerarquía equilibrada, todas las ramas descienden hasta el mismo nivel y el elemento primario lógico de cada miembro se encuentra en el nivel inmediatamente superior al del miembro. La jerarquía Product Categories de la dimensión Product de la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es un buen ejemplo de jerarquía equilibrada. Cada miembro del nivel Product Name tiene un miembro primario en el nivel Subcategory, que a su vez tiene un miembro primario en el nivel Category. Además, todas las ramas de la jerarquía tienen un miembro hoja en el nivel Product Name.  
  
### <a name="unbalanced-hierarchies"></a>Jerarquías desequilibradas  
 En una jerarquía desequilibrada, las ramas descienden hasta niveles diferentes. Las jerarquías de elementos primarios y secundarios son jerarquías desequilibradas. Por ejemplo, la dimensión Organization de la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contiene un miembro para cada empleado. El CEO es el miembro superior de la jerarquía, y los jefes de departamento y las secretarias de dirección se encuentran inmediatamente por debajo de él. Los jefes de departamento tienen miembros subordinados, pero las secretarias de dirección no.  
  
 Puede que a los usuarios finales les resulte muy difícil distinguir entre las jerarquías desequilibradas y las irregulares. No obstante, puede utilizar diversas técnicas y propiedades en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para admitir estos dos tipos de jerarquías. Para obtener más información, vea [Jerarquías desiguales](../multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md) y [Atributos en jerarquías de elementos primarios y secundarios](../multidimensional-models/parent-child-dimension-attributes.md).  
  
### <a name="ragged-hierarchies"></a>Jerarquías desiguales  
 En una jerarquía desigual, el miembro primario lógico de al menos un miembro no se encuentra en el nivel que está inmediatamente por encima del miembro. Esto puede hacer que las ramas de la jerarquía desciendan hasta niveles diferentes. Por ejemplo, en una dimensión Geography definida con los niveles Continent, CountryRegion y City, por este orden, el miembro Europe aparece en el nivel superior de la jerarquía, el miembro France aparece en el nivel medio y el miembro Paris aparece en el nivel inferior. France es más específico que Europe y Paris es más específico que France. En esta jerarquía regular, se realizan los siguientes cambios:  
  
-   El miembro Vatican City se agrega al nivel CountryRegion.  
  
-   Se agregan miembros en el nivel City que se asocian al miembro Vatican City en el nivel CountryRegion.  
  
-   Se agrega un nivel llamado Province entre los niveles CountryRegion y City.  
  
 El nivel Province se rellena con miembros asociados a otros miembros en el nivel CountryRegion y los miembros del nivel City se asocian a sus miembros correspondientes en el nivel Province. Sin embargo, puesto que el miembro Vatican City del nivel CountryRegion no tiene miembros asociados en el nivel Province, los miembros se deben asociar desde el nivel City directamente al miembro Vatican City en el nivel CountryRegion. Debido a los cambios, la jerarquía de la dimensión es ahora irregular. El elemento primario de la ciudad Vatican City es el país o región Vatican City, que no se encuentra en el nivel inmediatamente superior al miembro Vatican City del nivel City. Para más información, vea [Jerarquías desiguales](../multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
### <a name="parent-child-hierarchies"></a>Jerarquías de elementos primarios y secundarios  
 Las jerarquías de elementos primarios y secundarios para dimensiones se definen mediante un atributo especial, llamado atributo primario, para determinar cómo se relacionan entre sí los miembros. Un atributo primario describe una *relación que hace referencia a sí misma*o una *autocombinación*dentro de una tabla principal de dimensiones. Las jerarquías de elementos primarios y secundarios se construyen a partir de un único atributo primario. A una jerarquía de elementos primarios y secundarios solo se le asigna un nivel, puesto que los niveles presentes en la jerarquía se extraen de las relaciones de elementos primarios y secundarios entre los miembros asociados al atributo primario. El esquema de dimensiones de una jerarquía de elementos primarios y secundarios depende de la relación que hace referencia a sí misma presente en la tabla principal de dimensiones. Por ejemplo, en el diagrama siguiente se muestra la tabla principal de dimensión de biomorgan [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] en la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos de ejemplo.  
  
 ![Combinación con referencia automática en la tabla de Biomorgan](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/dimorganization.gif "Combinación con referencia automática en la tabla de Biomorgan")  
  
 En esta tabla de dimensiones, la columna **ParentOrganizationKey** tiene una relación de clave externa con la columna de clave principal **OrganizationKey** . En otras palabras, cada registro de esta tabla puede relacionarse a través de una relación de elementos primarios y secundarios con otro registro de la tabla. Este tipo de autocombinación se utiliza generalmente para representar los datos de entidad de la organización, como la estructura de administración de los empleados de un departamento.  
  
 Cuando se crea una jerarquía de elementos primarios y secundarios, las columnas representadas por ambos atributos deben tener el mismo tipo de datos. Además, los dos atributos deben estar en la misma tabla. De forma predeterminada, se considera que cualquier miembro cuya clave principal sea igual a su propia clave de miembro, valor NULL, 0 (cero) o un valor no presente en la columna de las claves de miembro es un miembro del nivel superior (excepto el nivel (All)).  
  
 La profundidad de una jerarquía de elementos primarios y secundarios puede variar entre sus ramas jerárquicas. En otras palabras, una jerarquía de elementos primarios y secundarios se considera una jerarquía desequilibrada.  
  
 A diferencia de las jerarquías definidas por el usuario, en las que el número de niveles de la jerarquía determina el número de niveles que se mostrarán a los usuarios finales, una jerarquía de elementos primarios y secundarios se define con el único nivel de una jerarquía de atributo, y los valores de este único nivel generan los diversos niveles que ven los usuarios finales. El número de niveles mostrados depende del contenido de las columnas de la tabla de dimensiones, que almacenan las claves de miembro y las claves principales. El número de niveles puede variar cuando cambian los datos de las tablas de dimensiones. Para obtener más información, vea jerarquía de elementos primarios y [secundarios](../multidimensional-models/parent-child-dimension.md)y [atributos en jerarquías](../multidimensional-models/parent-child-dimension-attributes.md)de elementos primarios y secundarios.  
  
## <a name="see-also"></a>Vea también  
 [Crear jerarquías definidas por el usuario](../multidimensional-models/user-defined-hierarchies-create.md)   
 [Propiedades de jerarquía de usuario](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Referencia de las propiedades de los atributos de dimensión](../multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
