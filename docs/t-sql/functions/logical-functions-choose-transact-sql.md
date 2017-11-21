---
title: Elija (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHOOSE
- CHOOSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHOOSE function
ms.assetid: 1c382c83-7500-4bae-bbdc-c1dbebd3d83f
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bbc1dbe9a41bcd256da27b04f56f98b863ed7394
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="logical-functions---choose-transact-sql"></a>Funciones lógicas - elija (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve el elemento en el índice especificado de una lista de valores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CHOOSE ( index, val_1, val_2 [, val_n ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *índice*  
 Expresión entera que representa un índice de base uno de la lista de elementos que le siguen.  
  
 Si el valor de índice proporcionado tiene un tipo de datos numérico distinto de **int**, a continuación, el valor se convierte implícitamente en un entero. Si el valor de índice supera los límites de la matriz de valores, CHOOSE devuelve NULL.  
  
 *val_1... val_n*  
 Lista de valores separados por comas de cualquier tipo de datos.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve el tipo de datos con la mayor prioridad del conjunto de tipos pasados a la función. Para obtener más información, vea [Prioridad de tipo de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 CHOOSE actúa como un índice de una matriz, donde la matriz consta de los argumentos que siguen al argumento de índice. El argumento de índice determina cuál de los valores siguientes se devolverá.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve el tercer elemento de la lista de valores que se proporciona.  
  
```  
SELECT CHOOSE ( 3, 'Manager', 'Director', 'Developer', 'Tester' ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
-------------  
Developer  
  
(1 row(s) affected)  
```  
  
 En el ejemplo siguiente se devuelve una cadena de caracteres simple basada en el valor de la columna `ProductCategoryID`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductCategoryID, CHOOSE (ProductCategoryID, 'A','B','C','D','E') AS Expression1  
FROM Production.ProductCategory;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ProductCategoryID Expression1  
----------------- -----------  
3                 C  
1                 A  
2                 B  
4                 D  
  
(4 row(s) affected)  
  
```  
  
 En el ejemplo siguiente se devuelve el trimestre en el que se contrató a un empleado. La función MONTH se usa para devolver el valor de mes de la columna `HireDate`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT JobTitle, HireDate, CHOOSE(MONTH(HireDate),'Winter','Winter', 'Spring','Spring','Spring','Summer','Summer',   
                                                  'Summer','Autumn','Autumn','Autumn','Winter') AS Quarter_Hired  
FROM HumanResources.Employee  
WHERE  YEAR(HireDate) > 2005  
ORDER BY YEAR(HireDate);  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
JobTitle                                           HireDate   Quarter_Hired  
-------------------------------------------------- ---------- -------------  
Sales Representative                               2006-11-01 Autumn  
European Sales Manager                             2006-05-18 Spring  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2006-07-01 Summer  
Sales Representative                               2007-07-01 Summer  
Pacific Sales Manager                              2007-04-15 Spring  
Sales Representative                               2007-07-01 Summer  
  
```  
  
## <a name="see-also"></a>Vea también  
 [IIF &#40; Transact-SQL &#41;](../../t-sql/functions/logical-functions-iif-transact-sql.md)  
  
  

