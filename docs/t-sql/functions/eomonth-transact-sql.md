---
title: EOMONTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EOMONTH
- EOMONTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EOMONTH function
ms.assetid: 1d060d8e-3297-4244-afef-57df2f8f92e2
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f9ef67d87b628f53b9bb97d6cf32ecb79aa3befb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="eomonth-transact-sql"></a>EOMONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Devuelve el último día del mes que contiene la fecha especificada, con un desplazamiento opcional.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
EOMONTH ( start_date [, month_to_add ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *start_date*  
 Expresión de fecha que especifica la fecha para la que se devuelve el último día del mes.  
  
 *month_to_add*  
 Expresión opcional de tipo entero que especifica el número de meses que se va a agregar a *start_date*.  
  
 Si se especifica este argumento, **EOMONTH** agrega el número especificado de meses a *start_date* y, después, devuelve el último día del mes de la fecha resultante. Si esto desborda el intervalo válido de fechas, se producirá un error.  
  
## <a name="return-type"></a>Tipo devuelto  
 **date**  
  
## <a name="remarks"></a>Notas  
 Esta función se puede enviar de forma remota a servidores [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y posteriores. No se puede enviar de forma remota a servidores con una versión anterior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-eomonth-with-explicit-datetime-type"></a>A. EOMONTH con un tipo datetime explícito  
  
```  
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
  
```  
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
  
### <a name="c-eomonth-with-and-without-the-monthtoadd-parameter"></a>C. EOMONTH con y sin el parámetro month_to_add  
  
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
  
  

