---
title: TRY_CAST (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TRY_CAST_TSQL
- TRY_CAST
dev_langs:
- TSQL
helpviewer_keywords:
- TRY_CAST function
ms.assetid: ea3a16de-995b-415c-b5f0-9355cf7bb401
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 09c5b6060798f28541f61e763954ed44920cf83d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="trycast-transact-sql"></a>TRY_CAST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una conversión de valor al tipo de datos especificado si la conversión se realiza correctamente; de lo contrario, devuelve NULL.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
TRY_CAST ( expression AS data_type [ ( length ) ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Valor que se puede convertir. Cualquier expresión válida.  
  
 *data_type*  
 Tipo de datos al que se va a convertir *expresión*.  
  
 *length*  
 Número entero opcional que especifica la longitud del tipo de datos de destino.  
  
 El intervalo de valores aceptables está determinado por el valor de *data_type*.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve una conversión de valor al tipo de datos especificado si la conversión se realiza correctamente; de lo contrario, devuelve NULL.  
  
## <a name="remarks"></a>Comentarios  
 **TRY_CAST** toma el valor pasado a él e intenta convertir al especificado *data_type*. Si la conversión se realiza correctamente, **TRY_CAST** devuelve el valor especificado *data_type*; si se produce un error, se devuelve null. Sin embargo si se solicita una conversión que no está explícitamente permitida, a continuación, **TRY_CAST** produce un error.  
  
 **TRY_CAST** no es una palabra clave reservada de nuevo y está disponible en todos los niveles de compatibilidad. **TRY_CAST** tiene la misma semántica que **TRY_CONVERT** al conectarse a servidores remotos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-trycast-returns-null"></a>A. TRY_CAST devuelve NULL  
 En el ejemplo siguiente se muestra que TRY_CAST devuelve NULL cuando se produce un error en la conversión.  
  
```tsql  
SELECT   
    CASE WHEN TRY_CAST('test' AS float) IS NULL   
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
  
```tsql  
SET DATEFORMAT dmy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
----------------------  
NULL  
  
(1 row(s) affected)  
```  
  
### <a name="b-trycast-fails-with-an-error"></a>B. TRY_CAST genera un error  
 En el ejemplo siguiente, se muestra que TRY_CAST devuelve un error cuando la conversión no está explícitamente permitida.  
  
```tsql  
SELECT TRY_CAST(4 AS xml) AS Result;  
GO  
```  
  
 El resultado de esta instrucción es un error, ya que un entero no se puede convertir en un tipo de datos xml.  
  
```  
Explicit conversion from data type int to xml is not allowed.  
```  
  
### <a name="c-trycast-succeeds"></a>C. TRY_CAST se realiza correctamente  
 Este ejemplo demuestra que la expresión debe tener el formato esperado.  
  
```  
SET DATEFORMAT mdy;  
SELECT TRY_CAST('12/31/2010' AS datetime2) AS Result;  
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
 [TRY_CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/try-convert-transact-sql.md)   
 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

