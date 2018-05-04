---
title: Instrucción CREATE GLOBAL CUBE (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GLOBAL CUBE
- CUBE
- GLOBAL
- CREATE
- CREATE GLOBAL
- CREATE GLOBAL CUBE
dev_langs:
- kbMDX
helpviewer_keywords:
- statements [MDX], CREATE GLOBAL CUBE
- CREATE GLOBAL CUBE
ms.assetid: b46f3c98-a4f1-4ebb-915f-a3333f4054dc
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a6ed1613fdb2d0b6f77cbbf0724bfdf74d5249cc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---create-global-cube"></a>Definición de datos MDX - Crear cubo GLOBAL
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Crea y rellena un cubo guardado de forma local basado en un subcubo de un cubo del servidor. No es necesaria una conexión al servidor para conectarse al cubo almacenado de forma local. Para obtener más información acerca de los cubos locales, consulte [cubos locales &#40;Analysis Services - datos multidimensionales&#41;](../analysis-services/multidimensional-models/olap-physical/local-cubes-analysis-services-multidimensional-data.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE GLOBAL CUBE local_cube_name STORAGE 'Cube_Location'   
FROM source_cube_name (<param list>)  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= < dim DM from clause> | <reg dim from clause>   
  
<dim DM from clause>::= dm_model_name> COLUMN column_name   
  
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
 local_cube_name  
 Nombre del cubo local.  
  
 'Cube_Location'  
 Nombre y ruta de acceso del cubo almacenado de forma local.  
  
 source_cube_name  
 Nombre del cubo en el que se basa el cubo local.  
  
 source_cube_name.measure_name  
 Nombre completo de la medida de origen que se incluye en el cubo local. No se permiten los miembros calculados de la dimensión Measures.  
  
 measure_name  
 Nombre de la medida del cubo local.  
  
 source_cube_name.dimension_name  
 Nombre completo de la dimensión de origen que se incluye en el cubo local.  
  
 dimension_name  
 Nombre de la dimensión del cubo local.  
  
 DESDE \<dim cláusula from >  
 Especificación válida únicamente para la definición de la dimensión derivada.  
  
 NOT_RELATED_TO_FACTS  
 Especificación válida únicamente para la definición de la dimensión derivada.  
  
 \<tipo de nivel >  
 Especificación válida únicamente para la definición de la dimensión derivada.  
  
## <a name="remarks"></a>Comentarios  
 Un cubo local es definedin términos de las medidas y las definiciones que lo definen. Existen dos tipos de dimensiones.  
  
-   Dimensiones de origen: se trata de dimensiones que formaban parte de uno de varios cubos de origen  
  
-   Dimensiones derivadas: se trata de las dimensiones que proporcionan nuevas capacidades de análisis. Una dimensión derivada puede ser una dimensión normal definida en función de una dimensión de origen segmentada vertical u horizontalmente, o que contiene una agrupación personalizada de miembros de dimensión. Una dimensión derivada también puede ser una dimensión de minería de datos basada en un modelo de minería de datos.  
  
> [!NOTE]  
>  La palabra clave Dimension puede hacer referencia a dimensiones o a jerarquías.  
  
 En un cubo local, pueden realizarse las siguientes tareas:  
  
-   Eliminar las dimensiones que existen en el cubo de origen  
  
-   Agregar o eliminar jerarquías en una dimensión  
  
-   Eliminar grupos de medida o medidas específicas  
  
 La instrucción CREATE GLOBAL CUBE sigue estas reglas:  
  
-   La instrucción CREATE GLOBAL CUBE copia automáticamente todos los comandos, como las medidas calculadas o acciones, al cubo local. Si un comando contiene una expresión MDX (Expresiones multidimensionales) que hace referencia explícita al cubo primario, el cubo local no podrá ejecutar el comando. Para evitar este problema, utilice la **CURRENTCUBE** palabra clave para definir expresiones de MDX para los comandos. El **CURRENTCUBE** palabra clave usa el contexto de cubo actual cuando se hace referencia a un cubo de una expresión MDX.  
  
-   No es posible guardar en el mismo archivo de cubo local un cubo global creado desde un cubo global existente en un archivo de cubo local. Por ejemplo, puede crear un cubo global con el nombre SalesLocal1 y guardarlo en el archivo C:\SalesLocal.cub. A continuación, puede conectarse al archivo C:\SalesLocal.cub y crear un segundo cubo global con el nombre SalesLocal2. Si intenta guardar el cubo global SalesLocal2 en el archivo C:\SalesLocal.cub, se mostrará un error. Sin embargo, puede guardar el cubo global SalesLocal2 en otro archivo de cubo local.  
  
-   Los cubos globales no admiten medidas de recuento distintivas. Dado que no es posible agregar los cubos que incluyen medidas de recuento distintivas, la instrucción CREATE GLOBAL CUBE no admite la creación o uso de medidas de recuento distintivas.  
  
-   Al agregar una medida a un cubo local, también debe incluirse, como mínimo, una dimensión relacionada con la medida agregada.  
  
-   Al agregar una jerarquía de elementos primarios y secundarios a un cubo local, se omiten los niveles y filtros de una jerarquía de elementos primarios y secundarios, y se incluye toda la jerarquía de elementos primarios y secundarios.  
  
-   En los cubos locales, no se admiten las propiedades de miembro.  
  
-   No se puede crear un cubo local desde una perspectiva.  
  
-   Al incluir una medida de suma parcial a un cubo local, se aplican las siguientes reglas:  
  
    -   Debe incluirse la dimensión Account si la propiedad AggregateFunction de la medida agregada es ByAccount.  
  
    -   Debe incluirse toda la dimensión Time si la propiedad AggregateFunction de la medida agregada es FirstChild, LastChild, FirstNonEmpty, LastNonEmpty o AverageOfChildren.  
  
-   No se pueden agregar dimensiones de minería de datos a un cubo local.  
  
-   Las dimensiones de referencia se materializan y se agregan como dimensiones normales.  
  
-   Al incluir una dimensión de varios a varios, se aplican las siguientes reglas:  
  
    -   Debe agregarse toda la dimensión varios a varios.  
  
    -   Debe agregarse el grupo de medida intermedio.  
  
    -   Debe agregarse la totalidad de las dimensiones comunes a los dos grupos de medida implicados en la relación de varios a varios.  
  
 El siguiente ejemplo muestra cómo crear una versión almacenada local del cubo de Adventure Works que solo contenga la medida Reseller Sales Amount, la dimensión Reseller y la dimensión Date.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller1.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
   )  
```  
  
 El siguiente ejemplo muestra cómo segmentar para crear un cubo local. El cubo global creado se basa en el cubo de Adventure Works segmentado verticalmente por el miembro 2005 del nivel Fiscal Year y horizontalmente por los niveles Fiscal Year y Month.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller2.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
      (  
LEVEL [Fiscal Year],  
LEVEL [Month],  
MEMBER [Date].[Fiscal].[Fiscal Year].&[2005]  
      )  
   )  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones de definición de datos MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)   
 [Instrucción CREATE SESSION CUBE &#40;MDX&#41;](../mdx/mdx-data-definition-create-session-cube.md)  
  
  
