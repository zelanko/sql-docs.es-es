---
title: += (Asignación de suma) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- +=
- +=_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- += (add equals)
- compound operators, +=
- assignment operators, +=
- augmented operators, +=
ms.assetid: 9ea52519-80d1-473f-b988-0572f0e2c92f
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7c916cf14a27e55e49ce3298627280306f6352fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927407"
---
# <a name="-addition-assignment-transact-sql"></a>+= (Asignación de suma) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Suma dos números y establece un valor como resultado de la operación. Por ejemplo, si una variable @x es igual a 35, @x += 2 toma el valor original de @x, suma 2 y establece @x en el nuevo valor (37).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
expression += expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md) válida de cualquiera de los tipos de datos de la categoría numérica, excepto el tipo de datos **bit**.  
  
## <a name="result-types"></a>Tipos de resultado  
 Devuelve el tipo de datos del argumento con mayor prioridad. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Notas  
 Para más información, vea [+ &#40;Suma&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/add-transact-sql.md).  
  
## <a name="see-also"></a>Consulte también  
 [Operadores compuestos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  (Expressions [Transact-SQL])  
 [Operators &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  (Operadores [Transact-SQL])  
 [+= &#40;Asignación de concatenación de cadenas&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/string-concatenation-equal-transact-sql.md)  
  
  
