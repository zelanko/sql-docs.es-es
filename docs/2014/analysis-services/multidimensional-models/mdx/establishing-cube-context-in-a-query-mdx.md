---
title: Establecer el contexto de cubo en una consulta (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], MDX
- MDX [Analysis Services], cube context
- SELECT statement [MDX]
- Multidimensional Expressions [Analysis Services], cube context
- queries [MDX], cube context
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9f0f960c531fac8bae8f03479bacd507ffc3078
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074598"
---
# <a name="establishing-cube-context-in-a-query-mdx"></a>Establecer el contexto de cubo en una consulta (MDX)
  Las consultas de MDX se ejecutan en un contexto de cubo especificado. En este contexto se definen los miembros que se evalúan mediante las expresiones contenidas en la consulta.  
  
 En la instrucción SELECT, la cláusula FROM determina el contexto de cubo. Este contexto puede ser todo el cubo o simplemente un subcubo de ese cubo. Al especificar el contexto de cubo mediante la cláusula FROM, puede utilizar funciones adicionales para expandir o restringir ese contexto.  
  
> [!NOTE]  
>  Las instrucciones SCOPE y CALCULATE también le permiten gestionar el contexto de cubo desde un script de MDX. Para más información, vea [Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md).  
  
## <a name="from-clause-syntax"></a>Sintaxis de la cláusula FROM  
 La siguiente sintaxis describe la cláusula FROM:  
  
```  
<SELECT subcube clause> ::=  
   Cube_Identifier |   
   (SELECT [  
      * |   
      ( <SELECT query axis clause> [ , <SELECT query axis clause> ... ] ) ]   
   FROM <SELECT subcube clause> <SELECT slicer axis clause> )  
```  
  
 En esta sintaxis, observe que es la cláusula `<SELECT subcube clause>` la que describe el cubo o el subcubo en el que se ejecuta la instrucción SELECT.  
  
 Un sencillo ejemplo de una cláusula FROM sería una que se ejecutase contra la totalidad del cubo de ejemplo Adventure Works. Esa cláusula FROM tendría el formato siguiente:  
  
```  
FROM [Adventure Works]  
```  
  
 Para más información sobre la cláusula FROM de la instrucción MDX SELECT, vea [SELECT &#40;Instrucción, MDX&#41;](/sql/mdx/mdx-data-manipulation-select).  
  
## <a name="refining-the-context"></a>Refinar el contexto  
 Aunque la cláusula FROM especifica el contexto de cubo para un solo cubo, esto no debe limitarle a la hora de trabajar con datos de más de un cubo de forma simultánea.  
  
 Puede utilizar la función de MDX [LookupCube](/sql/mdx/lookupcube-mdx) para recuperar datos de cubos que se encuentren fuera del contexto de cubo. Además, funciones como [Filter](/sql/mdx/filter-mdx) están disponibles para permitir la restricción temporal del contexto mientras se evalúa la consulta.  
  
## <a name="see-also"></a>Consulte también  
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
