---
title: UNICODE (Transact-SQL) | Documentos de Microsoft
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
- UNICODE
- UNICODE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- first character of input expression [SQL Server]
- UNICODE function
- Unicode [SQL Server], UNICODE function
ms.assetid: 5e3c40b2-8401-4741-9f2a-bae70eaa4da6
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 60d3a635b15cd1413b3c7ba6db145cd5717b7e41
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="unicode-transact-sql"></a>UNICODE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el valor entero, según la definición del estándar Unicode, para el primer carácter de la expresión de entrada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
UNICODE ( 'ncharacter_expression' )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *ncharacter_expression* **'**  
 Es un **nchar** o **nvarchar** expresión.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 En las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], la función UNICODE devuelve un punto de código UCS-2 en el intervalo de 0 a 0xFFFF. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y ediciones posteriores, cuando se utilizan intercalaciones de SC, UNICODE devuelve un punto de código UTF 16 en el intervalo de 0 a 0x10FFFF.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-unicode-and-the-nchar-function"></a>A. Utilizar las funciones UNICODE y NCHAR  
 En el ejemplo siguiente se utilizan las funciones `UNICODE` y `NCHAR` para imprimir el valor UNICODE del primer carácter de la cadena `Åkergatan` de 24 caracteres y para imprimir el verdadero primer carácter (`Å`).  
  
```  
DECLARE @nstring nchar(12);  
SET @nstring = N'Åkergatan 24';  
SELECT UNICODE(@nstring), NCHAR(UNICODE(@nstring));  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------- -   
197         Å  
```  
  
### <a name="b-using-substring-unicode-and-convert"></a>B. Utilizar SUBSTRING, UNICODE y CONVERT  
 En el ejemplo siguiente se utilizan las funciones `SUBSTRING`, `UNICODE` y `CONVERT` para imprimir el número de carácter, el carácter Unicode y el valor UNICODE de cada uno de los caracteres de la cadena `Åkergatan 24`.  
  
```  
-- The @position variable holds the position of the character currently  
-- being processed. The @nstring variable is the Unicode character   
-- string to process.  
DECLARE @position int, @nstring nchar(12);  
-- Initialize the current position variable to the first character in   
-- the string.  
SET @position = 1;  
-- Initialize the character string variable to the string to process.   
-- Notice that there is an N before the start of the string, which   
-- indicates that the data following the N is Unicode data.  
SET @nstring = N'Åkergatan 24';  
-- Print the character number of the position of the string you are at,   
-- the actual Unicode character you are processing, and the UNICODE   
-- value for this particular character.  
PRINT 'Character #' + ' ' + 'Unicode Character' + ' ' + 'UNICODE Value';  
WHILE @position <= DATALENGTH(@nstring)  
-- While these are still characters in the character string,  
   BEGIN;  
   SELECT @position,   
      CONVERT(char(17), SUBSTRING(@nstring, @position, 1)),  
      UNICODE(SUBSTRING(@nstring, @position, 1));  
   SELECT @position = @position + 1;  
   END;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Character # Unicode Character UNICODE Value  
  
----------- ----------------- -----------   
1           Å                 197           
  
----------- ----------------- -----------   
2           k                 107           
  
----------- ----------------- -----------   
3           e                 101           
  
----------- ----------------- -----------   
4           r                 114           
  
----------- ----------------- -----------   
5           g                 103           
  
----------- ----------------- -----------   
6           a                 97            
  
----------- ----------------- -----------   
7           t                 116           
  
----------- ----------------- -----------   
8           a                 97            
  
----------- ----------------- -----------   
9           n                 110           
  
----------- ----------------- -----------   
10                            32            
  
----------- ----------------- -----------   
11          2                 50            
  
----------- ----------------- -----------   
12          4                 52  
```  
  
## <a name="see-also"></a>Vea también  
 [NCHAR &#40; Transact-SQL &#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  


