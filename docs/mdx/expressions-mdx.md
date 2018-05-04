---
title: Expresiones (MDX) | Documentos de Microsoft
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
dev_langs:
- kbMDX
helpviewer_keywords:
- identifiers [MDX]
- expressions [MDX]
- expressions [MDX], about expressions
- MDX [Analysis Services], expressions
- Multidimensional Expressions [Analysis Services], expressions
ms.assetid: e20c34bc-30fa-4ac5-b896-9d4c9925ef59
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a158bbcdd77e4a7e1e026db793b46e306d8c6fbe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="expressions-mdx"></a>Expresiones (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Una expresión es una combinación de identificadores, valores y operadores que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede evaluar para obtener un resultado. Los datos se pueden usar en varios sitios distintos cuando se cambian o se tiene acceso a ellos. Por ejemplo, las expresiones se pueden usar como parte de los datos que se van a recuperar (mediante una consulta) o como una condición de búsqueda de los datos que cumplan un conjunto de criterios.  
  
## <a name="simple-and-complex-expressions"></a>Expresiones simples y complejas  
 En MDX, las expresiones pueden ser simples o complejas:  
  
 Una expresión simple puede ser una de las siguientes:  
  
 Constante  
 Una constante es un símbolo que representa un único valor específico en MDX. Los valores de cadena, numéricos y de fecha pueden representarse como constantes. A diferencia de las constantes numéricas, las constantes de cadena y de fecha deben delimitarse con caracteres de comillas simples (').  
  
 Función escalar  
 Una función escalar devuelve un solo valor en el contexto de evaluación de MDX. Esta diferencia es importante para comprender cómo resuelve MDX las funciones escalares, puesto que la mayoría de las expresiones, instrucciones y scripts MDX se evalúan no respecto a un solo elemento de datos, sino de forma iterativa respecto a un grupo de elementos de datos como celdas o miembros. Sin embargo, cuando se evalúa la función escalar, la función suele revisar un solo elemento de datos.  
  
 Identificador de objeto  
 MDX está orientado a objetos por la naturaleza de los datos multidimensionales. Los identificadores de objetos se consideran expresiones simples en MDX. Para obtener más información acerca de los identificadores, vea [identificadores &#40;MDX&#41;](../mdx/identifiers-mdx.md).  
  
 Las expresiones complejas también pueden generarse a partir de la combinación de estas entidades mediante operadores.  
  
## <a name="expression-results"></a>Resultados de la expresión  
 Para una expresión simple creada con una constante, variable, función escalar o nombre de columna, el tipo de datos, intercalación, precisión, escala y valor de la expresión es el tipo de datos, intercalación, precisión, escala y valor del elemento de referencia. Dado que MDX solo es compatible directamente con el tipo de datos OLE VARIANT, no deberían producirse coerciones al utilizar expresiones simples.  
  
 En el caso de las expresiones complejas, pueden producirse coerciones si se utilizan dos o más expresiones simples con tipos de datos distintos.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 La consulta siguiente muestra ejemplos de medidas calculadas cuyas definiciones son expresiones simples:  
  
 `WITH`  
  
 `MEMBER MEASURES.CONSTANTVALUE AS 1`  
  
 `MEMBER MEASURES.SCALARFUNCTION AS [Date].[Calendar Year].CURRENTMEMBER.NAME`  
  
 `MEMBER MEASURES.OBJECTIDENTIFIER AS [Measures].[Internet Sales Amount]`  
  
 `SELECT {MEASURES.CONSTANTVALUE,MEASURES.SCALARFUNCTION,MEASURES.OBJECTIDENTIFIER } ON 0,`  
  
 `[Date].[Calendar Year].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 Una expresión también puede ser un cálculo, como `[Measures].[Discount Amount] * 1.5`. En el siguiente ejemplo se ilustra el empleo de un cálculo para definir un miembro en una instrucción MDX SELECT:  
  
```  
WITH   
   MEMBER [Measures].[Special Discount] AS  
   [Measures].[Discount Amount] * 1.5  
SELECT   
   [Measures].[Special Discount] on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Uso de expresiones de cubo y de subcubo](../mdx/using-cube-and-subcube-expressions.md)|Define expresiones de cubo y subcubo.|  
|[Uso de expresiones de dimensiones](../mdx/using-dimension-expressions.md)|Define expresiones de dimensión.|  
|[Uso de expresiones de miembro](../mdx/using-member-expressions.md)|Define expresiones de miembro.|  
|[Uso de expresiones de tupla](../mdx/using-tuple-expressions.md)|Define expresiones de tupla.|  
|[Uso de expresiones de conjunto](../mdx/using-set-expressions.md)|Define expresiones de conjunto.|  
|[Uso de expresiones escalares](../mdx/using-scalar-expressions.md)|Define expresiones escalares.|  
|[Trabajar con valores vacíos](../mdx/working-with-empty-values.md)|Describe un valor vacío y cómo se administran estos valores.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia del lenguaje MDX & #40; MDX & #41;](../mdx/mdx-language-reference-mdx.md)   
 [Aspectos básicos de consulta MDX & #40; Analysis Services & #41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
