---
title: Uso de expresiones de cubo y subcubo | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f13d92c114783646bbeab9451c3d212ff01b8f8c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63125431"
---
# <a name="using-cube-and-subcube-expressions"></a>Usar expresiones de cubo y de subcubo


  Las expresiones de cubo y subcubo se utilizan en las instrucciones de expresiones multidimensionales (MDX) para definir, manipular o recuperar los datos de un cubo o subcubo.  
  
## <a name="cube-expressions"></a>Expresiones de cubo  
 Las expresiones de cubo contienen un identificador de cubo o la palabra clave CURRENTCUBE y, por lo tanto, solo pueden ser expresiones simples. Muchas instrucciones MDX usan la palabra clave CURRENTCUBE para identificar el contexto del cubo actual, en lugar de requerir un identificador de cubo.  
  
 Aparece un identificador de cubo como *Cube_Name* en las descripciones de notación de BNF de las instrucciones MDX.  
  
 Las expresiones de cubo pueden aparecer en varios lugares. En una instrucción MDX SELECT, especifican el cubo del que van a recuperarse los datos. En la consulta de ejemplo siguiente, la expresión [Adventure Works] hace referencia al cubo de ese nombre:  
  
 `SELECT [Measures].[Internet Sales Amount] ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 En la instrucción CREATE MEMBER, la expresión de cubo especifica en qué cubo va a aparecer el miembro calculado que se está creando. En el ejemplo siguiente, la instrucción crea una medida calculada en la dimensión Measures del cubo Adventure Works:  
  
 `CREATE MEMBER [Adventure Works].[Measures].[Test] AS 1`  
  
 Cuando la instrucción CREATE MEMBER se utiliza dentro de un script MDX, el nombre del cubo puede reemplazarse por la palabra clave CURRENTCUBE, puesto que el cubo donde va a crearse el miembro calculado debe ser el mismo cubo al que pertenece el script MDX, tal y como se muestra en el siguiente ejemplo:  
  
 `CREATE MEMBER CURRENTCUBE.[Measures].[Test] AS 1;`  
  
 Hacer esto lo facilita la operación de copiar y pegar las definiciones de los miembros calculados de un cubo a otro, puesto que el nombre del cubo ya no está codificado de forma rígida.  
  
## <a name="subcube-expressions"></a>Expresiones de subcubo  
 Una expresión de subcubo puede contener un identificador de subcubo o una instrucción MDX que devuelve un subcubo. Si la expresión de subcubo contiene un identificador de subcubo, será una expresión simple. Si contiene una instrucción MDX que devuelve un subcubo, será una instrucción compleja. Por ejemplo, la instrucción MDX SELECT devuelve un subcubo y puede usarse cuando no se permiten las expresiones de subcubo, tal y como se muestra en el siguiente ejemplo:  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Date].[Calendar Year].MEMBERS ON ROWS`  
  
 `FROM`  
  
 `(SELECT [Measures].[Internet Sales Amount] ON COLUMNS,`  
  
 `[Date].[Calendar Year].&[2004] ON ROWS`  
  
 `FROM [Adventure Works])`  
  
 Este uso de una instrucción SELECT en la cláusula FROM también recibe el nombre de subselección.  
  
 Otro escenario común donde podemos encontrar expresiones de subcubo es cuando se realizan asignaciones con ámbito en un script MDX. En el ejemplo siguiente, la instrucción SCOPE se utiliza para limitar una asignación a un subcubo que está compuesto de [Measures].[Internet Sales Amount]:  
  
 `SCOPE([Measures].[Internet Sales Amount]);`  
  
 `This=1;`  
  
 `END SCOPE;`  
  
 Un identificador de subcubo aparece como *Subcube_Name*. en las descripciones de la notación de BNF para las instrucciones MDX.  
  
## <a name="see-also"></a>Vea también  
 [Consulta de MDX básica &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)   
 [Generar subcubos en MDX &#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx.md)   
 [Instrucción CREATE SUBCUBE &#40;MDX&#41;](../mdx/mdx-data-definition-create-subcube.md)   
 [Expressions &#40;MDX&#41;](../mdx/expressions-mdx.md)   
 [SCOPE &#40;Instrucción, MDX&#41;](../mdx/mdx-scripting-scope.md)  
  
  
