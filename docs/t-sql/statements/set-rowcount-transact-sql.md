---
title: SET ROWCOUNT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_ROWCOUNT_TSQL
- ROWCOUNT_TSQL
- SET ROWCOUNT
- ROWCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- row return limitations [SQL Server]
- SET ROWCOUNT statement
- number of rows affected by statement
- ROWCOUNT option
- counting rows
- stopping queries
- limiting rows returned
- queries [SQL Server], stopping
ms.assetid: c6966fb7-6421-47ef-98f3-82351f2f6bdc
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eda7f9faf2bb45b06cf1112dbe48cbdb281fdab3
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-rowcount-transact-sql"></a>SET ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detenga el procesamiento de la consulta una vez que se han devuelto las filas especificadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
SET ROWCOUNT { number | @number_var }   
```  
  
## <a name="arguments"></a>Argumentos  
 *número* | @*number_var*  
 Es el número entero de filas que se deben procesar antes de detener la consulta específica.  
  
## <a name="remarks"></a>Comentarios  
  
> [!IMPORTANT]  
>  La utilización de SET ROWCOUNT no afectará a las instrucciones DELETE, INSERT ni UPDATE en una futura versión de SQL Server. Evite utilizar SET ROWCOUNT con las instrucciones DELETE, INSERT y UPDATE en los nuevos trabajos de desarrollo, y modifique las aplicaciones que la utilizan en la actualidad. Para conseguir un comportamiento similar, utilice la sintaxis TOP. Para obtener más información, vea [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 Para desactivar esta opción con el fin de que se devuelvan todas las filas, especifique SET ROWCOUNT 0.  
  
 Al establecer la opción SET ROWCOUNT, la mayoría de las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] dejarán de procesarse cuando se haya alcanzado el número de filas especificado. Esto incluye a los desencadenadores. La opción ROWCOUNT no afecta a los cursores dinámicos, pero limita el conjunto de filas de los cursores controlados por conjunto de claves e INSENSITIVE. Esta opción debe utilizarse con cautela.  
  
 SET ROWCOUNT invalida la palabra clave TOP de la instrucción SELECT si el recuento de filas es el valor mínimo.  
  
 La opción SET ROWCOUNT se establece en tiempo de ejecución, no en tiempo de análisis.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
 SET ROWCOUNT detiene el procesamiento cuando se alcanza el número de filas especificado. En el ejemplo siguiente se observa que más de 500 filas cumplen los criterios de `Quantity` menor que `300`. Sin embargo, después de aplicar SET ROWCOUNT, se puede ver que no se devolvieron todas las filas.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT count(*) AS Count  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Count`  
  
 `-----------`  
  
 `537`  
  
 `(1 row(s) affected)`  
  
 Ahora, se establece `ROWCOUNT` en `4` y se devuelven todas las filas para mostrar que solo se devuelven 4 filas.  
  
```  
SET ROWCOUNT 4;  
SELECT *  
FROM Production.ProductInventory  
WHERE Quantity < 300;  
GO  
```  
  
 `(4 row(s) affected)`  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 SET ROWCOUNT detiene el procesamiento cuando se alcanza el número de filas especificado. En el ejemplo siguiente, tenga en cuenta que más de 20 filas cumplen los criterios de `AccountType = 'Assets'`. Sin embargo, después de aplicar SET ROWCOUNT, se puede ver que no se devolvieron todas las filas.  
  
```  
-- Uses AdventureWorks  
  
SET ROWCOUNT 5;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
 Para devolver todas las filas, establezca el número de filas en 0.  
  
```  
-- Uses AdventureWorks  
  
SET ROWCOUNT 0;  
SELECT * FROM [dbo].[DimAccount]  
WHERE AccountType = 'Assets';  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


