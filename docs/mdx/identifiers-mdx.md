---
title: Identificadores (MDX) | Documentos de Microsoft
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
dev_langs:
- kbMDX
helpviewer_keywords:
- formats [Analysis Services]
- Multidimensional Expressions [Analysis Services], identifiers
- identifiers [MDX]
- MDX [Analysis Services], identifiers
- delimited identifiers [MDX]
- regular identifiers [MDX]
- formats [Analysis Services], identifiers
ms.assetid: 739a8a67-bef3-4b56-961d-ee96cfc36b5b
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: a04d387c0ee40d825fddf3c50f02793e722cdbc8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="identifiers-mdx"></a>Identificadores (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Un identificador es el nombre de un [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] objeto. Cada objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede y debe tener un identificador. Esto incluye cubos, dimensiones, jerarquías, niveles, miembros, etc. El identificador de un objeto se utiliza para hacer referencia al objeto en instrucciones de expresiones multidimensionales (MDX).  
  
 En función del nombre del objeto, el identificador del objeto será bien un identificador normal o delimitado.  
  
> [!NOTE]  
>  Identificadores, normales y delimitados deben contener entre 1 y 100 caracteres.  
  
## <a name="using-regular-identifiers"></a>Usar identificadores normales  
 Un identificador normal es un nombre de objeto que cumple las siguientes reglas de formato para identificadores normales. Los identificadores normales pueden usarse con o sin delimitadores.  
  
### <a name="formatting-rules-for-regular-identifiers"></a>Reglas de formato para los identificadores normales  
  
1.  El primer carácter debe ser alguno de los siguientes:  
  
    -   Una letra, tal como se define por el estándar Unicode 2.0. Además de letras de otros idiomas, la definición Unicode de letras incluye caracteres latinos de la "a" a la "z" y de la "A" a la "Z".  
  
    -   El carácter de subrayado (_).  
  
2.  Los caracteres subsiguientes pueden ser:  
  
    -   Letras, tal como se define en el estándar Unicode 2.0.  
  
    -   Números decimales del alfabeto Latín básico u otros alfabetos de otros idiomas.  
  
    -   El carácter de subrayado (_).  
  
3.  El identificador no debe ser una palabra clave reservada de DMX. Las palabras clave reservadas de DMX no distinguen entre mayúsculas y minúsculas. Para obtener más información, consulte [palabras clave reservadas &#40;sintaxis MDX&#41;](../mdx/reserved-keywords-mdx-syntax.md).  
  
4.  No se permiten los caracteres especiales o los espacios incrustados.  
  
### <a name="examples-of-regular-identifiers"></a>Ejemplos de identificadores normales  
 En la siguiente instrucción MDX, los identificadores `Measures`, `Product` y `Style` cumplen las reglas de formato de los identificadores normales. Dichos identificadores normales no precisan delimitadores.  
  
 `SELECT Measures.MEMBERS ON COLUMNS,`  
  
 `Product.Style.CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
 Aunque no son necesarios, también se pueden usar delimitadores con los identificadores normales. En la siguiente instrucción MDX, los identificadores normales `Measures`, `Product` y `Style` se han delimitado correctamente mediante corchetes.  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Product].[Style].CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
## <a name="using-delimited-identifiers"></a>Usar identificadores delimitados  
 Si un identificador no sigue las reglas de formato de los identificadores normales, debe aparecer siempre delimitado mediante corchetes ([]).  
  
> [!NOTE]  
>  Los delimitadores solo pueden utilizarse para los identificadores. No es posible utilizar delimitadores para palabras clave, estén o no marcadas como reservadas en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Los identificadores delimitados se emplean en las siguientes situaciones:  
  
-   Cuando el nombre de un objeto o parte del nombre incluye palabras reservadas.  
  
     Se recomienda no utilizar palabras clave reservadas como nombres de objeto. Las bases de datos actualizadas desde versiones anteriores de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] podrían contener identificadores que incluyan palabras que no estaban reservadas en la versión anterior, pero son palabras reservadas para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Hasta que pueda cambiar el identificador del objeto, puede hacer referencia al objeto mediante un identificador delimitado.  
  
-   Cuando el nombre de un objeto contiene caracteres no incluidos en la lista de identificadores calificados.  
  
     [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] permite que los identificadores delimitados utilicen cualquier carácter de la página de códigos actual. No obstante, el uso indiscriminado de caracteres especiales en los nombres de objeto puede hacer que las instrucciones y scripts MDX resulten difíciles de leer y de mantener.  
  
### <a name="formatting-rules-for-delimited-identifiers"></a>Reglas de formato para los identificadores delimitados  
 La parte de cuerpo de un identificador delimitado puede contener cualquier combinación de caracteres de la página de códigos actual, incluidos los propios caracteres delimitadores. Si el cuerpo del identificador delimitado contiene caracteres delimitadores, será necesario un tratamiento especial:  
  
-   Si el cuerpo del identificador solamente contiene un corchete de apertura ([), no se requiere ninguna manipulación.  
  
-   Si el cuerpo del identificador contiene un corchete de cierre (]), deberá especificar dos corchetes de cierre (]]).  
  
### <a name="examples-of-delimited-identifiers"></a>Ejemplos de identificadores delimitados  
 En la siguiente instrucción MDX hipotética, `Sales Volume`, `Sales Cube` y `select` son identificadores delimitados:  
  
 `-- The [Sales Volume] and [Sales Cube] identifiers contain a space.`  
  
 `SELECT Measures.[Sales Volume]`  
  
 `FROM [Sales Cube]`  
  
 `WHERE Product.[select]`  
  
 `-- The [select] identifier is a reserved keyword.`  
  
 En el siguiente ejemplo, el nombre del objeto es `Total Profit [Domestic]`. Para hacer referencia al mismo es necesario utilizar el siguiente identificador delimitado:  
  
 `[Total Profit [Domestic]]]`  
  
 Observe que no ha sido necesario cambiar el corchete de apertura situado justo delante de `Domestic` para crear el identificador delimitado. Sin embargo, el corchete de cierre situado detrás de `Domestic` sí ha tenido que ser reemplazado por dos corchetes de cierre.  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>Delimitar identificadores con varias partes  
 Cuando se utilizan nombres de objetos completos, podría ser necesario delimitar varios de los identificadores que componen el nombre del objeto. Por ejemplo, es necesario delimitar el identificador Front Brakes que aparece en el siguiente código.  
  
 SELECT [Measures].MEMBERS ON COLUMNS,  
  
 [Product].[Product].[Front Brakes] ON ROWS  
  
 FROM [Adventure Works]  
  
 También se ha delimitado el identificador Measures del ejemplo anterior para mostrar la delimitación de más de un identificador.  
  
## <a name="see-also"></a>Vea también  
 [Referencia del lenguaje MDX & #40; MDX & #41;](../mdx/mdx-language-reference-mdx.md)   
 [Aspectos básicos de consulta MDX & #40; Analysis Services & #41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Elementos de sintaxis MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  
