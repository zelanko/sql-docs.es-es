---
title: DATEDIFF_BIG (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6c8228f0db3e37fe3bf6425d60fd4f9067e92220
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Devuelve el recuento (entero grande firmado) del elemento especificado *datepart* traspasan los límites entre especificado *startdate* y *enddate*.
  
Para obtener información general de todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora y funciones, vea [funciones y tipos de datos de hora y fecha &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumentos  
*parte de fecha*  
Es la parte de *startdate* y *enddate* que especifica el tipo de límite cruzado. La siguiente tabla se recogen válidos *datepart* argumentos. Los equivalentes de variables definidas por el usuario no son válidos.
  
|*parte de fecha*|Abreviaturas|  
|---|---|
|**año**|**yy, yyyy**|  
|**trimestre**|**TT, q**|  
|**mes**|**mm, m**|  
|**DAYOFYEAR**|**dy, y**|  
|**día**|**dd, d**|  
|**semana**|**wk, ww**|  
|**hora**|**hh**|  
|**minuto**|**Mi, n**|  
|**segundo**|**ss, s**|  
|**milisegundo**|**MS**|  
|**microsegundos**|**MCS**|  
|**nanosegundos**|**NS**|  
  
*startdate*  
Es una expresión que se pueda resolver como un **tiempo**, **fecha**, **smalldatetime**, **datetime**, **datetime2**, o **datetimeoffset** valor. *fecha* puede ser una expresión, la expresión de columna, la variable definida por el usuario o la cadena literal. *StartDate* se resta de *enddate*.  
Para evitar ambigüedades, use años de cuatro dígitos. Para obtener información sobre los años de dos dígitos, consulte [configurar two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
*EndDate*  
Vea *startdate*.
  
## <a name="return-type"></a>Tipo devuelto  
 Firmado   
        **bigint**  
  
## <a name="return-value"></a>Valor devuelto  
Devuelve el número (con signo bigint) de los límites de datepart especificado se traspasa entre los especificados startdate y enddate.
-   Cada *datepart* y sus abreviaturas devuelven el mismo valor.  
  
Si el valor devuelto está fuera del intervalo de **bigint** (-9.223.372.036.854.775.808 a 9.223.372.036.854.775.807), se devuelve un error. Para **milisegundo**, la diferencia máxima entre *startdate* y *enddate* es 24 días, 20 horas, 31 minutos y 23,647 segundos. Para **segundo**, la diferencia máxima es de 68 años.
  
Si *startdate* y *enddate* tienen asignado un valor de hora y la *datepart* no es una hora *datepart*, se devuelve 0.
  
Componente de ajuste de una zona horaria *startdate* o *endate* no se utiliza para calcular el valor devuelto.
  
Dado que [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) solo es preciso hasta el minuto, cuando un **smalldatetime** valor se utiliza para *startdate* o *enddate*, segundos y milisegundos siempre se establecen en 0 en el valor devuelto.
  
Si solo se asigna un valor de tiempo a una variable de un tipo de datos de fecha, el valor de la parte de la fecha que falta se establece en el valor predeterminado: 1900-01-01. Si solo se asigna un valor de fecha a una variable de un tipo de datos de fecha u hora, el valor de la parte de la hora que falta se establece en el valor predeterminado: 00:00:00. Si el valor *startdate* o *enddate* tener solo una parte de hora y el otro solo una parte de fecha, la hora que faltan y partes de la fecha se establecen en los valores predeterminados.
  
Si *startdate* y *enddate* son de tipos de datos de fecha diferentes y uno tiene más partes de hora o la precisión de fracciones de segundo que el otro, las partes que faltan de la otra se establecen en 0.
  
## <a name="datepart-boundaries"></a>límites de DATEPART
Las instrucciones siguientes tienen el mismo *startdate* y el mismo *endate*. Esas fechas son adyacentes y difieren y tienen una diferencia horaria de 0,0000001 segundos. La diferencia entre el *startdate* y *endate* en cada instrucción cruza un límite de calendario u hora de su *datepart*. Cada instrucción devuelve 1. Si se utilizan años diferentes en este ejemplo y si tanto *startdate* y *endate* están en la misma semana del calendario, el valor devuelto para **semana** será 0.

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
  
## <a name="remarks"></a>Comentarios  
DATEDIFF_BIG puede utilizarse en la lista select, WHERE, HAVING, GROUP BY y ORDER cláusulas BY.
  
DATEDIFF_BIG convierte implícitamente los literales de cadena como un **datetime2** tipo. Esto significa que DATEDIFF_BIG no admite el formato año-día-mes cuando se pasa la fecha como una cadena. Se debe convertir explícitamente la cadena a un **datetime** o **smalldatetime** tipo que se usa el formato de ADM.
  
Especificación de SET DATEFIRST no tiene ningún efecto en DATEDIFF_BIG. DATEDIFF_BIG siempre utiliza el domingo como el primer día de la semana para garantizar que la función es determinista.
  
## <a name="examples"></a>Ejemplos  
Los ejemplos siguientes usan diferentes tipos de expresiones como argumentos para la *startdate* y *enddate* parámetros.
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>Especificar las columnas para startdate y enddate  
El ejemplo siguiente calcula el número de límites de día que se cruzan entre las fechas en dos columnas de una tabla.
  
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
  
Para muchos ejemplos adicionales, vea los ejemplos estrechamente relacionados en [DATEDIFF &#40; Transact-SQL &#41; ](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40; Transact-SQL &#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
