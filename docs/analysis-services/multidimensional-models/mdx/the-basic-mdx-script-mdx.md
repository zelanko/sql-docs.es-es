---
title: "Script MDX b&#225;sico (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "scripts MDX predeterminados"
  - "instrucciones [MDX]"
  - "expresiones [MDX], secuencias de scripts"
  - "scripts [MDX], acerca de los scripts"
ms.assetid: 83d9afda-7d34-42b5-8f28-20172a905f23
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# Script MDX b&#225;sico (MDX)
  Un script MDX (Expresiones multidimensionales) define el proceso de cálculo de un cubo en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Hay dos tipos de scripts MDX:  
  
 **Script MDX predeterminado**  
 Al crear un cubo, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea un script MDX predeterminado para el cubo. Este script define un paso de cálculo para todo el cubo.  
  
 **Script MDX definido por el usuario**  
 Después de crear el cubo, se pueden agregar scripts MDX definidos por el usuario que amplían las capacidades de cálculo del cubo.  
  
## Script MDX predeterminado  
 El script MDX predeterminado que crea [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] al definir un cubo contiene una sola instrucción CALCULATE. Esta única instrucción CALCULATE se ubica al comienzo del script MDX predeterminado e indica que todo el cubo debe calcularse durante el primer paso de cálculo.  
  
 El script MDX predeterminado también incluye los comandos que crean conjuntos con nombre, asignaciones y miembros calculados creados en el Diseñador de cubos:  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] agrega directamente comandos de script al script MDX predeterminado.  
  
-   Para cada conjunto con nombre del cubo existe una instrucción CREATE SET correspondiente en el script MDX predeterminado.  
  
-   Para cada miembro calculado definido en el cubo existe una instrucción CREATE MEMBER correspondiente en el script MDX predeterminado.  
  
 Para controlar el orden de los comandos de script, conjuntos con nombre y miembros calculados del script MDX predeterminado puede utilizar la pestaña **Cálculos** del Diseñador de cubos. Para más información sobre cómo definir los cálculos almacenados en el script MDX predeterminado, vea [Cálculos en modelos multidimensionales](../../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md).  
  
 Si no se asocia ningún script MDX a un cubo, éste asume el script MDX predeterminado. Es necesario asociar los cubos a un script MDX como mínimo, ya que los cubos se basan en estos scripts para determinar el comportamiento del cálculo. Es decir, un cubo que no se haya asociado a ningún script MDX o que se haya asociado a un script MDX vacío no podría calcular ninguna celda. Si crea los cubos mediante programación, mediante comandos ASSL (Analysis Services Scripting Language) o mediante los Objetos de administración de análisis (AMO), se recomienda crear un script MDX predeterminad que contenga una única instrucción CALCULATE para el cubo.  
  
## Contenido del script MDX  
 Un script MDX puede incluir las siguientes instrucciones y expresiones:  
  
 Todas las instrucciones de scripting MDX  
 En los scripts MDX, las instrucciones de scripting MDX controlan el contexto y el ámbito de los cálculos y administran el comportamiento de otras instrucciones del script MDX. Esta categoría incluye las siguientes instrucciones:  
  
-   [CALCULATE](../Topic/CALCULATE%20Statement%20\(MDX\).md)  
  
-   [FREEZE](../Topic/FREEZE%20Statement%20\(MDX\).md)  
  
-   [SCOPE](../Topic/SCOPE%20Statement%20\(MDX\).md)  
  
 Para más información sobre las instrucciones para scripting de MDX, vea [Instrucciones para scripting de MDX &#40;MDX&#41;](../../../mdx/mdx-scripting-statements-mdx.md).  
  
 [CREATE MEMBER](../Topic/CREATE%20MEMBER%20Statement%20\(MDX\).md)  
 La instrucción CREATE MEMBER crea miembros calculados. Para más información sobre cómo crear miembros calculados, vea [Generar miembros calculados en MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-calculated-members-in-mdx-mdx.md).  
  
 [CREATE SET](../Topic/CREATE%20SET%20Statement%20\(MDX\).md)  
 La instrucción CREATE SET crea conjuntos con nombre. Para más información sobre cómo crear conjuntos con nombre, vea [Crear conjuntos con nombre en MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md).  
  
 Instrucciones condicionales  
 Las instrucciones condicionales agregan lógica condicional a los scripts MDX. En esta categoría se incluyen las instrucciones [CASE](../../../mdx/case-statement-mdx.md) e [IF](../Topic/IF%20Statement%20%20\(MDX\).md) .  
  
 Expresiones de asignación  
 Las expresiones de asignación asignan una expresión, como un valor, a los subcubos restringidos. Una expresión de subcubo restringido es una colección de expresiones de conjunto restringidas que definen los "bordes" de un subcubo de un script MDX. En los siguientes ejemplos de código se muestra la sintaxis de una expresión de subcubo restringido:  
  
```  
<Constrained subcube> ::= (   
    ( <Constrained set> [<Crossjoin operator> <Constrained set>...] |  
    <ROOT function> |  
    <TREE function> |  
    LEAVES() |  
    * ) [, <Constrained subcube>...]  
<Constrained set> ::=   
    <Natural hierarchy>.MEMBERS |   
    <Natural hierarchy>.LEVEL(<numeric expression>).MEMBERS |   
    { <Natural hierarchy member> } |   
    DESCENDANTS( <Natural hierarchy member>, <Level expression>, ( SELF | AFTER | SELF_AND_AFTER ) ) |   
    DESCENDANTS( <Natural hierarchy member>, , LEAVES )  
<Natural hierarchy> ::= <Hierarchy identifier>  
<Natural hierarchy member> ::= <Natural hierarchy>.<identifier>[.<identifier>...]  
```  
  
## Vea también  
 [Referencia del lenguaje MDX &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  