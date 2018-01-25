---
title: DBCC CHECKCONSTRAINTS (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC CHECKCONSTRAINTS
- DBCC_CHECKCONSTRAINTS_TSQL
- CHECKCONSTRAINTS
- CHECKCONSTRAINTS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- DBCC CHECKCONSTRAINTS statement
- consistency [SQL Server], constraints
- checking constraint consistency
- constraints [SQL Server], consistency checks
- integrity [SQL Server], constraints
ms.assetid: da6c9cee-6687-46e8-b504-738551f9068b
caps.latest.revision: "45"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2ff75ba3c32d138d9124eba5cfe170cf146d5778
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-checkconstraints-transact-sql"></a>DBCC CHECKCONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Comprueba la integridad de una restricción especificada o de todas las restricciones de una tabla determinada en la base de datos actual.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DBCC CHECKCONSTRAINTS  
[   
    (   
    table_name | table_id | constraint_name | constraint_id   
    )  
]  
    [ WITH   
    [ { ALL_CONSTRAINTS | ALL_ERRORMSGS } ]  
    [ , ] [ NO_INFOMSGS ]   
    ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name* | *table_id* | *constraint_name* | *constraint_id*  
 Es la tabla o la restricción que se va a comprobar. Cuando *table_name* o *table_id* está especificado, se comprueban todas las restricciones habilitadas en la tabla. Cuando *constraint_name* o *constraint_id* está especificado, se comprueba sólo esa restricción. Si no se especifica un identificador de tabla ni un identificador de restricción, se comprueban todas las restricciones habilitadas en todas las tablas de la base de datos actual.  
 Un nombre de restricción identifica exclusivamente a la tabla a la que pertenece. Para obtener más información, vea [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 por  
 Habilita la especificación de opciones.  
  
 ALL_CONSTRAINTS  
 Comprueba todas las restricciones habilitadas y deshabilitadas de la tabla, si se especifica el nombre de tabla o si se comprueban todas las tablas; de lo contrario, comprueba solo la restricción habilitada. ALL_CONSTRAINTS no tiene ningún efecto cuando se especifica un nombre de restricción.  
  
 ALL_ERRORMSGS  
 Devuelve todas las filas que infringen las restricciones de la tabla comprobada. El valor predeterminado es las 200 primeras filas.  
  
 NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
## <a name="remarks"></a>Comentarios  
DBCC CHECKCONSTRAINTS construye y ejecuta una consulta para todas las restricciones FOREIGN KEY y CHECK en una tabla.
  
Por ejemplo, una consulta de clave externa tiene el siguiente formato:
  
```sql
SELECT <columns>  
FROM <table_being_checked> LEFT JOIN <referenced_table>  
    ON <table_being_checked.fkey1> = <referenced_table.pkey1>   
    AND <table_being_checked.fkey2> = <referenced_table.pkey2>  
WHERE <table_being_checked.fkey1> IS NOT NULL   
    AND <referenced_table.pkey1> IS NULL  
    AND <table_being_checked.fkey2> IS NOT NULL  
    AND <referenced_table.pkey2> IS NULL  
```  
  
La consulta de datos se almacena en una tabla temporal. Tras la comprobación de todas las tablas o restricciones solicitadas, se devuelve el conjunto de resultados.
DBCC CHECKCONSTRAINTS comprueba la integridad de las restricciones FOREIGN KEY y CHECK, pero no comprueba la integridad de las estructuras de datos del disco en una tabla. Estas comprobaciones de la estructura de datos pueden realizarse mediante [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) y [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
  
**Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
Si *table_name* o *table_id* se especifica y está habilitado para control de versiones de sistema, DBCC CHECKCONSTRAINTS también realiza comprobaciones de coherencia de datos temporales en la tabla especificada. Cuando *NO_INFOMSGS* no se especifica, este comando devolverá cada infracción de coherencia en la salida en una línea independiente. El formato del resultado será ([pkcol1], [pkcol2]...) = (\<pkcol1_value >, \<pkcol2_value >...) Y \<cuál es el problema con el registro de la tabla temporal >.
  
|Comprobación|Información adicional en la salida si el error de comprobación|  
|-----------|-----------------------------------------------|  
|PeriodEndColumn ≥ PeriodStartColumn (actual)|[sys_end] = '{0}' AND MAX(DATETIME2) = '9999-12-31 23:59:59.99999'|  
|PeriodEndColumn ≥ PeriodStartColumn (actual, historial)|[sys_start] = '{0}' AND [sys_end] = '{1}'|  
|PeriodStartColumn < current_utc_time (actual)|[sys_start] = '{0}' y SYSUTCTIME|  
|PeriodEndColumn < current_utc_time (historial)|[sys_end] = '{0}' y SYSUTCTIME|  
|Se superpone a|(sys_start1, sys_end1), (sys_start2, sys_end2) para dos que se superponen los registros.<br /><br /> Si hay más de 2 que se superponen los registros, salida tendrá varias filas cada uno con un par de superposiciones.|  
  
No hay ninguna manera de especificar constraint_name o constraint_id para ejecutar comprobaciones de coherencia solo.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC CHECKCONSTRAINTS devuelve un conjunto de filas con las siguientes columnas.
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|Nombre de tabla|**varchar**|Nombre de la tabla.|  
|Constraint Name|**varchar**|Nombre de la restricción infringida.|  
|Where|**varchar**|Asignaciones del valor de columna que identifican la fila o las filas que infringen la restricción.<br /><br /> El valor de esta columna se puede utilizar en una cláusula WHERE de una instrucción SELECT para consultar qué filas infringen la restricción.|  
  
## <a name="permissions"></a>Permissions  
Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-checking-a-table"></a>A. Comprobar una tabla  
El ejemplo siguiente comprueba la integridad de la restricción de la tabla `Table1` de la base de datos `AdventureWorks`.
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (Col1 int, Col2 char (30));  
GO  
INSERT INTO Table1 VALUES (100, 'Hello');  
GO  
ALTER TABLE Table1 WITH NOCHECK ADD CONSTRAINT chkTab1 CHECK (Col1 > 100);  
GO  
DBCC CHECKCONSTRAINTS(Table1);  
GO  
```  
  
### <a name="b-checking-a-specific-constraint"></a>B. Comprobar una restricción específica  
El ejemplo siguiente comprueba la integridad de la restricción `CK_ProductCostHistory_EndDate`.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKCONSTRAINTS ('Production.CK_ProductCostHistory_EndDate');  
GO  
```  
  
### <a name="c-checking-all-enabled-and-disabled-constraints-on-all-tables"></a>C. Comprobar todas las restricciones habilitadas y deshabilitadas en todas las tablas  
 El ejemplo siguiente comprueba la integridad de todas las restricciones habilitadas y deshabilitadas en todas las tablas de la base de datos actual.  
  
```sql  
DBCC CHECKCONSTRAINTS WITH ALL_CONSTRAINTS;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
