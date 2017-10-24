---
title: QUOTENAME (Transact-SQL) | Documentos de Microsoft
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
- QUOTENAME_TSQL
- QUOTENAME
dev_langs:
- TSQL
helpviewer_keywords:
- delimited identifiers [SQL Server]
- input strings [SQL Server]
- Unicode [SQL Server], delimited identifiers
- QUOTENAME function
- valid identifiers [SQL Server]
ms.assetid: 34d47f1e-2ac7-4890-8c9c-5f60f115e076
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7f4e40797fc49e8a70b01162fc6959ad60475e8b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="quotename-transact-sql"></a>QUOTENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una cadena Unicode con los delimitadores agregados para convertirla en un identificador delimitado válido de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
QUOTENAME ( 'character_string' [ , 'quote_character' ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 '*character_string*'  
 Es una cadena de datos de caracteres Unicode. *character_string* es **sysname** y está limitado a 128 caracteres. Las entradas mayores de 128 caracteres devuelven NULL.  
  
 '*quote_character*'  
 Es una cadena de un solo carácter que se utiliza como delimitador. Puede ser una comilla simple ( **'** ), un corchete izquierdo o derecho ( **[]** ), o un signo de comillas dobles ( **"** ). Si *quote_character* no se especifica, se utilizarán corchetes.  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar (258)**  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se toma la cadena de caracteres `abc[]def` y se utilizan los caracteres `[` y `]` para crear un identificador delimitado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido.  
  
```  
SELECT QUOTENAME('abc[]def');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc[]]def]  
  
(1 row(s) affected)  
```  
  
 Observe que el corchete derecho de la cadena `abc[]def` aparece dos veces para indicar que se trata de un carácter de escape.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo se toma la cadena de caracteres `abc def` y se utilizan los caracteres `[` y `]` para crear un identificador delimitado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] válido.  
  
```  
SELECT QUOTENAME('abc def');   
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
[abc def]  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de cadena &#40; Transact-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  


