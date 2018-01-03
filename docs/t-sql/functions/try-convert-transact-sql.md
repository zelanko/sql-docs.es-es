---
title: TRY_CONVERT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- TRY_CONVERT_TSQL
- TRY_CONVERT
dev_langs: TSQL
helpviewer_keywords: TRY_CONVERT function
ms.assetid: 3e6e7825-6482-4cb2-a8c2-9abc99e265a6
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5fedc9777146d24cb04fb7652344f244babc8246
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="tryconvert-transact-sql"></a>TRY_CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una conversión de valor al tipo de datos especificado si la conversión se realiza correctamente; de lo contrario, devuelve NULL.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TRY_CONVERT ( data_type [ ( length ) ], expression [, style ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *data_type [(longitud)]*  
 Tipo de datos al que se va a convertir *expresión*.  
  
 *expression*  
 Valor que se puede convertir.  
  
 *estilo*  
 Expresión de entero opcional que especifica cómo la **TRY_CONVERT** función consiste en traducir *expresión*.  
  
 *estilo* acepta los mismos valores que la *estilo* parámetro de la **convertir** función. Para obtener más información, vea [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
 El intervalo de valores aceptables está determinado por el valor de *data_type*. Si *estilo* es null, entonces **TRY_CONVERT** devuelve null.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve una conversión de valor al tipo de datos especificado si la conversión se realiza correctamente; de lo contrario, devuelve NULL.  
  
## <a name="remarks"></a>Comentarios  
 **TRY_CONVERT** toma el valor pasado a él e intenta convertir al especificado *data_type*. Si la conversión se realiza correctamente, **TRY_CONVERT** devuelve el valor especificado *data_type*; si se produce un error, se devuelve null. Sin embargo si se solicita una conversión que no está explícitamente permitida, a continuación, **TRY_CONVERT** produce un error.  
  
 **TRY_CONVERT** es una palabra reservada en el nivel de compatibilidad 110 y posteriores.  
  
 Esta función se puede enviar de forma remota a servidores que tengan una versión de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y superior. No se puede enviar de forma remota a servidores que tengan una versión inferior a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-tryconvert-returns-null"></a>A. TRY_CONVERT devuelve NULL  
 En el ejemplo siguiente se muestra que TRY_CONVERT devuelve NULL cuando se produce un error en la conversión.  
  
```sql  
SELECT   
    CASE WHEN TRY_CONVERT(float, 'test') IS NULL   
    THEN 'Cast failed'  
    ELSE 'Cast succeeded'  
END AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
------------  
Cast failed  
  
(1 row(s) affected)  
```  
  
 En el ejemplo siguiente se demuestra que la expresión debe tener el formato esperado.  
  
```sql  
SET DATEFORMAT dmy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-tryconvert-fails-with-an-error"></a>B. TRY_CONVERT genera un error  
 En el ejemplo siguiente, se muestra que TRY_CONVERT devuelve un error cuando la conversión no está explícitamente permitida.  
  
```sql  
SELECT TRY_CONVERT(xml, 4) AS Result;  
GO  
```  
  
 El resultado de esta instrucción es un error, ya que un entero no se puede convertir en un tipo de datos xml.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-tryconvert-succeeds"></a>C. TRY_CONVERT se realiza correctamente  
 Este ejemplo demuestra que la expresión debe tener el formato esperado.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CONVERT(datetime2, '12/31/2010') AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------------------  
2010-12-31 00:00:00.0000000  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  
