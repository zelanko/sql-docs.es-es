---
title: ISNUMERIC (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISNUMERIC
- ISNUMERIC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], valid numeric type
- numeric data
- ISNUMERIC function
- verifying valid numeric type
- valid numeric type [SQL Server]
- checking valid numeric type
ms.assetid: 7aa816de-529a-4f6c-a99f-4d5a9ef599eb
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3a993fed6ec04a033586feec02afb1a84b983e6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="isnumeric-transact-sql"></a>ISNUMERIC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Determina si una expresión es un tipo numérico válido.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ISNUMERIC ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es el [expresión](../../t-sql/language-elements/expressions-transact-sql.md) que se debe evaluar.  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 ISNUMERIC devuelve 1 cuando la expresión de entrada se evalúa para un tipo de datos numérico válido; de lo contrario, devuelve 0. Entre los tipos de datos numéricos válidos se encuentran los siguientes:  
  
|||  
|-|-|  
|**int**|**numeric**|  
|**bigint**|**money**|  
|**smallint**|**smallmoney**|  
|**tinyint**|**float**|  
|**decimal**|**real**|  
  
> [!NOTE]  
>  ISNUMERIC devuelve 1 para algunos caracteres que no son números, como el signo más (+), menos (-) y símbolos de moneda válidos, como el signo de dólar ($). Para obtener una lista completa de símbolos de moneda, vea [money y smallmoney &#40; Transact-SQL &#41; ](../../t-sql/data-types/money-and-smallmoney-transact-sql.md).  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo utiliza `ISNUMERIC` para devolver todos los códigos postales que no son valores numéricos.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, PostalCode  
FROM Person.Address   
WHERE ISNUMERIC(PostalCode)<> 1;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 El siguiente ejemplo utiliza `ISNUMERIC` para devolver todos los códigos postales que no son valores numéricos.  
  
```  
USE master;  
GO  
SELECT name, isnumeric(name) AS IsNameANumber, database_id, isnumeric(database_id) AS IsIdANumber   
FROM sys.databases;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40; Transact-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  


