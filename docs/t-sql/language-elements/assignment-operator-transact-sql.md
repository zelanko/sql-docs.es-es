---
description: = Operador de asignación (Transact-SQL)
title: = (Operador de asignación) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], assignment
- assignment operators [Transact-SQL]
- headings [SQL Server columns]
- relationships [SQL Server], assignment operators
- column headings [SQL Server]
ms.assetid: c3040db6-21d6-40ac-a783-82c98ec006cc
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9e7b83fe2e452d2f58f592d4af6958ce94786f13
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196852"
---
# <a name="-assignment-operator-transact-sql"></a>= Operador de asignación (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  El signo igual (=) es el único operador de asignación de [!INCLUDE[tsql](../../includes/tsql-md.md)]. En el siguiente ejemplo se crea la variable `@MyCounter` y, a continuación, el operador de asignación define `@MyCounter` en un valor devuelto por una expresión.  
  
```sql  
DECLARE @MyCounter INT;  
SET @MyCounter = 1;  
```  
  
 El operador de asignación también se puede utilizar para establecer la relación entre un encabezado de columna y la expresión que define los valores para esa columna. El siguiente ejemplo muestra los encabezados de columna `FirstColumnHeading` y `SecondColumnHeading`. La cadena `xyz` se muestra en el encabezado de columna `FirstColumnHeading` para todas las filas. A continuación, cada Id. de producto de la tabla `Product` se enumera en el encabezado de columna `SecondColumnHeading`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT FirstColumnHeading = 'xyz',  
       SecondColumnHeading = ProductID  
FROM Production.Product;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores compuestos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
