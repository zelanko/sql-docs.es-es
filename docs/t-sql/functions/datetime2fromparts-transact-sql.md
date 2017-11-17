---
title: DATETIME2FROMPARTS (Transact-SQL) | Documentos de Microsoft
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
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: f54170fc9f17ff7eb69f5de8cfdf865fd31bd4d8
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="datetime2fromparts-transact-sql"></a>DATETIME2FROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Devuelve un **datetime2** valor para la fecha y hora especificadas y con la precisión especificada.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATETIME2FROMPARTS ( year, month, day, hour, minute, seconds, fractions, precision )  
```  
  
## <a name="arguments"></a>Argumentos  
*año*  
Expresión entera que especifica un año.
  
*mes*  
Expresión entera que especifica un mes.
  
*día*  
Expresión entera que especifica un día.
  
 *hora*  
Expresión entera que especifica horas.
  
*minuto* expresión entera que especifica los minutos.
  
*segundos*  
Expresión entera que especifica segundos.
  
*fracciones*  
Expresión entera que especifica fracciones.
  
*precisión*  
Literal entero que especifica la precisión de la **datetime2** valor va a devolver.
  
## <a name="return-types"></a>Tipos de valor devuelto
**datetime2 (** *precisión* **)**
  
## <a name="remarks"></a>Comentarios  
**DATETIME2FROMPARTS** devuelve un totalmente inicializado **datetime2** valor. Si los argumentos no son válidos, se produce un error. Si los argumentos necesarios son NULL, se devuelve un valor NULL. Sin embargo, si la *precisión* del argumento es null, a continuación, se produce un error.
  
El *fracciones* argumento depende el *precisión* argumento. Por ejemplo, si *precisión* es 7, a continuación, cada fracción representa 100 nanosegundos; si *precisión* es 3, cada fracción representa un milisegundo. Si el valor de *precisión* es cero, el valor de *fracciones* también debe ser cero; en caso contrario, se produce un error.
  
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
En el ejemplo siguiente se muestra el uso de la *fracciones* y *precisión* parámetros:
  
1.  Cuando *fracciones* tiene un valor de 5 y *precisión* tiene un valor de 1, a continuación, el valor de *fracciones* representa 5/10 de un segundo.  
  
2.  Cuando *fracciones* tiene un valor de 50 y *precisión* tiene un valor de 2, a continuación, el valor de *fracciones* representa 50/100 de un segundo.  
  
3.  Cuando *fracciones* tiene un valor de 500 y *precisión* tiene un valor de 3, a continuación, el valor de *fracciones* representa 500/1000 de un segundo.  
  
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
  
  


