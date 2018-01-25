---
title: "INSERT (gráfico SQL) | Documentos de Microsoft"
description: "Inserte la sintaxis para las tablas de borde o nodo de gráfico de SQL."
ms.date: 05/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: 
caps.latest.revision: "1"
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6bac7f1d7da67f319a9c84425b370bb61a35ca19
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="insert-sql-graph"></a>INSERT (gráfico SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Agrega una o más filas a un `node` o `edge` tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!NOTE]   
>  Para instrucciones Transact-SQL estándar, consulte [Insertar tabla (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md).
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>Insertar en la sintaxis de la tabla de nodo 
La sintaxis para insertar en una tabla de nodo es el misma que el de una tabla normal. 

```  
[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ (column_list) ] | [(<edge_table_column_list>)]  
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
    node_table_name  | edge_table_name
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <on_or_where_search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  

<on_or_where_search_condition> ::=
    {  <search_condition_with_match> | <search_condition> }

<search_condition_with_match> ::=
    { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) }
    [ AND { <graph_predicate> | [ NOT ] <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<search_condition> ::=
    { [ NOT ] <predicate> | ( <search_condition> ) }
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]
    [ ,...n ]

<graph_predicate> ::=
    MATCH( <graph_search_pattern> [ AND <graph_search_pattern> ] [ , ...n] )

<graph_search_pattern>::=
    <node_alias> { { <-( <edge_alias> )- | -( <edge_alias> )-> } <node_alias> }

<edge_table_column_list> ::=
    ($from_id, $to_id, [column_list])

```  
  
 
## <a name="arguments"></a>Argumentos  
 Este documento describe los argumentos pertenecen al gráfico SQL. Para una lista completa y una descripción de los argumentos admitidos en la instrucción INSERT, vea [Insertar tabla (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md)

 INTO  
 Es una palabra clave opcional que se puede usar entre `INSERT` y la tabla de destino.  
  
 *search_condition_with_match*   
 `MATCH`cláusula se puede usar en una subconsulta al insertar en una tabla de nodo o borde. Para `MATCH` sintaxis de la instrucción, consulte [gráfico coincidencia (Transact-SQL)](../../t-sql/queries/match-sql-graph.md)

 *graph_search_pattern*   
 Patrón de búsqueda proporcionado a `MATCH` cláusula como parte del predicado de gráfico.

 *edge_table_column_list*   
 Los usuarios deben proporcionar valores para `$from_id` y `$to_id` al insertar en un borde. Si no se proporciona un valor o valores NULL se inserta en estas columnas, se devolverá un error. 
  

## <a name="remarks"></a>Comentarios  
Insertar en un nodo es el mismo que insertar en cualquier tabla relacional. Valores de la columna de node_id $ se generan automáticamente.

Al insertar en una tabla irregular, los usuarios deben proporcionar valores para `$from_id` y `$to_id` columnas.   

Inserción masiva para la tabla de nodos es permanece igual una tabla relacional.

Antes de insertar en una tabla irregular de forma masiva, se deben importar las tablas del nodo. Los valores para `$from_id` y `$to_id` , a continuación, se puede extraer de la `$node_id` columna de la tabla de nodos y se inserta como bordes. 

  
### <a name="permissions"></a>Permissions  
 El permiso INSERT es obligatorio en la tabla de destino.  
  
 Insertar el valor predeterminado de permisos a los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** y **db_datawriter** se han corregido los roles de base de datos y el propietario de la tabla. Los miembros de la **sysadmin**, **db_owner**y el **db_securityadmin** roles y el propietario de la tabla pueden transferir permisos a otros usuarios.  
  
 Para ejecutar INSERT con la opción BULK de función OPENROWSET, debe ser miembro de la **sysadmin** rol fijo de servidor o de la **bulkadmin** rol fijo de servidor.  
  

## <a name="examples"></a>Ejemplos  
  
#### <a name="a--insert-into-node-table"></a>A.  Insertar en la tabla de nodos  
 En el ejemplo siguiente se crea una tabla de nodo de la persona e inserta 2 filas de esa tabla.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  Insertar en la tabla irregular  
 En el ejemplo siguiente se crea una tabla irregular de confianza y se inserta un borde en la tabla.

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>Vea también  
 [Insertar tabla &#40; Transact-SQL &#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Gráfico de procesamiento con SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)  


