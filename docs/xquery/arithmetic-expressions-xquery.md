---
title: Expresiones aritméticas (XQuery) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f904b4ac09539a3cac29014b86bd32e0f47db9fd
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="arithmetic-expressions-xquery"></a>Expresiones aritméticas (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Se admiten todos los operadores aritméticos, excepto para **idiv**. Los siguientes ejemplos ilustran el uso básico de operadores aritméticos:  
  
```  
DECLARE @x xml  
SET @x=''  
SELECT @x.query('2 div 2')  
SELECT @x.query('2 * 2')  
```  
  
 Dado que **idiv** no es compatible, una solución consiste en usar la **xs:integer()** constructor:  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 El tipo resultante de un operador aritmético se basa en los tipos de los valores de entrada. Si los operandos son de tipos distintos, uno o los dos, cuando sea necesario, se convertirán a un tipo base primitivo común, según la jerarquía de tipos. Para obtener información acerca de la jerarquía de tipos, vea [reglas de conversión de tipo en XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 La promoción de tipos numéricos se produce si los dos operandos son de tipos base numéricos distintos. Por ejemplo, al agregar un **xs: decimal** a una **xs: Double** , primero se cambiaría el valor decimal a double. A continuación, se efectuaría la suma, que daría como resultado un valor double.  
  
 Valores atómicos sin tipo se convierten al tipo de base numérico del otro operando, o a **xs: Double** si el otro operando es también sin tipo.  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   Argumentos para los operadores aritméticos deben ser de tipo numérico o **untypedAtomic**.  
  
-   Operaciones en **xs: Integer** los valores que se producen en un valor de tipo **xs: decimal** en lugar de **xs: Integer**.  
  
  
