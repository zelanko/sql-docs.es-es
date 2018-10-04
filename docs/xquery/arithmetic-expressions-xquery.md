---
title: Expresiones aritméticas (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expressions [XQuery], arithmetic
- arithmetic expressions
ms.assetid: 90d675bf-56da-459a-9771-8cd13920a9fc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3d970209b71a842aa1c78b2f7dd0db980e0ce73e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47642653"
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
  
 Dado que **idiv** no es compatible, una solución consiste en usar el **xs:integer()** constructor:  
  
```  
DECLARE @x xml  
SET @x=''  
-- Following will not work  
-- SELECT @x.query('2 idiv 2')  
-- Workaround   
SELECT @x.query('xs:integer(2 div 3)')  
```  
  
 El tipo resultante de un operador aritmético se basa en los tipos de los valores de entrada. Si los operandos son de tipos distintos, uno o los dos, cuando sea necesario, se convertirán a un tipo base primitivo común, según la jerarquía de tipos. Para obtener información acerca de la jerarquía de tipos, vea [reglas de conversión de tipos en XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 La promoción de tipos numéricos se produce si los dos operandos son de tipos base numéricos distintos. Por ejemplo, agregando un **xs: decimal** a un **xs: Double** primero se cambiaría el valor decimal a double. A continuación, se efectuaría la suma, que daría como resultado un valor double.  
  
 Valores atómicos sin tipo se convierten al tipo de base numérico del otro operando, o **xs: Double** si el otro operando es también sin tipo.  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   Argumentos para los operadores aritméticos deben ser de tipo numérico o **untypedAtomic**.  
  
-   Operaciones en **xs: Integer** valores como resultado un valor de tipo **xs: decimal** en lugar de **xs: Integer**.  
  
  
