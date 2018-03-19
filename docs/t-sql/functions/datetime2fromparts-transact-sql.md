---
title: DATETIME2FROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATETIME2FROMPARTS_TSQL
- DATETIME2FROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIME2FROMPARTS function
ms.assetid: 632b757d-d2d1-43a5-b870-792a779ae204
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ce109671228e82bc0f02e9920b2ef98c9bbcdb83
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Devuelve un valor **datetime2** para la fecha y la hora especificadas, y con la precisión indicada.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumentos  
*year*  
Expresión entera que especifica un año.
  
*month*  
Expresión entera que especifica un mes.
  
*day*  
Expresión entera que especifica un día.
  
 *hour*  
Expresión entera que especifica horas.
  
*minute* Expresión entera que especifica minutos.
  
*segundos*  
Expresión entera que especifica segundos.
  
*fractions*  
Expresión entera que especifica fracciones.
  
*precisión*  
Literal entero que especifica la precisión del valor **datetime2** que se va a devolver.
  
## <a name="return-types"></a>Tipos de valor devueltos
**datetime2(** *precision* **)**
  
## <a name="remarks"></a>Notas  
**DATETIME2FROMPARTS** devuelve un valor de **datetime2** totalmente inicializado. Si los argumentos no son válidos, se generará un error. Si los argumentos necesarios son NULL, se devuelve un valor NULL. Pero si el argumento *precision* es NULL, se generará un error.
  
El argumento *fractions* depende del argumento *precision*. Por ejemplo, si *precision* es 7, cada fracción representa 100 nanosegundos; si *precision* es 3, cada fracción representa un milisegundo. Si el valor de *precision* es cero, el valor de *fractions* también debe ser cero; de lo contrario, se generará un error.
  
Esta función se puede enviar de forma remota a servidores de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y superiores. No se puede enviar de forma remota a servidores que tengan una versión inferior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. Ejemplo simple sin fracciones de segundo  
  
```sql
SELECT DATETIME2FROMPARTS ( 2010, 12, 31, 23, 59, 59, 0, 0 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
---------------------------  
2010-12-31 23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Ejemplo con fracciones de segundo  
En el siguiente ejemplo se muestra el uso de los parámetros *fractions* y *precision*:
  
1.  Cuando *fractions* tiene el valor 5 y *precision*, el valor 1, el valor de *fractions* representa 5/10 de un segundo.  
  
2.  Cuando *fractions* tiene el valor 50 y *precision*, el valor 2, el valor de *fractions* representa 50/100 de un segundo.  
  
3.  Cuando *fractions* tiene el valor 500 y *precision*, el valor 3, el valor de *fractions* representa 500/1000 de un segundo.  
  
```sql
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 5, 1 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 50, 2 );  
SELECT DATETIME2FROMPARTS ( 2011, 8, 15, 14, 23, 44, 500, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------  
2011-08-15 14:23:44.5  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.50  
  
(1 row(s) affected)  
  
----------------------  
2011-08-15 14:23:44.500  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)
  
  

