---
title: MONTH (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MONTH_TSQL
- MONTH
dev_langs:
- TSQL
helpviewer_keywords:
- values [SQL Server], date and time
- dates [SQL Server], functions
- month of year [SQL Server]
- date and time [SQL Server], MONTH
- dateparts [SQL Server], month
- functions [SQL Server], date and time
- dates [SQL Server], MONTH
- MONTH function [SQL Server]
ms.assetid: 9dd8aff7-b0fc-45df-b316-ead14ee9b8b7
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d060b5256841b692b5bc26bdb98914fe2645964a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="month-transact-sql"></a>MONTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un entero que representa la parte del mes de la fecha *date* especificada.  
  
 Para ver información general sobre todos los tipos de datos y funciones de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], vea [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
MONTH ( date )  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 Es una expresión que se puede resolver en un valor **time**, **date**, **smalldatetime**, **datetime**, **datetime2** o **datetimeoffset**. El argumento *date* puede ser una expresión, expresión de columna, variable definida por el usuario o literal de cadena.  
  
## <a name="return-type"></a>Tipo devuelto  
 **int**  
  
## <a name="return-value"></a>Valor devuelto  
 MONTH devuelve el mismo valor que [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**month**, *date*).  
  
 Si *date* contiene solo una parte horaria, el valor devuelto es 1, el mes base.  
  
## <a name="examples"></a>Ejemplos  
 La siguiente instrucción devuelve `4`. Este número corresponde al mes.  
  
```  
SELECT MONTH('2007-04-30T01:01:01.1234567 -07:00');  
```  
  
 La siguiente instrucción devuelve `1900, 1, 1`. El argumento para *date* es el número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como 1 de enero de 1900.  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 El siguiente ejemplo devuelve `4`. Este número corresponde al mes.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP 1 MONTH('2007-04-30T01:01:01.1234')   
FROM dbo.DimCustomer;  
```  
  
 El siguiente ejemplo devuelve `1900, 1, 1`. El argumento para *date* es el número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como 1 de enero de 1900.  
  
```  
-- Uses AdventureWorks  
  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0) FROM dbo.DimCustomer;  
```  
  
## <a name="see-also"></a>Ver también  
 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

