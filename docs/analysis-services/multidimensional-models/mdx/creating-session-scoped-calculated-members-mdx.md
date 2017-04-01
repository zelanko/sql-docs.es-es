---
title: "Crear miembros calculados de &#225;mbito de sesi&#243;n (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
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
  - "CREATE MEMBER, instrucción"
  - "miembros calculados de ámbito de sesión [MDX]"
ms.assetid: 2875ed89-2c26-4645-8ed9-8848479d110f
caps.latest.revision: 30
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Crear miembros calculados de &#225;mbito de sesi&#243;n (MDX)
  Para crear un miembro calculado que esté disponible en una sesión de expresiones multidimensionales (MDX), es necesario usar la instrucción [CREATE MEMBER](../Topic/CREATE%20MEMBER%20Statement%20\(MDX\).md). Un miembro calculado creado mediante la instrucción CREATE MEMBER no se eliminará hasta que se cierre la sesión MDX.  
  
 Como se indica en este tema, la sintaxis de la instrucción CREATE MEMBER es muy sencilla y fácil de usar.  
  
> [!NOTE]  
>  Para más información sobre los miembros calculados, vea [Generar miembros calculados en MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/building-calculated-members-in-mdx-mdx.md).  
  
## Sintaxis de CREATE MEMBER  
 Utilice la siguiente sintaxis para agregar la instrucción CREATE MEMBER a la instrucción MDX:  
  
```  
CREATE [SESSION] MEMBER [<cube-name>.]<fully-qualified-member-name> AS <expression> [,<property-definition-list>]  
<cube name> ::= CURRENTCUBE | <Cube Name>  
<property-definition-list> ::= <property-definition>  
  | <property-definition>, <property-definition-list>  
<property-definition> ::= <property-identifier> = <property-value>  
<property-identifier> ::= VISIBLE | SOLVEORDER | SOLVE_ORDER | FORMAT_STRING | NON_EMPTY_BEHAVIOR <ole db member properties>  
```  
  
 En la sintaxis de la instrucción CREATE MEMBER, el valor `fully-qualified-member-name` es el nombre completo del miembro calculado. El nombre completo incluye la dimensión o el nivel al que se asocia el miembro calculado. El valor `expression` devuelve el valor del miembro calculado después de haber evaluado el valor de la expresión.  
  
## Ejemplo de CREATE MEMBER  
 En el siguiente ejemplo se utiliza la instrucción CREATE MEMBER para crear el miembro calculado `LastFourStores` . Este miembro calculado devuelve la suma de las unidades vendidas en los cuatro últimos almacenes, y está disponible mientras dure la sesión del cubo.  
  
```  
Create Session Member [Store].[Measures].LastFourStores as   
sum(([Stores].[ByLocation].Lag(3) :  
[Stores].[ByLocation].NextMember), [Measures].[Units Sold])  
```  
  
## Vea también  
 [Crear miembros calculados en el ámbito de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/creating-query-scoped-calculated-members-mdx.md)  
  
  