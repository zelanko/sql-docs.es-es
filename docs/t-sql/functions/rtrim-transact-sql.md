---
title: RTRIM (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/05/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RTRIM_TSQL
- RTRIM
dev_langs:
- TSQL
helpviewer_keywords:
- RTRIM function
- character strings [SQL Server], trailing blanks
- blank characters [SQL Server]
- trailing blanks
ms.assetid: 52fd6e8d-650c-4f66-abcf-67765aa5aa83
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 838bad2a5d5434fdb3bb338ba32f75ebdfd1460c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="rtrim-transact-sql"></a>RTRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una cadena de caracteres después de truncar todos los espacios finales.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
RTRIM ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de datos de caracteres. *character_expression* puede ser una constante, variable o columna de caracteres o datos binarios.  
  
 *character_expression* debe ser de un tipo de datos que es implícitamente convertible a **varchar**. De lo contrario, utilice [conversión](../../t-sql/functions/cast-and-convert-transact-sql.md) para convertir explícitamente *character_expression*.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varchar** o **nvarchar**  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-example"></a>A. Ejemplo sencillo  
 El siguiente ejemplo toma una cadena de caracteres que tiene espacios al final de la frase y devuelve el texto sin esos espacios.  
  
```  
SELECT RTRIM('Removes trailing spaces.   ');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
  `Removes trailing spaces.`  
  
### <a name="b-simple-example"></a>B: ejemplo simple  
 En el ejemplo siguiente se muestra cómo utilizar `RTRIM` para quitar los espacios finales. No existe este tiempo es otra cadena concatenada a la primera cadena para mostrar que los espacios han desaparecido.  
  
```  
SELECT RTRIM('Four spaces are after the period in this sentence.    ') + 'Next string.';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
`Four spaces are after the period in this sentence.Next string.`  

### <a name="c-using-rtrim-with-a-variable"></a>C. Usar RTRIM con una variable  
 En el ejemplo siguiente se muestra cómo utilizar `RTRIM` para quitar los espacios finales de una variable de caracteres.  
  
```  
DECLARE @string_to_trim varchar(60);  
SET @string_to_trim = 'Four spaces are after the period in this sentence.    ';  
SELECT @string_to_trim + ' Next string.';  
SELECT RTRIM(@string_to_trim) + ' Next string.';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```sql   
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence.     Next string.  
 
 (1 row(s) affected)`  
 
 -------------------------------------------------------------------------  
 Four spaces are after the period in this sentence. Next string.  
 
 (1 row(s) affected)
 ```  
  

  
## <a name="see-also"></a>Vea también  
 [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [RECORTE &#40; Transact-SQL &#41;](../../t-sql/functions/trim-transact-sql.md)  
 [LTRIM &#40; Transact-SQL &#41;](../../t-sql/functions/ltrim-transact-sql.md)  
  
  



