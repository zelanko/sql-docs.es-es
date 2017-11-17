---
title: DATETIMEOFFSETFROMPARTS (Transact-SQL) | Documentos de Microsoft
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
- DATETIMEOFFSETFROMPARTS_TSQL
- DATETIMEOFFSETFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- DATETIMEOFFSETFROMPARTS function
ms.assetid: 463da1f4-b4b6-45a3-9a95-ea1f99575542
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 665607c3b6ea9411d90137fba416d96d3d46a4c1
ms.contentlocale: es-es
ms.lasthandoff: 10/17/2017

---
# <a name="datetimeoffsetfromparts-transact-sql"></a>DATETIMEOFFSETFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Devuelve un **datetimeoffset** valor para la fecha y hora especificadas y con los desplazamientos especificados y la precisión.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATETIMEOFFSETFROMPARTS ( year, month, day, hour, minute, seconds, fractions, hour_offset, minute_offset, precision )  
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
  
*minuto*  
Expresión entera que especifica minutos.
  
*segundos*  
Expresión entera que especifica segundos.
  
*fracciones*  
Expresión entera que especifica fracciones.
  
*hour_offset*  
Expresión entera que especifica la parte de hora del ajuste de zona horaria.
  
*minute_offset*  
Expresión entera que especifica la parte de minutos del ajuste de zona horaria.
  
*precisión*  
Literal entero que especifica la precisión de la **datetimeoffset** valor va a devolver.
  
## <a name="return-types"></a>Tipos de valor devuelto
**DateTimeOffset (** *precisión* **)**
  
## <a name="remarks"></a>Comentarios  
**DATETIMEOFFSETFROMPARTS** devuelve un totalmente inicializado **datetimeoffset** tipo de datos. Los argumentos de desplazamiento se usan para representar el ajuste de zona horaria. Si se omiten los argumentos de desplazamiento, se supone que el ajuste de zona horaria es 00:00; es decir, no hay ningún ajuste de zona horaria. Si se especifican los argumentos de desplazamiento, ambos argumentos deben estar presente y ambos deben ser positivos o negativos. Si *minute_offset* se especifica sin *hour_offset*, se produce un error. Si otros argumentos no son válidos, se generará un error. Si es necesario argumentos son nulos, se devuelve un valor null. Sin embargo, si la *precisión* del argumento es null, a continuación, se produce un error.
  
El *fracciones* argumento depende el *precisión* argumento. Por ejemplo, si *precisión* es 7, a continuación, cada fracción representa 100 nanosegundos; si *precisión* es 3, cada fracción representa un milisegundo. Si el valor de *precisión* es cero, el valor de *fracciones* también debe ser cero; en caso contrario, se produce un error.
  
Esta función se puede enviar de forma remota a servidores de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y superiores. No se puede enviar de forma remota a servidores que tengan una versión inferior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. Ejemplo simple sin fracciones de segundo  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2010, 12, 31, 14, 23, 23, 0, 12, 0, 7 ) AS Result;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Result  
-------------------------------------------  
2010-12-07 00:00:00.0000000 +00:00  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. Ejemplo con fracciones de segundo  
En el ejemplo siguiente se muestra el uso de la *fracciones* y *precisión* parámetros:
1.   Cuando *fracciones* tiene un valor de 5 y *precisión* tiene un valor de 1, a continuación, el valor de *fracciones* representa 5/10 de un segundo.  
1.   Cuando *fracciones* tiene un valor de 50 y *precisión* tiene un valor de 2, a continuación, el valor de *fracciones* representa 50/100 de un segundo.  
1.   Cuando *fracciones* tiene un valor de 500 y *precisión* tiene un valor de 3, a continuación, el valor de *fracciones* representa 500/1000 de un segundo.  
  
```sql
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 5, 12, 30, 1 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 50, 12, 30, 2 );  
SELECT DATETIMEOFFSETFROMPARTS ( 2011, 8, 15, 14, 30, 00, 500, 12, 30, 3 );  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
----------------------------------  
2011-08-15 14:30:00.5 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.50 +12:30  
  
(1 row(s) affected)  
  
----------------------------------  
2011-08-15 14:30:00.500 +12:30  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
[EN la zona HORARIA & #40; Transact-SQL & #41;](../../t-sql/queries/at-time-zone-transact-sql.md)
  
  



