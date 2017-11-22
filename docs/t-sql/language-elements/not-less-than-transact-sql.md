---
title: '!&lt; (No menor que) (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '!<'
- Not Less
- '!<_TSQL'
- Not Less Than
- Less Than
dev_langs: TSQL
helpviewer_keywords:
- '!< (not less than)'
- not less than operator (!<)
ms.assetid: ecbb598e-58a2-4b6c-90b4-3ad5bdfcae39
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72275fdc65d349c4afcd7e0c21454510efbb1f40
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="lt-not-less-than-transact-sql"></a>!&lt; (No menor que) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Compara dos expresiones (es un operador de comparación). Cuando se comparan expresiones no NULL, el resultado es TRUE si el operando de la izquierda no tiene un valor menor que el de la derecha; de lo contrario, el resultado es FALSE. Si uno o ambos operandos son NULL, vea el tema [SET ANSI_NULLS &#40; Transact-SQL &#41; ](../../t-sql/statements/set-ansi-nulls-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
expression !< expression  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md). Ambas expresiones deben tener tipos de datos que se puedan convertir implícitamente. La conversión depende de las reglas de [prioridad de tipo de datos](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="result-types"></a>Tipos de resultado  
 **Boolean**  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
