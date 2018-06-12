---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 26ea16e8e80fd2b8febf8a95c848490b41f0408a
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34744104"
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Esta función devuelve el recuento (como un valor entero grande con firma) de los límites *datepart* que se han cruzado entre los valores *startdate* y *enddate* especificados.
  
Vea [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) para obtener información general sobre todos los tipos de datos y las funciones de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
La parte de *startdate* y *enddate* que especifica el tipo de límite cruzado. `DATEDIFF_BIG` no aceptará los equivalentes de variables definidas por el usuario. En esta tabla se enumeran todos los argumentos válidos de *datepart*.

> [!NOTE]
> `DATEDIFF_BIG` no acepta los equivalentes de variables definidas por el usuario para los argumentos *datepart*.
  
|*datepart*|Abreviaturas|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*startdate*  
Una expresión que se puede resolver en uno de los valores siguientes:

+ **date**
+ **datetime**
+ **datetimeoffset**
+ **datetime2** 
+ **smalldatetime**
+ **time**

Para *date*, `DATEDIFF_BIG` aceptará una expresión de columna, expresión, literal de cadena o variable definida por el usuario. Un valor de literal de cadena se debe resolver en un argumento **datetime**. Para evitar problemas de ambigüedad, use años de cuatro dígitos. `DATEDIFF_BIG` resta *enddate* de *startdate*. Para evitar ambigüedades, use años de cuatro dígitos. Vea [Establecer la opción de configuración del servidor Fecha límite de año de dos dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) para obtener información sobre los años de dos dígitos.
  
*enddate*  
Vea *startdate*.
  
## <a name="return-type"></a>Tipo devuelto  

**bigint** con firma  
  
## <a name="return-value"></a>Valor devuelto  
Devuelve el recuento (como valor bigint con firma) de los límites datepart especificados que se han cruzado entre los valores startdate y enddate especificados.
-   Cada argumento *datepart* específico y las abreviaturas para ese argumento *datepart* devolverán el mismo valor.  
  
Para un valor devuelto fuera del intervalo de **bigint** (de -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807) `DATEDIFF_BIG` devuelve un error. En **millisecond**, la diferencia máxima entre *startdate* y *enddate* es de 24 días, 20 horas, 31 minutos y 23.647 segundos. En **second**, la diferencia máxima es de 68 años.
  
Si *startdate* y *enddate* solo tienen asignado un valor de hora y *datepart* no es un valor *datepart* de hora, `DATEDIFF_BIG` devuelve 0.
  
`DATEDIFF_BIG` no usa un componente de desplazamiento de zona horaria de *startdate* o *enddate* para calcular el valor devuelto.
  
Para un valor **smalldatetime** que se use para *startdate* o *enddate*, `DATEDIFF_BIG` siempre establece los segundos y milisegundos en 0 en el valor devuelto porque [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) solo es preciso hasta los minutos.
  
Si solo se asigna un valor de hora a una variable de tipo de datos de fecha, `DATEDIFF_BIG` establece el valor de la parte de la fecha que falta en el valor predeterminado: 01-01-1900. Si solo se asigna un valor de fecha a una variable de tipo de datos de fecha u hora, `DATEDIFF_BIG` establece el valor de la parte de la hora que falta en el valor predeterminado: 00:00:00. Si *startdate* o *enddate* solo tienen una parte de hora y el otro solo una parte de fecha, `DATEDIFF_BIG` establece las partes de hora y fecha que faltan en los valores predeterminados.
  
Si *startdate* y *enddate* tienen tipos de datos de fecha diferentes y uno tiene más partes de hora o precisión de fracciones de segundo que el otro, `DATEDIFF_BIG` establece las partes que faltan del otro en 0.
  
## <a name="datepart-boundaries"></a>Límites de datepart
Las instrucciones siguientes tienen los mismos valores *startdate* y *enddate*. Esas fechas son adyacentes y tienen una diferencia horaria de 0,0000001 segundos. La diferencia entre *startdate* y *enddate* en cada instrucción cruza un límite de calendario u hora de su *datepart*. Cada instrucción devuelve 1. Si *startdate* y *enddate* tienen valores de año diferentes pero tienen los mismos valores de semana del calendario, `DATEDIFF_BIG` devolverá 0 para *datepart* **week**.

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Notas  
Use `DATEDIFF_BIG` en las cláusulas SELECT <list>, WHERE, HAVING, GROUP BY y ORDER BY.
  
`DATEDIFF_BIG` convierte implícitamente los literales de cadena como un tipo **datetime2**. Esto significa que `DATEDIFF_BIG` no admite el formato año-día-mes cuando la fecha se pasa como una cadena. La cadena se debe convertir explícitamente a un tipo **datetime** o **smalldatetime** para poder usar el formato año-día-mes.
  
La especificación de SET DATEFIRST no tiene efecto en `DATEDIFF_BIG`. `DATEDIFF_BIG` siempre usa el domingo como el primer día de la semana para garantizar que la función actúa de forma determinista.
  
## <a name="examples"></a>Ejemplos 
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>Especificar las columnas para startdate y enddate  
En este ejemplo se usan otros tipos de expresiones como argumentos para los parámetros *startdate* y *enddate*. Calcula el número de límites de día que se cruzan entre las fechas en dos columnas de una tabla.
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  

Vea ejemplos más estrechamente relacionados en [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
