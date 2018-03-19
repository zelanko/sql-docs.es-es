---
title: "= (Operador de asignación) (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c21e0e9525a68c423cbf273d3a5a8ba3aa3da04a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="-assignment-operator-transact-sql"></a>= Operador de asignación (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all_md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  El signo igual (=) es el único operador de asignación de [!INCLUDE[tsql](../../includes/tsql-md.md)]. En el siguiente ejemplo se crea la variable `@MyCounter` y, a continuación, el operador de asignación define `@MyCounter` en un valor devuelto por una expresión.  
  
```  
DECLARE @MyCounter INT;  
SET @MyCounter = 1;  
```  
  
 El operador de asignación también se puede utilizar para establecer la relación entre un encabezado de columna y la expresión que define los valores para esa columna. El siguiente ejemplo muestra los encabezados de columna `FirstColumnHeading` y `SecondColumnHeading`. La cadena `xyz` se muestra en el encabezado de columna `FirstColumnHeading` para todas las filas. A continuación, cada Id. de producto de la tabla `Product` se enumera en el encabezado de columna `SecondColumnHeading`.  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstColumnHeading = 'xyz',  
       SecondColumnHeading = ProductID  
FROM Production.Product;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Operadores compuestos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [Expresiones &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
