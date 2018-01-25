---
title: Seleccione @local_variable (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- variable_TSQL
- '@loca_variable'
- '@local'
- variable
- '@loca_variable_TSQL'
- '@local_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- variables [SQL Server], assigning
- SELECT statement [SQL Server], @local_variable
- '@local_variable'
- local variables [SQL Server]
ms.assetid: 8e1a9387-2c5d-4e51-a1fd-a2a95f026d6f
caps.latest.revision: "32"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 44fd55346e8a4a27f1d3301d6cb3c6bdf7bdf548
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="select-localvariable-transact-sql"></a>Seleccione @local_variable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Establece una variable local en el valor de una expresión.  
  
 Para asignar variables, recomendamos que use [establecer @local_variable ](../../t-sql/language-elements/set-local-variable-transact-sql.md) en lugar de SELECT @*local_variable*.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SELECT { @local_variable { = | += | -= | *= | /= | %= | &= | ^= | |= } expression } 
    [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
@*local_variable*  
 Es una variable declarada a la que se va a asignar un valor.  
  
{= | += | -= | \*= | /= | %= | &= | ^= | |= }   
Asigna el valor de la derecha a la variable de la izquierda.  
  
Operador de asignación compuesta:  
  |operador |action |   
  |-----|-----|  
  | = | La expresión siguiente, se asigna a la variable. |  
  | += | Agregar y asignar |   
  | -= | Restar y asignar |  
  | \*= | Multiplicar y asignar |  
  | /= | Dividir y asignar |  
  | %= | Módulo y asignar |  
  | &= | AND bit a bit y asignar |  
  | ^= | Bit a bit XOR y asignar |  
  | \|= | OR bit a bit y asignar |  
  
 *expression*  
 Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md). Esto incluye una subconsulta escalar.  
  
## <a name="remarks"></a>Comentarios  
 SELECT @*local_variable* normalmente se utiliza para devolver un valor único en la variable. Sin embargo, cuando *expresión* es el nombre de una columna, puede devolver varios valores. Si la instrucción SELECT devuelve más de un valor, se asigna a la variable el último valor devuelto.  
  
 Si la instrucción SELECT no devuelve filas, la variable mantiene su valor actual. Si *expresión* es una subconsulta escalar que no devuelve ningún valor, la variable se establece en NULL.  
  
 Una instrucción SELECT puede inicializar varias variables locales.  
  
> [!NOTE]  
>  Una instrucción SELECT que contenga una asignación de variable no se puede utilizar para realizar operaciones típicas de obtención de conjuntos de resultados.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-use-select-localvariable-to-return-a-single-value"></a>A. Utilizar instrucciones SELECT @local_variable para devolver un solo valor  
 En el siguiente ejemplo, se asigna el valor `@var1` a la variable `Generic Name`. La consulta realizada en la tabla `Store` no devuelve filas debido a que el valor especificado en `CustomerID` no existe en la tabla. La variable mantiene el valor `Generic Name`.  
  
```sql  
-- Uses AdventureWorks    
  
DECLARE @var1 varchar(30);         
SELECT @var1 = 'Generic Name';         
SELECT @var1 = Name         
FROM Sales.Store         
WHERE CustomerID = 1000 ;        
SELECT @var1 AS 'Company Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Company Name  
 ------------------------------  
 Generic Name  
 ```  
  
### <a name="b-use-select-localvariable-to-return-null"></a>B. Utilizar instrucciones SELECT @local_variable para devolver un valor nulo  
 En el siguiente ejemplo, se utiliza una subconsulta para asignar un valor a `@var1`. Debido a que el valor solicitado para `CustomerID` no existe, la subconsulta no devuelve ningún valor y la variable se establece en `NULL`.  
  
```sql  
-- Uses AdventureWorks  
  
DECLARE @var1 varchar(30)   
SELECT @var1 = 'Generic Name'   
SELECT @var1 = (SELECT Name   
FROM Sales.Store   
WHERE CustomerID = 1000)   
SELECT @var1 AS 'Company Name' ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Company Name  
----------------------------  
NULL  
```  
  
## <a name="see-also"></a>Vea también  
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [Compuesta operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
