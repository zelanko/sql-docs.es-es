---
title: "Crear ámbito de sesión calcula miembros (MDX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE MEMBER statement
- session-scoped calculated members [MDX]
ms.assetid: 2875ed89-2c26-4645-8ed9-8848479d110f
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7c8eadd09ca4946db6618f30e48907d97147b80d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-calculated-members---session-scoped-calculated-members"></a>MDX miembros - miembros calculados de ámbito de sesión calculados
  Para crear un miembro calculado que esté disponible en una sesión de expresiones multidimensionales (MDX), es necesario usar la instrucción [CREATE MEMBER](../../../mdx/mdx-data-definition-create-member.md) . Un miembro calculado creado mediante la instrucción CREATE MEMBER no se eliminará hasta que se cierre la sesión MDX.  
  
 Como se indica en este tema, la sintaxis de la instrucción CREATE MEMBER es muy sencilla y fácil de usar.  
  
> [!NOTE]  
>  Para más información sobre los miembros calculados, vea [Generar miembros calculados en MDX &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md).  
  
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
 [Crear miembros calculados en el ámbito de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)  
  
  
