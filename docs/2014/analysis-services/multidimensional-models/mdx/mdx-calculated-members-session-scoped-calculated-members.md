---
title: Crear ámbito de sesión calcula miembros (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- CREATE MEMBER statement
- session-scoped calculated members [MDX]
ms.assetid: 2875ed89-2c26-4645-8ed9-8848479d110f
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d8e51a2fa5d8179134ac2654f55e9da7ff5ced67
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106231"
---
# <a name="creating-session-scoped-calculated-members-mdx"></a>Crear miembros calculados de ámbito de sesión (MDX)
  Para crear un miembro calculado que esté disponible en una sesión de expresiones multidimensionales (MDX), es necesario usar la instrucción [CREATE MEMBER](/sql/mdx/mdx-data-definition-create-member). Un miembro calculado creado mediante la instrucción CREATE MEMBER no se eliminará hasta que se cierre la sesión MDX.  
  
 Como se indica en este tema, la sintaxis de la instrucción CREATE MEMBER es muy sencilla y fácil de usar.  
  
> [!NOTE]  
>  Para más información sobre los miembros calculados, vea [Generar miembros calculados en MDX &#40;MDX&#41;](mdx-calculated-members-building-calculated-members.md).  
  
## <a name="create-member-syntax"></a>Sintaxis de CREATE MEMBER  
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
  
## <a name="create-member-example"></a>Ejemplo de CREATE MEMBER  
 En el siguiente ejemplo se utiliza la instrucción CREATE MEMBER para crear el miembro calculado `LastFourStores` . Este miembro calculado devuelve la suma de las unidades vendidas en los cuatro últimos almacenes, y está disponible mientras dure la sesión del cubo.  
  
```  
Create Session Member [Store].[Measures].LastFourStores as   
sum(([Stores].[ByLocation].Lag(3) :  
[Stores].[ByLocation].NextMember), [Measures].[Units Sold])  
```  
  
## <a name="see-also"></a>Vea también  
 [Crear ámbito de consulta miembros calculados &#40;MDX&#41;](mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
