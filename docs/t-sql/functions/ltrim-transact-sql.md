---
title: LTRIM (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 02/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- LTRIM
- LTRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- leading blanks
- deleting blank spaces
- characters [SQL Server], blanks
- removing blank spaces
- LTRIM function
- blank characters [SQL Server]
ms.assetid: 369ed340-1a09-4597-a9eb-6720156cd39a
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad63999f685b31848ea505fd5a671d1e163ddc91
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="ltrim-transact-sql"></a>LTRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una expresión de caracteres tras quitar todos los espacios iniciales en blanco.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
LTRIM ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de caracteres o datos binarios. *character_expression* puede ser una constante, variable o columna. *character_expression* debe ser de un tipo de datos, excepto **texto**, **ntext**, y **imagen**, que se pueden convertir implícitamente a **varchar** . De lo contrario, utilice [conversión](../../t-sql/functions/cast-and-convert-transact-sql.md) para convertir explícitamente *character_expression*.  
  
## <a name="return-type"></a>Tipo devuelto  
 **varchar** o **nvarchar**  
  
## <a name="examples"></a>Ejemplos  

### <a name="a-simple-example"></a>A. Ejemplo sencillo   

 En el ejemplo siguiente se usa LTRIM para quitar los espacios iniciales de una expresión de caracteres.  
  
```tsql  
SELECT LTRIM('     Five spaces are at the beginning of this string.') FROM sys.databases;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `---------------------------------------------------------------`  
  `Five spaces are at the beginning of this string.`  

### <a name="b-example-using-a-variable"></a>B: ejemplo usando una variable   
  
 En el siguiente ejemplo se utiliza `LTRIM` para quitar espacios iniciales de una variable de caracteres.  
  
```  
DECLARE @string_to_trim varchar(60);  
SET @string_to_trim = '     5 spaces are at the beginning of this string.';  
SELECT 
    @string_to_trim AS 'Original string',
    LTRIM(@string_to_trim) AS 'Without spaces';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Original string Without spaces
--------------------------------------------------- ---------------------------------------------
     5 spaces are at the beginning of this string.  5 spaces are at the beginning of this string.
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  



