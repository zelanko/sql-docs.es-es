---
title: Script MDX básico (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- default MDX scripts
- statements [MDX]
- expressions [MDX], scripts
- scripts [MDX], about scripts
ms.assetid: 83d9afda-7d34-42b5-8f28-20172a905f23
author: minewiskan
ms.author: owend
ms.openlocfilehash: de0d2fea002beda0eca480bd27140bdd202fcb83
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546204"
---
# <a name="the-basic-mdx-script-mdx"></a>Script MDX básico (MDX)
  Un script de expresiones multidimensionales (MDX) define el proceso de cálculo de un cubo en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Hay dos tipos de scripts MDX:  
  
 **Script MDX predeterminado**  
 Al crear un cubo, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] crea un script MDX predeterminado para el cubo. Este script define un paso de cálculo para todo el cubo.  
  
 **Script MDX definido por el usuario**  
 Después de crear el cubo, se pueden agregar scripts MDX definidos por el usuario que amplían las capacidades de cálculo del cubo.  
  
## <a name="the-default-mdx-script"></a>Script MDX predeterminado  
 El script MDX predeterminado que crea [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] al definir un cubo contiene una sola instrucción CALCULATE. Esta única instrucción CALCULATE se ubica al comienzo del script MDX predeterminado e indica que todo el cubo debe calcularse durante el primer paso de cálculo.  
  
 El script MDX predeterminado también incluye los comandos que crean conjuntos con nombre, asignaciones y miembros calculados creados en el Diseñador de cubos:  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] agrega directamente comandos de script al script MDX predeterminado.  
  
-   Para cada conjunto con nombre del cubo existe una instrucción CREATE SET correspondiente en el script MDX predeterminado.  
  
-   Para cada miembro calculado definido en el cubo existe una instrucción CREATE MEMBER correspondiente en el script MDX predeterminado.  
  
 Para controlar el orden de los comandos de script, conjuntos con nombre y miembros calculados del script MDX predeterminado puede utilizar la pestaña **Cálculos** del Diseñador de cubos. Para más información sobre cómo definir los cálculos almacenados en el script MDX predeterminado, vea [Cálculos en modelos multidimensionales](../calculations-in-multidimensional-models.md).  
  
 Si no se asocia ningún script MDX a un cubo, éste asume el script MDX predeterminado. Es necesario asociar los cubos a un script MDX como mínimo, ya que los cubos se basan en estos scripts para determinar el comportamiento del cálculo. Es decir, un cubo que no se haya asociado a ningún script MDX o que se haya asociado a un script MDX vacío no podría calcular ninguna celda. Si crea los cubos mediante programación, mediante comandos ASSL (Analysis Services Scripting Language) o mediante los Objetos de administración de análisis (AMO), se recomienda crear un script MDX predeterminad que contenga una única instrucción CALCULATE para el cubo.  
  
## <a name="mdx-script-content"></a>Contenido del script MDX  
 Un script MDX puede incluir las siguientes instrucciones y expresiones:  
  
 Todas las instrucciones de scripting MDX  
 En los scripts MDX, las instrucciones de scripting MDX controlan el contexto y el ámbito de los cálculos y administran el comportamiento de otras instrucciones del script MDX. Esta categoría incluye las siguientes instrucciones:  
  
-   [CALCULATE](/sql/mdx/mdx-scripting-calculate)  
  
-   [INMOVILICE](/sql/mdx/mdx-scripting-freeze)  
  
-   [ID](/sql/mdx/mdx-scripting-scope)  
  
 Para más información sobre las instrucciones para scripting de MDX, vea [Instrucciones para scripting de MDX &#40;MDX&#41;](/sql/mdx/mdx-scripting-statements-mdx).  
  
 [CREATE MEMBER](/sql/mdx/mdx-data-definition-create-member)  
 La instrucción CREATE MEMBER crea miembros calculados. Para más información sobre cómo crear miembros calculados, vea [Generar miembros calculados en MDX &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md).  
  
 [CREATE SET](/sql/mdx/mdx-data-definition-create-set)  
 La instrucción CREATE SET crea conjuntos con nombre. Para más información sobre cómo crear conjuntos con nombre, vea [Crear conjuntos con nombre en MDX &#40;MDX&#41;](mdx-named-sets-building-named-sets.md).  
  
 Instrucciones condicionales  
 Las instrucciones condicionales agregan lógica condicional a los scripts MDX. En esta categoría se incluyen las instrucciones [CASE](/sql/mdx/case-statement-mdx) e [IF](/sql/mdx/mdx-scripting-if) .  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Referencia del lenguaje MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)   
 [Aspectos básicos de scripting MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
  
