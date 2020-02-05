---
title: SOUNDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f0a8dd4c5faecc54b7d1c5a5d506fc7cf4ecd00
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67907075"
---
# <a name="soundex-transact-sql"></a>SOUNDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve un código de cuatro caracteres (SOUNDEX) para evaluar la semejanza de dos cadenas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SOUNDEX ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) alfanumérica de datos de caracteres. *character_expression* puede ser una constante, una variable o una columna.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **varchar**  
  
## <a name="remarks"></a>Observaciones  
 SOUNDEX convierte una cadena alfanumérica en un código de cuatro caracteres que se basa en cómo suena la cadena cuando se pronuncia. El primer carácter del código es el primer carácter de *character_expression*, convertido a mayúsculas. Los caracteres segundo a cuarto del código son números que representan las letras de la expresión. Las letras A, E, I, O, U, H, W e Y se omiten a menos que sean la primera letra de la cadena. Se agregan ceros al final si se necesita crear un código de cuatro caracteres. Para más información sobre el código SOUNDEX, vea [The Soundex Indexing System](https://www.archives.gov/research/census/soundex.html) (Sistema de indización Soundex).  
  
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
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Válido para una intercalación Latin1_General.  
  
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
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Válido para una intercalación Latin1_General.  
  
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
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Válido para una intercalación Latin1_General.  
  
```  
-----------   
2             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte también  
 [DIFFERENCE &#40;Transact-SQL&#41;](../../t-sql/functions/difference-transact-sql.md)   
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
  
  

