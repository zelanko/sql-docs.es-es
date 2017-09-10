---
title: REPLACE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REPLACE_TSQL
- REPLACE
dev_langs:
- TSQL
helpviewer_keywords:
- first string expression [SQL Server]
- replacing string expression
- third string expressions [SQL Server]
- second string expressions [SQL Server]
- REPLACE function
ms.assetid: 8a7aaaf2-62e3-46c0-8e44-fa22290dd86b
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8340c1b3af3ad843a0e3080cbfdc771d7353c7b7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="replace-transact-sql"></a>REPLACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Reemplaza todas las instancias de un valor de cadena especificado por otro valor de cadena.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
REPLACE ( string_expression , string_pattern , string_replacement )  
```  
  
## <a name="arguments"></a>Argumentos  
 *string_expression*  
 Es la cadena [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que se debe buscar. *string_expression* pueden ser de un tipo de datos de carácter o binario.  
  
 *string_*patrón  
 Es la subcadena que se va a buscar. *string_pattern* puede ser de un tipo de datos de carácter o binario. *string_pattern* no puede ser una cadena vacía (") y no debe superar el número máximo de bytes que cabe en una página.  
  
 *string_*reemplazo  
 Es la cadena de reemplazo. *string_replacement* puede ser de un tipo de datos de carácter o binario.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve **nvarchar** si uno de los argumentos de entrada es el **nvarchar** el tipo de datos; en caso contrario, REPLACE devuelve **varchar**.  
  
 Devuelve NULL si alguno de los argumentos es NULL.  
  
 Si *string_expression* no es del tipo **varchar (max)** o **nvarchar (max), reemplazar** trunca el valor devuelto en 8.000 bytes. Para devolver valores mayores de 8.000 bytes, *string_expression* debe convertirse explícitamente a un tipo de datos de valores grandes.  
  
## <a name="remarks"></a>Comentarios  
 REPLACE realiza comparaciones basándose en la intercalación de la entrada. Para realizar una comparación en la intercalación especificada, puede usar [COLLATE](~/t-sql/statements/collations.md) para aplicar una intercalación explícita a la entrada.  
  
 0 x 0000 (**char(0)**) es un carácter no definido en las intercalaciones de Windows y no se pueden incluir en REPLACE.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo reemplaza la cadena `cde` de `abcdefghi` por `xxx`.  
  
```sql  
SELECT REPLACE('abcdefghicde','cde','xxx');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
abxxxfghixxx  
(1 row(s) affected)  
```  
  
 El siguiente ejemplo utiliza la función `COLLATE`.  
  
```sql  
SELECT REPLACE('This is a Test'  COLLATE Latin1_General_BIN,  
'Test', 'desk' );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
------------  
This is a desk  
(1 row(s) affected)  
```  

  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  

