---
title: "Establecer el contexto de cubo en una consulta (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "cubos [Analysis Services], MDX"
  - "MDX [Analysis Services], contexto de cubo"
  - "SELECT, instrucción [MDX]"
  - "Expresiones multidimensionales [Analysis Services], contexto de cubo"
  - "consultas [MDX], contexto de cubo"
ms.assetid: 79d6a1e8-2825-4eb9-97df-5071aecae8f0
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# Establecer el contexto de cubo en una consulta (MDX)
  Las consultas de MDX se ejecutan en un contexto de cubo especificado. En este contexto se definen los miembros que se evalúan mediante las expresiones contenidas en la consulta.  
  
 En la instrucción SELECT, la cláusula FROM determina el contexto de cubo. Este contexto puede ser todo el cubo o simplemente un subcubo de ese cubo. Al especificar el contexto de cubo mediante la cláusula FROM, puede utilizar funciones adicionales para expandir o restringir ese contexto.  
  
> [!NOTE]  
>  Las instrucciones SCOPE y CALCULATE también le permiten gestionar el contexto de cubo desde un script de MDX. Para más información, vea [Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md).  
  
## Sintaxis de la cláusula FROM  
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
  
 Para más información sobre la cláusula FROM de la instrucción MDX SELECT, vea [SELECT &#40;Instrucción, MDX&#41;](../Topic/SELECT%20Statement%20\(MDX\).md).  
  
## Refinar el contexto  
 Aunque la cláusula FROM especifica el contexto de cubo para un solo cubo, esto no debe limitarle a la hora de trabajar con datos de más de un cubo de forma simultánea.  
  
 Puede utilizar la función de MDX [LookupCube](../../../mdx/lookupcube-mdx.md) para recuperar datos de cubos que se encuentren fuera del contexto de cubo. Además, funciones como [Filter](../../../mdx/filter-mdx.md) están disponibles para permitir la restricción temporal del contexto mientras se evalúa la consulta.  
  
## Vea también  
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  