---
title: (Dividir a igual) (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /=_TSQL
- /=
dev_langs:
- TSQL
helpviewer_keywords:
- compound operators, /=
- /= (divide equals)
ms.assetid: 9ab25d1e-5c98-4dd7-b2cd-9f49499c86e7
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c75fb8bf157f1bba666df065e238993909038418
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="divide-equals-transact-sql"></a>(Dividir a igual) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Divide un número entre otro y establece un valor en el resultado de la operación. Por ejemplo, si una variable @x es igual a 34, a continuación, @x / = 2 toma el valor original de @x, divide entre 2 y establece @x en el nuevo valor (17).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
expression /= expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de uno de los datos de tipos de la categoría numérica, excepto el **bits** tipo de datos.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos del argumento con mayor prioridad. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información, vea [&#40; división &#41; &#40; Transact-SQL &#41; ](../../t-sql/language-elements/divide-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
