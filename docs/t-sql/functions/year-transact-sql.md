---
title: "AÑO (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- YEAR
- YEAR_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server], years
- date and time [SQL Server], YEAR
- functions [SQL Server], date and time
- YEAR function [SQL Server]
- dateparts [SQL Server], year
ms.assetid: 74aa7ccc-8575-4018-80cf-14aeca379687
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 80a38599ae04209d0f8e479b8cbad16d39bef31a
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="year-transact-sql"></a>YEAR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un entero que representa el año del elemento especificado *fecha*.  
  
 Para obtener información general de todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora y funciones, vea [funciones y tipos de datos de hora y fecha &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
YEAR ( date )  
```  
  
## <a name="arguments"></a>Argumentos  
 *date*  
 Es una expresión que se pueda resolver como un **tiempo**, **fecha**, **smalldatetime**, **datetime**, **datetime2**, o **datetimeoffset** valor. El *fecha* argumento puede ser una expresión, expresión de columna, variable definida por el usuario o literal de cadena.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="return-value"></a>Valor devuelto  
 YEAR devuelve el mismo valor que [DATEPART](../../t-sql/functions/datepart-transact-sql.md) (**año**, *fecha*).  
  
 Si *fecha* contiene solo una parte horaria, el valor devuelto es 1900, el año de base.  
  
## <a name="examples"></a>Ejemplos  
 La siguiente instrucción devuelve `2010`. Este número corresponde al año.  
  
```  
SELECT YEAR('2010-04-30T01:01:01.1234567-07:00');  
```  
  
 La siguiente instrucción devuelve `1900, 1, 1`. El argumento para *fecha* es el número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como 1 de enero de 1900.  
  
```  
SELECT YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 La siguiente instrucción devuelve `1900, 1, 1`. El argumento para *fecha* es el número `0`. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta `0` como 1 de enero de 1900.  
  
```  
SELECT TOP 1 YEAR(0), MONTH(0), DAY(0);  
```  
  
## <a name="see-also"></a>Vea también  
 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  


