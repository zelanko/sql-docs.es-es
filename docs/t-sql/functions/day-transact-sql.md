---
title: "DÍA (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DAY_TSQL
- DAY
dev_langs:
- TSQL
helpviewer_keywords:
- date and time [SQL Server], DAY
- dates [SQL Server], functions
- DAY function [SQL Server]
- dates [SQL Server], days
- functions [SQL Server], date and time
- dateparts [SQL Server], day
ms.assetid: 2f4410ea-fd3e-4d69-ac4b-3b0091a084bc
caps.latest.revision: 41
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 9edfdc46ede4c090080c09253e2bb213a384816c
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="day-transact-sql"></a>DAY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve un entero que representa el día (día del mes) del elemento especificado *fecha*.
  
Para obtener información general de todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora y funciones, vea [funciones y tipos de datos de hora y fecha & #40; Transact-SQL & #41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DAY ( date )  
```  
  
## <a name="arguments"></a>Argumentos  
*date*  
Es una expresión que se pueda resolver como un **tiempo**, **fecha**, **smalldatetime**, **datetime**, **datetime2**, o **datetimeoffset** valor. El *fecha* argumento puede ser una expresión, expresión de columna, variable definida por el usuario o literal de cadena.
  
## <a name="return-type"></a>Tipo devuelto  
**int**
  
## <a name="return-value"></a>Valor devuelto  
DAY devuelve el mismo valor que [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**día**, *fecha*).
  
Si *fecha* contiene solo una parte horaria, el valor devuelto es 1, el día base.
  
## <a name="examples"></a>Ejemplos  
La siguiente instrucción devuelve `30`. Este número corresponde al día.
  
```sql
SELECT DAY('2015-04-30 01:01:01.1234567');  
```  
  
La siguiente instrucción devuelve `1900, 1, 1`. El argumento para *fecha* es el número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como 1 de enero de 1900.
  
```sql
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  



