---
title: SOUNDEX (Transact-SQL) | Documentos de Microsoft
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
- SOUNDEX
- SOUNDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SOUNDEX function
- comparing string data
- strings [SQL Server], similarity
- strings [SQL Server], comparing
- SOUNDEX values
ms.assetid: 8f1ed34e-8467-4512-a211-e0f43dee6584
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ec170c756fd207c648e210de15df9d18024ea718
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="soundex-transact-sql"></a>SOUNDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un código de cuatro caracteres (SOUNDEX) para evaluar la semejanza de dos cadenas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SOUNDEX ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es un carácter alfanumérico [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de datos de caracteres. *character_expression* puede ser una constante, variable o columna.  
  
## <a name="return-types"></a>Tipos devueltos  
 **varchar**  
  
## <a name="remarks"></a>Comentarios  
 SOUNDEX convierte una cadena alfanumérica en un código de cuatro caracteres que se basa en cómo suena la cadena cuando se pronuncia. El primer carácter del código es el primer carácter de *character_expression*, convertido a mayúsculas. Los caracteres segundo a cuarto del código son números que representan las letras de la expresión. Las letras A, E, I, O, U, H, W e Y se omiten a menos que sean la primera letra de la cadena. Se agregan ceros al final si se necesita crear un código de cuatro caracteres. Para obtener más información sobre el código SOUNDEX, vea [el sistema de indización Soundex](https://www.archives.gov/research/census/soundex.html).  
  
 Se pueden comparar códigos SOUNDEX de distintas cadenas para ver la similitud de las cadenas cuando se pronuncian. La función DIFFERENCE realiza una operación SOUNDEX en dos cadenas y devuelve un entero que representa la similitud de los códigos SOUNDEX para esas cadenas.  
  
 SOUNDEX distingue la intercalación. Las funciones de cadena se pueden anidar.  
  
## <a name="soundex-compatibility"></a>Compatibilidad con SOUNDEX  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la función SOUNDEX aplicaba un subconjunto de las reglas de SOUNDEX. En el nivel de compatibilidad de base de datos 110 o posterior, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica un conjunto de reglas más completo.  
  
 Después de actualizar al nivel de compatibilidad 110 o posterior, es posible que tenga que regenerar los índices, los montones o las restricciones CHECK que usan la función SOUNDEX.  
  
-   Un montón que contiene una columna computada persistida definida con SOUNDEX no puede ser consultada hasta que el montón sea reconstruido ejecutando la declaración`ALTER TABLE <table> REBUILD`.  
  
-   Las restricciones CHECK definidas con SOUNDEX son deshabilitadas tras una actualización. Para permitir la restricción, ejecute la declaración`ALTER TABLE <table> WITH CHECK CHECK CONSTRAINT ALL`.  
  
-   Los índices (incluyendo las vistas indizadas) que contienen una columna computada persistida definida con SOUNDEX no pueden ser consultados hasta que el índice sea reconstruido ejecutando la declaración`ALTER INDEX ALL ON <object> REBUILD`.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente muestra la función SOUNDEX y la función relacionada DIFFERENCE. En el primer ejemplo se obtienen los valores estándar de `SOUNDEX` para todas las consonantes. Al usar `SOUNDEX` para las cadenas `Smith` y `Smythe` se obtiene el mismo resultado, ya que todas las vocales, la letra `y`, las letras duplicadas y la letra `h` no se incluyen.  
  
```  
-- Using SOUNDEX  
SELECT SOUNDEX ('Smith'), SOUNDEX ('Smythe');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]Válido para una intercalación Latin1_General.  
  
```  
  
----- -----   
S530  S530    
  
(1 row(s) affected)  
```  
  
 La función `DIFFERENCE` compara la diferencia entre los resultados del modelo `SOUNDEX`. El siguiente ejemplo muestra dos cadenas que solo difieren en las vocales. La diferencia obtenida es `4`, la mínima posible.  
  
```  
-- Using DIFFERENCE  
SELECT DIFFERENCE('Smithers', 'Smythers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]Válido para una intercalación Latin1_General.  
  
```  
-----------   
4             
  
(1 row(s) affected)  
```  
  
 En el ejemplo siguiente, las cadenas varían en las consonantes; por tanto, la diferencia obtenida es `2`, la máxima posible.  
  
```  
SELECT DIFFERENCE('Anothers', 'Brothers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]Válido para una intercalación Latin1_General.  
  
```  
-----------   
2             
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 El ejemplo siguiente muestra la función SOUNDEX y la función relacionada DIFFERENCE. En el primer ejemplo se obtienen los valores estándar de `SOUNDEX` para todas las consonantes. Al usar `SOUNDEX` para las cadenas `Smith` y `Smythe` se obtiene el mismo resultado, ya que todas las vocales, la letra `y`, las letras duplicadas y la letra `h` no se incluyen.  
  
```  
-- Using SOUNDEX  
SELECT SOUNDEX ('Smith'), SOUNDEX ('Smythe');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]Válido para una intercalación Latin1_General.  
  
```  
  
----- -----   
S530  S530    
  
(1 row(s) affected)  
```  
  
 La función `DIFFERENCE` compara la diferencia entre los resultados del modelo `SOUNDEX`. El siguiente ejemplo muestra dos cadenas que solo difieren en las vocales. La diferencia obtenida es `4`, la mínima posible.  
  
```  
-- Using DIFFERENCE  
SELECT DIFFERENCE('Smithers', 'Smythers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]Válido para una intercalación Latin1_General.  
  
```  
-----------   
4             
  
(1 row(s) affected)  
```  
  
 En el ejemplo siguiente, las cadenas varían en las consonantes; por tanto, la diferencia obtenida es `2`, la máxima posible.  
  
```  
SELECT DIFFERENCE('Anothers', 'Brothers');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]Válido para una intercalación Latin1_General.  
  
```  
-----------   
2             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [DIFERENCIA &#40; Transact-SQL &#41;](../../t-sql/functions/difference-transact-sql.md)   
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  


