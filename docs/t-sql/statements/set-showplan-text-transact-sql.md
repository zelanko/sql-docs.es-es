---
title: SET SHOWPLAN_TEXT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SHOWPLAN_TEXT
- SET_SHOWPLAN_TEXT_TSQL
- SET SHOWPLAN_TEXT
- SHOWPLAN_TEXT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_TEXT statement
- canceling statement execution
- SHOWPLAN_TEXT option
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: 2c4f3fc8-ff2c-4790-8b74-e7e8ef58f9a6
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7abd42acdcbfa4274686d3d8162e727cf36e5ee7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-showplantext-transact-sql"></a>SET SHOWPLAN_TEXT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Hace que Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ejecute instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. En su lugar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve información detallada sobre el modo en que se ejecutan las instrucciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET SHOWPLAN_TEXT { ON | OFF }  
```  
  
## <a name="remarks"></a>Comentarios  
 La opción SET SHOWPLAN_TEXT se establece en tiempo de ejecución, no en tiempo de análisis.  
  
 Cuando SET SHOWPLAN_TEXT es ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve información acerca de la ejecución de cada instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)], sin ejecutarla. Cuando esta opción está establecida en ON, se devuelve información acerca del plan de ejecución de todas las instrucciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siguientes hasta que se vuelve a establecer en OFF. Por ejemplo, si se ejecuta una instrucción CREATE TABLE cuando SET SHOWPLAN_TEXT es ON y después se ejecuta una instrucción SELECT en la que se especifica la tabla creada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un mensaje de error en el que se indica que la tabla especificada no existe. Por ello, las referencias posteriores que se hagan a la tabla generarán un error. Cuando SET SHOWPLAN_TEXT está establecida en OFF, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta las instrucciones sin generar ningún informe con información del plan de ejecución.  
  
 SET SHOWPLAN_TEXT está diseñada para devolver una salida legible para las aplicaciones Microsoft Win32 del símbolo del sistema, como el **osql** utilidad. SET SHOWPLAN_ALL devuelve información más detallada, destinada a los programas diseñados para tratarla.  
  
 SET SHOWPLAN_TEXT y SET SHOWPLAN_ALL no se pueden especificar en un procedimiento almacenado. Deben ser las únicas instrucciones de un lote.  
  
 SET SHOWPLAN_TEXT devuelve la información como un conjunto de filas en forma de árbol jerárquico que representa los pasos que sigue el procesador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al ejecutar cada instrucción. Cada instrucción reflejada en la salida contiene una fila con el texto de la instrucción, seguida de varias filas con los detalles de los pasos de su ejecución. La tabla muestra la columna que contiene la salida.  
  
|Nombre de columna|Description|  
|-----------------|-----------------|  
|**StmtText**|Para las filas que no son de tipo PLAN_ROW, esta columna contiene el texto de la [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción. En las filas de tipo PLAN_ROW, esta columna contiene una descripción de la operación. Esta columna contiene el operador físico y, opcionalmente, puede contener también el operador lógico. Esta columna también puede ir seguida de una descripción que viene determinada por el operador físico. Para obtener más información acerca de los operadores físicos, consulte la **argumento** columna [SET SHOWPLAN_ALL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-showplan-all-transact-sql.md).|  
  
 Para obtener más información acerca de los operadores físicos y lógicos que se pueden ver en la salida de Showplan, vea [Showplan lógicos y físicos de los operadores de referencia](../../relational-databases/showplan-logical-and-physical-operators-reference.md)  
  
## <a name="permissions"></a>Permissions  
 Para utilizar SET SHOWPLAN_TEXT, debe disponer de permisos suficientes para ejecutar las instrucciones en las que se ejecuta SET SHOWPLAN_TEXT, y debe tener el permiso SHOWPLAN para todas las bases de datos que contengan objetos a los que se hace referencia.  
  
 Para SELECT, INSERT, UPDATE, DELETE, EXEC *stored_procedure*y EXEC *user_defined_function* instrucciones para generar un plan de presentación que el usuario debe:  
  
-   Tener los permisos correspondientes para ejecutar las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Tener el permiso SHOWPLAN en todas las bases de datos que contengan objetos a los que hacen referencia las instrucciones Transact-SQL, como tablas, vistas, etc.  
  
 Para todas las demás instrucciones, como DDL, USE *database_name*, conjunto, DECLARE, SQL dinámica y así sucesivamente, solo los permisos adecuados para ejecutar el [!INCLUDE[tsql](../../includes/tsql-md.md)] son necesarias las instrucciones.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra la forma en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza los índices al procesar las instrucciones.  
  
 Ésta es la consulta que utiliza un índice:  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
StmtText                                             
---------------------------------------------------  
SELECT *  
FROM Production.Product   
WHERE ProductID = 905;   
  
StmtText                                                                                                                                                                                        
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Seek(OBJECT:([AdventureWorks2012].[Production].[Product].[PK_Product_ProductID]), SEEK:([AdventureWorks2012].[Production].[Product].[ProductID]=CONVERT_IMPLICIT(int,[@1],0)) ORDERED FORWARD)   
```  
  
 Ésta es la consulta que no utiliza un índice:  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_TEXT ON;  
GO  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET SHOWPLAN_TEXT OFF;  
GO  
```  
  
 El conjunto de resultados es:  
  
```  
StmtText                                                                  
------------------------------------------------------------------------  
SELECT *  
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;   
  
StmtText                                                                                                                                                                                                  
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
|--Clustered Index Scan(OBJECT:([AdventureWorks2012].[Production].[ProductCostHistory].[PK_ProductCostHistory_ProductCostID]), WHERE:([AdventureWorks2012].[Production].[ProductCostHistory].[StandardCost]<[@1]))  
```  
  
## <a name="see-also"></a>Vea también  
 [Operadores &#40; Transact-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)  
  
  

