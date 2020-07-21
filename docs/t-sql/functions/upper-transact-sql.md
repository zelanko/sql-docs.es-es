---
title: UPPER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- UPPER_TSQL
- UPPER
dev_langs:
- TSQL
helpviewer_keywords:
- UPPER function
- characters [SQL Server], lowercase
- converting lowercase to uppercase
- uppercase characters [SQL Server]
- characters [SQL Server], uppercase
- lowercase characters
ms.assetid: 5ced55f7-ac89-4cf2-9465-f63f4dc480db
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc6822f890ba66df1f2d7945e411a4cd334de1bc
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004075"
---
# <a name="upper-transact-sql"></a>UPPER (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Devuelve una expresión de caracteres con datos de caracteres en minúsculas convertidos a mayúsculas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
UPPER ( character_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de datos de caracteres. *character_expression* puede ser una constante, una variable o una columna de datos binarios o de caracteres.  
  
 *character_expression* debe ser de un tipo de datos que se pueda convertir implícitamente a **varchar**. De lo contrario, use [CAST](../../t-sql/functions/cast-and-convert-transact-sql.md) para convertir *character_expression* explícitamente.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **varchar** o **nvarchar**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utilizan las funciones `UPPER` y `RTRIM` para devolver el apellido de las personas de la tabla `dbo.DimEmployee` de manera que aparezca en mayúsculas, recortado y concatenado al nombre.  
  
```  
-- Uses AdventureWorks  
  
SELECT UPPER(RTRIM(LastName)) + ', ' + FirstName AS Name  
FROM dbo.DimEmployee  
ORDER BY LastName;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 ```
Name
------------------------------
ABBAS, Syed
ABERCROMBIE, Kim
ABOLROUS, Hazem
 ```  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
 [LOWER &#40;Transact-SQL&#41;](../../t-sql/functions/lower-transact-sql.md)  
  
  

