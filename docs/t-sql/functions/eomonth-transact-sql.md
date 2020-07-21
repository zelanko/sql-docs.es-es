---
title: EOMONTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EOMONTH
- EOMONTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EOMONTH function
ms.assetid: 1d060d8e-3297-4244-afef-57df2f8f92e2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3092c848f11ba62301755d9c112b49d6fb4d2fa7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732404"
---
# <a name="eomonth-transact-sql"></a>EOMONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

Esta función devuelve el último día del mes que contiene la fecha especificada, con un desplazamiento opcional.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
EOMONTH ( start_date [, month_to_add ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*start_date*  
Expresión de fecha que especifica la fecha para la que se devuelve el último día del mes.  
  
*month_to_add*  
Expresión opcional de tipo entero que especifica el número de meses que se van a agregar a *start_date*.  
  
Si el argumento, *month_to_add* tiene un valor, `EOMONTH` agrega el número especificado de meses a *start_date* y, después, devuelve el último día del mes de la fecha resultante. Si esto desborda el intervalo válido de fechas, `EOMONTH` producirá un error.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 **date**  
  
## <a name="remarks"></a>Observaciones  
La función `EOMONTH` se puede enviar de forma remota a servidores [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores. No se puede enviar de forma remota a servidores con una versión anterior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-eomonth-with-explicit-datetime-type"></a>A. EOMONTH con un tipo datetime explícito  
  
```sql 
DECLARE @date DATETIME = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  

### <a name="b-eomonth-with-string-parameter-and-implicit-conversion"></a>B. EOMONTH con parámetro de cadena y conversión implícita  
  
```sql
DECLARE @date VARCHAR(255) = '12/1/2011';  
SELECT EOMONTH ( @date ) AS Result;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
2011-12-31  
  
(1 row(s) affected)  
```  
  
### <a name="c-eomonth-with-and-without-the-month_to_add-parameter"></a>C. EOMONTH con y sin el parámetro month_to_add  
  
Los valores que se muestran en estos conjuntos de resultados reflejan una fecha de ejecución entre `12/01/2011` y `12/31/2011`, ambos incluidos.

```sql  
DECLARE @date DATETIME = GETDATE();  
SELECT EOMONTH ( @date ) AS 'This Month';  
SELECT EOMONTH ( @date, 1 ) AS 'Next Month';  
SELECT EOMONTH ( @date, -1 ) AS 'Last Month';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
This Month  
-----------------------  
2011-12-31  
  
(1 row(s) affected)  
  
Next Month  
-----------------------  
2012-01-31  
  
(1 row(s) affected)  
  
Last Month  
-----------------------  
2011-11-30  
  
(1 row(s) affected)  
```
