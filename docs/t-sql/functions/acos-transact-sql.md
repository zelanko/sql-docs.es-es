---
description: ACOS (Transact-SQL)
title: ACOS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ACOS
- ACOS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cosine
- ACOS function
- arccosine
ms.assetid: 4ec6b46e-9438-4f0f-8b96-461edd84280a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7d40695c1f9edef75f66c93e9e7cc7f3c6e8769
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111180"
---
# <a name="acos-transact-sql"></a>ACOS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Una función que devuelve el ángulo, expresado en radianes, cuyo coseno es la expresión float especificada. También se denomina arcoseno.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
ACOS ( float_expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*float_expression*  
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) o bien de tipo **float** o bien de un tipo que se puede convierte en float de manera implícita. Solo se admite un valor comprendido entre -1,00 y 1,00. Con valores fuera de este intervalo se devuelve NULL, y ASIN notifica un error del dominio.
  
## <a name="return-types"></a>Tipos de valor devuelto  
**float**
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se devuelve el valor `ACOS` del número especificado.
  
```sql
SET NOCOUNT OFF;  
DECLARE @cos FLOAT;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(VARCHAR, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte también
[Funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Funciones](../../t-sql/functions/functions.md)
  
  

