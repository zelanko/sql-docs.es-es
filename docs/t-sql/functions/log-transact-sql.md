---
title: LOG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LOG
- LOG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- float expressions
- logarithm of expression
- LOG function
ms.assetid: f7c39511-cd84-4362-93ba-0d93655217ee
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d0acbc4f5244852f988047e9ec1798201fefc30e
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008822"
---
# <a name="log-transact-sql"></a>LOG (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Devuelve el logaritmo natural de la expresión **float** especificada en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
-- Syntax for SQL Server, Azure SQL Database  
  
LOG ( float_expression [, base ] )  
```  
  
```syntaxsql
-- Syntax for Azure Synapse SQL 
  
LOG ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *float_expression*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de tipo **float** o de un tipo que se puede convertir en **float** de manera implícita.  
  
 *base*  
 Argumento entero opcional que establece la base del logaritmo.  
  
**Válido para** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores.
  
## <a name="return-types"></a>Tipos de valor devuelto  
 **float**  
  
## <a name="remarks"></a>Observaciones  
 De forma predeterminada, **LOG()** devuelve el logaritmo natural. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede cambiar la base del logaritmo por otro valor mediante el parámetro *base* opcional.  
  
 El logaritmo natural es el logaritmo en base **e**, donde **e** es una constante irracional aproximadamente igual a 2,718281828.  
  
 El logaritmo natural del valor exponencial de un número es el propio número: LOG( EXP( *n* ) ) = *n*. Asimismo, el valor exponencial del logaritmo natural de un número es el propio número: EXP( LOG( *n* ) ) = *n*.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-calculating-the-logarithm-for-a-number"></a>A. Calcular el logaritmo de un número  
 En el ejemplo siguiente se calcula el `LOG` de la expresión **float** especificada.  
  
```  
DECLARE @var FLOAT = 10;  
SELECT 'The LOG of the variable is: ' + CONVERT(VARCHAR, LOG(@var));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------------------------  
The LOG of the variable is: 2.30259  
  
(1 row(s) affected)  
```  
  
### <a name="b-calculating-the-logarithm-of-the-exponent-of-a-number"></a>B. Calcular el logaritmo del exponente de un número  
 En el ejemplo siguiente se calcula el valor de `LOG` del exponente de un número.  
  
```  
SELECT LOG (EXP (10));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------------------------  
10  
(1 row(s) affected)  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-calculating-the-logarithm-for-a-number"></a>C. Calcular el logaritmo de un número  
 En el ejemplo siguiente se calcula el `LOG` de la expresión **float** especificada.  
  
```  
SELECT LOG(10);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ----------------`  
  
 2.30
 ```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [EXP &#40;Transact-SQL&#41;](../../t-sql/functions/exp-transact-sql.md)   
 [LOG10 &#40;Transact-SQL&#41;](../../t-sql/functions/log10-transact-sql.md)  
  
  

