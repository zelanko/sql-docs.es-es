---
title: Instrucción CREATE SESSION CUBE (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_SESSION_CUBE
- SESSION
- CUBE
- SESSION CUBE
- CREATE SESSION CUBE
- CREATE SESSION
- CREATE
dev_langs:
- kbMDX
helpviewer_keywords:
- CREATE SESSION CUBE
- statements [MDX], CREATE SESSION CUBE
ms.assetid: 06b90f44-d943-4a52-b0d8-4bcbc57ed6ec
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 5f49f41f4a346d7a30bdfd8d95e1df5c0f2c0eb1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---create-session-cube"></a>Definición de datos MDX - crear el cubo de sesión
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea y llena un cubo de sesión a partir de un cubo de servidor existente. El cubo de sesión solamente es visible en la sesión actual; no puede examinarse ni consultarse desde otras sesiones. El cubo de sesión se elimina implícitamente al cerrar la sesión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE SESSION CUBE session_cube_name FROM <cube list> (<param list>)  
  
<cube list>::= source_cube_name [,<cube list>]  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= <reg dim from clause>   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN  
  
```  
  
## <a name="syntax-elements"></a>Elementos de la sintaxis  
 session_cube_name  
 Nombre del cubo de sesión.  
  
 source_cube_name  
 Nombre del cubo en el que se basa el cubo de sesión.  
  
 source_cube_name.measure_name  
 Nombre completo de la medida de origen que se incluye en el cubo de sesión. No se permiten los miembros calculados de la dimensión Measures.  
  
 measure_name  
 Nombre de la medida del cubo de sesión.  
  
 source_cube_name.dimension_name  
 Nombre completo de la dimensión de origen que se incluye en el cubo de sesión.  
  
 dimension_name  
 Nombre de la dimensión del cubo de sesión.  
  
 DESDE \<dim cláusula from >  
 Especificación válida únicamente para la definición de la dimensión derivada.  
  
 NOT_RELATED_TO_FACTS  
 Especificación válida únicamente para la definición de la dimensión derivada.  
  
 \<tipo de nivel >  
 Especificación válida únicamente para la definición de la dimensión derivada.  
  
## <a name="remarks"></a>Comentarios  
 A diferencia de los cubos de servidor y locales, un cubo de sesión no se mantiene más allá de la sesión que lo creó. Un cubo de sesión se define según las medidas y definiciones que lo definen. Existen dos tipos de dimensiones.  
  
-   Dimensiones de origen: se trata de las dimensiones que formaban parte de uno de varios cubos de origen.  
  
-   Dimensiones derivadas: se trata de las dimensiones que proporcionan nuevas capacidades de análisis. Una dimensión derivada puede ser una dimensión normal definida en función de una dimensión de origen segmentada vertical u horizontalmente, o que contiene una agrupación personalizada de miembros de dimensión. Una dimensión derivada también puede ser una dimensión de minería de datos basada en un modelo de minería de datos.  
  
> [!NOTE]  
>  La palabra clave Dimension puede hacer referencia a dimensiones o a jerarquías.  
  
 Los cubos de sesión se usan principalmente para la agrupación dinámica de miembros de atributos en grupos de miembros personalizados por parte de aplicaciones cliente, como Microsoft Excel. En un cubo de sesión, pueden realizarse las siguientes tareas:  
  
-   Eliminar las dimensiones presentes en el cubo de origen  
  
-   Agregar o eliminar jerarquías de una dimensión.  
  
-   Eliminar grupos de medida o medidas específicas  
  
-   Agregar un nuevo atributo, basándose en el enlace de atributo, a fin de crear grupos con un atributo existente...  
  
> [!IMPORTANT]  
>  La seguridad de los objetos de cubo de sesión se hereda de los objetos de origen subyacentes. El cubo de sesión también hereda otros objetos, como acciones y scripts de cálculo.  
  
 La instrucción CREATE SESSION CUBE sigue estas reglas:  
  
-   No es posible realizar agrupaciones en jerarquías de elementos primarios y secundarios.  
  
-   No es posible realizar agrupaciones en dimensiones ROLAP.  
  
-   No es posible realizar agrupaciones en dimensiones vinculadas.  
  
-   No es posible realizar agrupaciones en niveles con resúmenes personalizados.  
  
-   No es posible realizar agrupaciones en jerarquías de atributos de datos discretos.  
  
-   No es posible realizar agrupaciones en jerarquías no naturales, que son jerarquías con relaciones de varios a varios entre los distintos niveles (como edad y sexo).  
  
-   Las referencias explícitas a un nombre de cubo en un script MDX quedan anuladas por la agrupación porque el cubo de sesión tiene un nombre distinto. Utilice en su lugar la palabra clave CURRENTCUBE.  
  
-   No es posible realizar agrupaciones en dimensiones con miembros explícitos predeterminados.  
  
-   Al realizar una agrupación, se pierden los miembros calculados que pertenecen al ámbito de sesión del cubo de servidor original.  
  
-   Al realizar una agrupación en la dimensión de un cubo en un cubo de servidor, la agrupación afecta a todas las dimensiones del cubo basadas en la misma dimensión.  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo muestra cómo crear una versión de ámbito de sesión del cubo de Adventure Works que contiene la medida Reseller Sales Amount, la dimensión Reseller, la dimensión Product, la dimensión Geography y la dimensión Date. Dentro de este cubo de sesión, se crean dos grupos; uno de ellos contiene los países de Europa y el otro contiene grupos de Norteamérica. Este ejemplo es una versión simplificada de una instrucción CREATE SESSION CUBE emitida por Microsoft Excel cuando un usuario crea una agrupación personalizada de miembros.  
  
```  
CREATE SESSION CUBE [Adventure Works_XL_GROUPING1]   
   FROM [Adventure Works]   
   ( MEASURE [Adventure Works].[Internet Sales Amount]  
   ,MEASURE [Adventure Works].[Reseller Sales Amount]  
   ,DIMENSION [Adventure Works].[Date].[Calendar]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Year]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Semester]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Quarter]  
   ,DIMENSION [Adventure Works].[Date].[Month Name]  
   ,DIMENSION [Adventure Works].[Date].[Date]  
   ,DIMENSION [Adventure Works].[Geography].[Country]   
      HIDDEN AS _XL_GROUPING81  
   ,DIMENSION [Adventure Works].[Geography].[State-Province]  
   ,DIMENSION [Adventure Works].[Geography].[City]  
   ,DIMENSION [Adventure Works].[Geography].[Postal Code]  
   ,DIMENSION [Adventure Works].[Geography].[Geography]  
   ,DIMENSION [Adventure Works].[Product].[Product Categories]  
   ,DIMENSION [Adventure Works].[Product].[Category]  
   ,DIMENSION [Adventure Works].[Product].[Subcategory]  
   ,DIMENSION [Adventure Works].[Product].[Product]  
   ,DIMENSION [Adventure Works].[Product].[Product Key]  
   ,DIMENSION [Adventure Works].[Reseller].[Reseller]  
   ,DIMENSION [Adventure Works].[Reseller].[Geography Key]  
   ,DIMENSION [Geography].[Country]   
      NOT_RELATED_TO_FACTS FROM _XL_GROUPING81   
          ( LEVEL [(All)]  
         ,LEVEL [Country1] GROUPING  
         ,LEVEL [Country]  
            ,GROUP [Country1].[CountryXl_Grp_1]   
                ( MEMBER [Geography].[Country].&[Canada]  
                  ,MEMBER [Geography].[Country].&[United States] )  
            ,GROUP [Country1].[CountryXl_Grp_2]   
                ( MEMBER [Geography].[Country].&[France]  
                  ,MEMBER [Geography].[Country].&[Germany]  
                  ,MEMBER [Geography].[Country].&[United Kingdom] )   
            )   
   )  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [Instrucción CREATE GLOBAL CUBE &#40;MDX&#41;](../mdx/mdx-data-definition-create-global-cube.md)  
  
  
