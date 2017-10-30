---
title: Usar funciones de cadena | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- string functions
ms.assetid: 962e820a-a1f9-49b5-90f0-a05261e6682b
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 12fc2dca6c7a0eb1c7d126ef0cfdc87df869c878
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="using-string-functions"></a>Usar funciones de cadena
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Las funciones de cadena se pueden usar en casi todos los objetos de las expresiones multidimensionales (MDX). En los procedimientos almacenados, las funciones de cadena se usan principalmente para convertir el objeto en una representación de cadena. También sirven para evaluar una expresión de cadena con relación a un objeto para devolver un valor.  
  
 Las funciones de cadena más comúnmente usadas son **nombre** y **Uniquename**. Estas funciones devuelven el nombre y el nombre único de un objeto, respectivamente. Se utilizan principalmente al depurar cálculos para detectar qué miembro devuelve una función.  
  
## <a name="examples"></a>Ejemplos  
 Las consultas de ejemplo siguientes muestran el modo de usar estas funciones:  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 El **generar** función puede utilizarse para ejecutar una función de cadena en cada miembro de un conjunto y concatenar los resultados. Esto también puede resultar útil a la hora de depurar cálculos, puesto que permite visualizar el contenido de un conjunto. En el ejemplo siguiente se muestra cómo utilizar la función de esta forma:  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 Otro grupo de funciones de cadena que se utilizan mucho son las funciones que permiten convertir una cadena que contiene el nombre único de un objeto o una expresión que se resuelve en el objeto en el objeto propiamente dicho. La consulta de ejemplo siguiente se muestra cómo el **StrToMember** y **StrToSet** funciones hacer esto:  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  El **StrToMember** y **StrToSet** funciones deben usarse con precaución. Pueden dar lugar a un bajo rendimiento de las consultas si se utilizan dentro de definiciones de cálculo.  
  
## <a name="see-also"></a>Vea también  
 [Generar &#40; MDX &#41;](../mdx/generate-mdx.md)   
 [Nombre de &#40; MDX &#41;](../mdx/name-mdx.md)   
 [UniqueName &#40; MDX &#41;](../mdx/uniquename-mdx.md)   
 [Funciones &#40; La sintaxis de MDX &#41;](../mdx/functions-mdx-syntax.md)   
 [Mediante los procedimientos almacenados &#40; MDX &#41;](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40; MDX &#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40; MDX &#41;](../mdx/strtoset-mdx.md)  
  
  

