---
title: SIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SIN_TSQL
- SIN
dev_langs:
- TSQL
helpviewer_keywords:
- SIN function
- sine
ms.assetid: bc1781e9-185f-4981-929b-e77371be6b26
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 08463a1014a6226b12fa652e9bffb54782050289
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907120"
---
# <a name="sin-transact-sql"></a>SIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el seno trigonométrico del ángulo dado, en radianes, en una expresión **float** numérica aproximada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SIN ( float_expression )  
```  
  

## <a name="arguments"></a>Argumentos  
 *float_expression*  
 Es una [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de tipo **float** o de un tipo que se puede convertir en float de manera implícita.  
  
## <a name="return-types"></a>Tipos devueltos  
 **float**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se calcula el seno de un ángulo especificado.  
  
```  
DECLARE @angle float;  
SET @angle = 45.175643;  
SELECT 'The SIN of the angle is: ' + CONVERT(varchar,SIN(@angle));  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
The SIN of the angle is: 0.929607                         
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo se calcula el seno de un ángulo especificado.  
  
```  
SELECT SIN(45.175643);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
---------  
0.929607
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

