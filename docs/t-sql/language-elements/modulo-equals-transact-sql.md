---
title: "% = (Asignación y módulo) (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '%=_TSQL'
- '%='
dev_langs: TSQL
helpviewer_keywords:
- '%= (modulo equals)'
- '%= (modulus assignment)'
- compound operators, %=
- assignment operators, %=
- augmented operators, %=
ms.assetid: 45e35516-1f4c-406b-a580-70a14b087847
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 06b2992236f5d1705c10249ca07793e5fe01dff6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="-modulus-assignment-transact-sql"></a>% = (Asignación y módulo) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Divide un número entre otro y establece un valor en el resultado de la operación. Por ejemplo, si una variable @x es igual a 38, a continuación, @x % = 5 toma el valor original de @x, divide entre 5 y establece @x al resto de esa división (3).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
expression %= expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de uno de los datos de tipos de la categoría numérica, excepto el **bits** tipo de datos.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos del argumento con mayor prioridad. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información, vea [% &#40; Módulo &#41; &#40; Transact-SQL &#41; ](../../t-sql/language-elements/modulo-transact-sql.md).  
  
## <a name="see-also"></a>Vea también  
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
