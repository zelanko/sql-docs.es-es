---
title: FLOOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FLOOR_TSQL
- FLOOR
dev_langs:
- TSQL
helpviewer_keywords:
- integers [SQL Server]
- largest integers
- FLOOR function [Transact-SQL]
ms.assetid: 4f26c784-9240-491f-b854-754be3fccae4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2e366876c5b71f410f05b7ed4483347b1f754686
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "74249802"
---
# <a name="floor-transact-sql"></a>FLOOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el entero más grande que sea menor o igual que la expresión numérica especificada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
FLOOR ( numeric_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *numeric_expression*  
 Es una expresión de la categoría de tipos de datos numérico exacto o numérico aproximado, excepto para el tipo de datos **bit**.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Devuelve el mismo tipo que *numeric_expression*.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestran valores numéricos positivos, negativos y de moneda con la función `FLOOR`.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 El resultado es la parte entera del valor calculado en el mismo tipo de datos que *numeric_expression*.  
  
```  
---------      ---------     -----------  
123            -124          123.0000     
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo se muestran valores numéricos positivos y negativos con la función `FLOOR`.  
  
```  
SELECT FLOOR(123.45), FLOOR(-123.45), FLOOR($123.45);  
```  
  
 El resultado es la parte entera del valor calculado en el mismo tipo de datos que *numeric_expression*.  
  
 ```
 -----   ---------    -----------  
  
 123     -124         123
 ```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  

