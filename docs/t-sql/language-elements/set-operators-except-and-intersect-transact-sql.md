---
title: EXCEPT e INTERSECT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INTERSECT_TSQL
- EXCEPT_TSQL
- INTERSECT
- EXCEPT
dev_langs: TSQL
helpviewer_keywords:
- EXCEPT operator [Transact-SQL]
- queries [SQL Server], comparing
- comparing queries
- INTERSECT operator
ms.assetid: b1019300-171a-4a1a-854f-e1e751de3565
caps.latest.revision: "39"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 706aeaab949399ab6d235a368fa354c32cc54d98
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="set-operators---except-and-intersect-transact-sql"></a>Juego de operadores - EXCEPT e INTERSECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve filas distintas al comparar los resultados de dos consultas.  
  
 EXCEPT devuelve filas distintas de la consulta de entrada izquierda que no son de salida en la consulta de entrada derecha.  
  
 INTERSECT devuelve filas distintas que se generan mediante el operador de consultas de entrada izquierdo y derecho.  
  
 Las reglas básicas para combinar los conjuntos de resultados de dos consultas que utilizan EXCEPT o INTERSECT son las siguientes:   
  
-   El número y el orden de las columnas debe ser el mismo en todas las consultas.  
  
-   Los tipos de datos deben ser compatibles.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
{ <query_specification> | ( <query_expression> ) }   
{ EXCEPT | INTERSECT }  
{ <query_specification> | ( <query_expression> ) }  
```  
  
## <a name="arguments"></a>Argumentos  
 \<*query_specification*> | ( \<*query_expression*> )  
 Es una especificación o expresión de consulta que devuelve datos que se van a comparar con los de otra especificación o expresión de consulta. No es preciso que las definiciones de las columnas que forman parte de una operación EXCEPT o INTERSECT sean idénticas, pero deben ser comparables por medio de una conversión implícita. Cuando los tipos de datos difieren, el tipo que se utiliza para realizar la comparación y devolver resultados se determina según las reglas para [prioridad de tipo de datos](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
 Cuando los tipos son los mismos pero varían en cuanto a precisión, escala o longitud, el resultado se determina según las mismas reglas para combinar expresiones. Para más información, vea [Precisión, escala y longitud &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
 La especificación de consulta o la expresión no puede devolver **xml**, **texto**, **ntext**, **imagen**, o columnas de tipo definido por el usuario CLR no binarios Dado que estos tipos de datos no son comparables.  
  
 EXCEPT  
 Devuelve los valores distintos de la consulta a la izquierda del operador EXCEPT, que tampoco se devuelven desde la consulta derecha.  
  
 INTERSECT  
 Devuelve los valores distintos devueltos por las consultas situadas a los lados izquierdo y derecho del operador INTERSECT.  
  
## <a name="remarks"></a>Comentarios  
 Cuando los tipos de datos de columnas comparables devuelven por las consultas a la izquierda y derecha de la EXCEPT o INTERSECT operadores son tipos de datos de caracteres con intercalaciones diferentes, la comparación requerida se realiza según las reglas de [ precedencia de intercalación](../../t-sql/statements/collation-precedence-transact-sql.md). Si no es posible realizar esta conversión, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] devuelve un error.  
  
 Cuando se comparan los valores de columna para determinar filas DISTINCT, dos valores NULL se consideran equivalentes.  
  
 Los nombres de columna del conjunto de resultados devueltos por EXCEPT o INTERSECT son los mismos que han sido devueltos por la consulta situada en el lado izquierdo del operador.  
  
 Los nombres o alias de columna de las cláusulas ORDER BY deben hacer referencia a los nombres de columna devueltos por la consulta del lado izquierdo.  
  
 La nulabilidad de cualquier columna del conjunto de resultados devueltos por EXCEPT o INTERSECT es la misma que la de la columna correspondiente devuelta por la consulta situada en el lado izquierdo del operador.  
  
 Si EXCEPT o INTERSECT se utilizan con otros operadores en una expresión, ésta se evalúa en el contexto de la siguiente prioridad:  
  
1.  Expresiones entre paréntesis  
  
2.  El operador INTERSECT  
  
3.  EXCEPT y UNION se evalúan de izquierda a derecha según su posición en la expresión  
  
 Si EXCEPT o INTERSECT se utilizan para comparar más de dos conjuntos de consultas, la conversión del tipo de datos se determina al comparar dos consultas a la vez y mediante las reglas mencionadas de evaluación de expresiones.  
  
 EXCEPT e INTERSECT no se pueden usar en definiciones de vistas distribuidas con particiones ni en notificaciones de consultas.  
  
 EXCEPT e INTERSECT se pueden utilizar en consultas distribuidas, pero solo se ejecutan en el servidor local y no se insertan en el servidor vinculado. Por lo tanto, el uso de EXCEPT e INTERSECT en consultas distribuidas puede afectar al rendimiento.  
  
 Los cursores de solo avance rápido o estáticos son completamente compatibles con el conjunto de resultados si se utilizan con una operación EXCEPT o INTERSECT. Si un cursor controlado por conjunto de claves o dinámico se utiliza con una operación EXCEPT o INTERSECT, el cursor del conjunto de resultados de la operación se convierte en un cursor estático.  
  
 Cuando una operación EXCEPT se muestra mediante la característica de plan de presentación gráfico de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], la operación aparece como un [deja Antisemicombinación](../../relational-databases/showplan-logical-and-physical-operators-reference.md), y una operación INTERSECT aparece como un [Semicombinación izquierda](../../relational-databases/showplan-logical-and-physical-operators-reference.md).  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran el uso de la `INTERSECT` y `EXCEPT` operadores. La primera consulta devuelve todos los valores de la tabla `Production.Product` para comparar los resultados con `INTERSECT` y `EXCEPT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product ;  
--Result: 504 Rows  
```  
  
 La siguiente consulta devuelve los valores distintos devueltos por las consultas situadas a los lados izquierdo y derecho del operador `INTERSECT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
INTERSECT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 238 Rows (products that have work orders)  
```  
  
 La siguiente consulta devuelve los valores distintos de la consulta situados a la izquierda del operador `EXCEPT` que no se encuentran en la consulta derecha.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.Product  
EXCEPT  
SELECT ProductID   
FROM Production.WorkOrder ;  
--Result: 266 Rows (products without work orders)  
```  
  
 La siguiente consulta devuelve los valores distintos de la consulta situados a la izquierda del operador `EXCEPT` que no se encuentran en la consulta derecha. Las tablas se invierten respecto al ejemplo anterior.  
  
```  
-- Uses AdventureWorks  
  
SELECT ProductID   
FROM Production.WorkOrder  
EXCEPT  
SELECT ProductID   
FROM Production.Product ;  
--Result: 0 Rows (work orders without products)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En los siguientes ejemplos se muestra el modo de usar los operadores `INTERSECT` y `EXCEPT`. La primera consulta devuelve todos los valores de la tabla `FactInternetSales` para comparar los resultados con `INTERSECT` y `EXCEPT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales;  
--Result: 60398 Rows  
```  
  
 La siguiente consulta devuelve los valores distintos devueltos por las consultas situadas a los lados izquierdo y derecho del operador `INTERSECT`.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
INTERSECT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9133 Rows (Sales to customers that are female.)  
```  
  
 La siguiente consulta devuelve los valores distintos de la consulta situados a la izquierda del operador `EXCEPT` que no se encuentran en la consulta derecha.  
  
```  
-- Uses AdventureWorks  
  
SELECT CustomerKey   
FROM FactInternetSales    
EXCEPT   
SELECT CustomerKey   
FROM DimCustomer   
WHERE DimCustomer.Gender = 'F'  
ORDER BY CustomerKey;  
--Result: 9351 Rows (Sales to customers that are not female.)  
```  
  
  

