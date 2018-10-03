---
title: INSERT (gráfico SQL) | Microsoft Docs
description: Sintaxis INSERT para tablas perimetrales o de nodo de gráfico SQL.
ms.date: 05/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], SQL graph
- SQL graph, INSERT statement
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c0a22547436f8a511a5a61db35ec99a919d84e4b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644033"
---
# <a name="insert-sql-graph"></a>INSERT (gráfico SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Agrega una o varias filas a una tabla `node` o `edge` en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!NOTE]   
>  Para obtener instrucciones Transact-SQL estándar, vea [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md).
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="insert-into-node-table-syntax"></a>Sintaxis INSERT en tabla de nodo 
La sintaxis para insertar en una tabla de nodo es la misma que la de una tabla normal. 

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
 En este documento se describen los argumentos pertenecientes a un gráfico SQL. Para obtener una lista completa y una descripción de los argumentos admitidos en una instrucción INSERT, vea [INSERT TABLE (Transact-SQL)](../../t-sql/statements/insert-transact-sql.md).

 INTO  
 Es una palabra clave opcional que se puede usar entre `INSERT` y la tabla de destino.  
  
 *search_condition_with_match*   
 La cláusula `MATCH` se puede usar en una subconsulta mientras se realiza una operación de inserción en una tabla de nodo o perimetral. Para obtener la sintaxis la instrucción `MATCH`, vea [GRAPH MATCH (Transact-SQL)](../../t-sql/queries/match-sql-graph.md).

 *graph_search_pattern*   
 Patrón de búsqueda proporcionado a la cláusula `MATCH` como parte del predicado del gráfico.

 *edge_table_column_list*   
 Los usuarios deben proporcionar valores en `$from_id` y `$to_id` al realizar una operación de inserción en una tabla perimetral. De lo contrario, se devolverá un error o se insertará NULL en esas columnas. 
  

## <a name="remarks"></a>Notas  
Insertar en un nodo es lo mismo que insertar en cualquier tabla relacional. Los valores de la columna $node_id se generan automáticamente.

Al insertar en una tabla perimetral, los usuarios deben proporcionar valores para las columnas `$from_id` y `$to_id`.   

La inserción con BULK en una tabla de nodo permanece igual que en una tabla relacional.

Antes de insertar con BULK en una tabla perimetral, las tablas de nodo se deben importar. Así, los valores de `$from_id` y `$to_id` se podrán extraer de la columna `$node_id` de la tabla de nodo y se insertarán en la tabla perimetral. 

  
### <a name="permissions"></a>Permisos  
 El permiso INSERT es obligatorio en la tabla de destino.  
  
 Los permisos INSERT corresponden de forma predeterminada a los miembros del rol fijo de servidor **sysadmin**, de los roles fijos de base de datos **db_owner** y **db_datawriter** y al propietario de la tabla. Los miembros de los roles **sysadmin**, **db_owner** y **db_securityadmin** y el propietario de la tabla pueden transferir permisos a otros usuarios.  
  
 Para ejecutar INSERT con la opción BULK de la función OPENROWSET, debe ser miembro de los roles fijos de servidor **sysadmin** o **bulkadmin**.  
  

## <a name="examples"></a>Ejemplos  
  
#### <a name="a--insert-into-node-table"></a>A.  Insertar en una tabla de nodo  
 En el siguiente ejemplo se crea una tabla de nodo Person y se insertan 2 filas en ella.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 
 -- Insert records for Alice and John
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 ```
  
#### <a name="b--insert-into-edge-table"></a>B.  Insertar en una tabla perimetral  
 En el siguiente ejemplo se crea una tabla perimetral friend y se inserta un borde en ella.

 ```
 -- Create friend edge table
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Create a friend edge, that connect Alice and John
 INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');
 ```

  
## <a name="see-also"></a>Ver también  
 [INSERT TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Graph processing with SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md) (Procesamiento de gráficos con SQL Server 2017)  


