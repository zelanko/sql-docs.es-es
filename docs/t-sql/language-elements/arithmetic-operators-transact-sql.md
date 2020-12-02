---
description: Operadores aritméticos (Transact-SQL)
title: Operadores aritméticos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], arithmetic
- arithmetic operators
- math operations [Transact-SQL]
ms.assetid: a41b92a5-1061-4e4d-bb3b-a180b73c88fa
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b51c473bb75f3f2e1c82f96dcd8af743597678fc
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124546"
---
# <a name="arithmetic-operators-transact-sql"></a>Operadores aritméticos (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Los operadores aritméticos ejecutan operaciones matemáticas con dos expresiones de uno o varios tipos de datos. Se ejecutan en la categoría de tipos de datos numéricos. Para obtener más información sobre las categorías de tipos de datos, vea [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
|Operator|Significado|  
|--------------|-------------|  
|[+ (Sumar)](../../t-sql/language-elements/add-transact-sql.md)|Suma|  
|[- (Restar)](../../t-sql/language-elements/subtract-transact-sql.md)|Resta|  
|[* (Multiplicar)](../../t-sql/language-elements/multiply-transact-sql.md)|Multiplicación|  
|[/ (Dividir)](../../t-sql/language-elements/divide-transact-sql.md)|División|  
|[% (Módulo)](../../t-sql/language-elements/modulo-transact-sql.md)|Devuelve el resto entero de una división. Por ejemplo, 12 % 5 = 2 porque el resto de 12 dividido entre 5 es 2.|  
  
También se pueden usar los operadores más (+) y menos (-) para ejecutar operaciones aritméticas sobre valores **datetime** y **smalldatetime**.  
  
Para obtener más información sobre la precisión y la escala del resultado de una operación aritmética, vea [Precisión, escala y longitud &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
## <a name="see-also"></a>Consulte también  
[Funciones matemáticas &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
[Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
