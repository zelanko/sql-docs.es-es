---
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 262b89b15100a5e79fba5626c4cf7cfc890ecaac
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65948229"
---
# <a name="acos-transact-sql"></a>ACOS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Una función que devuelve el ángulo, expresado en radianes, cuyo coseno es la expresión float especificada. También se denomina arcoseno.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
ACOS ( float_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*float_expression*  
Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) o bien de tipo **float** o bien de un tipo que se puede convierte en float de manera implícita. Solo se admite un valor comprendido entre -1,00 y 1,00. Con valores fuera de este intervalo se devuelve NULL, y ASIN notifica un error del dominio.
  
## <a name="return-types"></a>Tipos devueltos  
**float**
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se devuelve el valor `ACOS` del número especificado.
  
```sql
SET NOCOUNT OFF;  
DECLARE @cos float;  
SET @cos = -1.0;  
SELECT 'The ACOS of the number is: ' + CONVERT(varchar, ACOS(@cos));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------------   
The ACOS of the number is: 3.14159   
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Vea también
[Funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
[Funciones](../../t-sql/functions/functions.md)
  
  

