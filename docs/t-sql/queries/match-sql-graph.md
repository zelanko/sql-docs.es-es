---
title: MATCH (SQL Graph) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 76807bc54394fe55248e76791fa97ae693cb462d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38027292"
---
# <a name="match-transact-sql"></a>MATCH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  Especifica una condición de búsqueda para un gráfico. MATCH puede usarse solo con tablas perimetrales o de nodo del gráfico, en la instrucción SELECT y como parte de la cláusula WHERE. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
MATCH (<graph_search_pattern>)

<graph_search_pattern>::=
    {<node_alias> { 
                     { <-( <edge_alias> )- } 
                   | { -( <edge_alias> )-> }
                 <node_alias> 
                 } 
     }
     [ { AND } { ( <graph_search_pattern> ) } ]
     [ ,...n ]
  
<node_alias> ::=
    node_table_name | node_alias 

<edge_alias> ::=
    edge_table_name | edge_alias
```

## <a name="arguments"></a>Argumentos  
*graph_search_pattern*  
Especifica el patrón que buscar o la ruta de acceso que atravesar en el gráfico. Este patrón usa sintaxis de arte ASCII para atravesar una ruta de acceso en el gráfico. El patrón va de un nodo a otro a través de un borde, en la dirección de la flecha proporcionada. Los nombres o alias de borde se suministran entre paréntesis. Los nombres o alias de nodo aparecen en los dos extremos de la flecha. La flecha puede ir en ambas direcciones en el patrón.

*node_alias*  
Nombre o alias de una tabla de nodo que se proporciona en la cláusula FROM.

*edge_alias*  
Nombre o alias de una tabla perimetral que se proporciona en la cláusula FROM.


## <a name="remarks"></a>Notas  
Los nombres de nodo dentro de MATCH se pueden repetir.  Dicho de otro, un nodo se puede atravesar un número arbitrario de veces en la misma consulta.  
Los nombres de borde no se pueden repetir dentro de MATCH.  
Un borde puede apuntar a cualquier dirección, pero debe tener una dirección explícita.  
Los operadores OR y NOT no se pueden usar en el patrón MATCH. MATCH se puede combinar con otras expresiones por medio de AND en la cláusula WHERE, pero esto no es posible con los operadores OR ni NOT. 

## <a name="examples"></a>Ejemplos  
### <a name="a--find-a-friend"></a>A.  Buscar un amigo 
 En el siguiente ejemplo se crea una tabla de nodos Person y una tabla perimetral friend, se insertan algunos datos y, tras ello, se usa MATCH para encontrar amigos de Alice, una persona del gráfico.

 ```
 -- Create person node table
 CREATE TABLE dbo.Person (ID integer PRIMARY KEY, name varchar(50)) AS NODE;
 CREATE TABLE dbo.friend (start_date DATE) AS EDGE;

 -- Insert into node table
 INSERT INTO dbo.Person VALUES (1, 'Alice');
 INSERT INTO dbo.Person VALUES (2,'John');
 INSERT INTO dbo.Person VALUES (3, 'Jacob');

-- Insert into edge table
INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'John'), '9/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'Alice'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2011');

INSERT INTO dbo.friend VALUES ((SELECT $node_id FROM dbo.Person WHERE name = 'John'),
        (SELECT $node_id FROM dbo.Person WHERE name = 'Jacob'), '10/15/2012');

-- use MATCH in SELECT to find friends of Alice
SELECT Person2.name AS FriendName
FROM Person Person1, friend, Person Person2
WHERE MATCH(Person1-(friend)->Person2)
AND Person1.name = 'Alice';

 ```

 ### <a name="b--find-friend-of-a-friend"></a>B.  Buscar un amigo de un amigo
 En el siguiente ejemplo se intenta encontrar un amigo de un amigo de Alice. 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>C.  Más patrones de `MATCH`
 Aquí encontrará algunas formas más en las que se puede especificar un patrón en MATCH.

 ```
 -- Find a friend
    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2
    WHERE MATCH(Person1-(friend)->Person2);
    
-- The pattern can also be expressed as below

    SELECT Person2.name AS FriendName
    FROM Person Person1, friend, Person Person2 
    WHERE MATCH(Person2<-(friend)-Person1);


-- Find 2 people who are both friends with same person
    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0<-(friend2)-Person2);
    
-- this pattern can also be expressed as below

    SELECT Person1.name AS Friend1, Person2.name AS Friend2
    FROM Person Person1, friend friend1, Person Person2, 
         friend friend2, Person Person0
    WHERE MATCH(Person1-(friend1)->Person0 AND Person2-(friend2)->Person0);
 ```
 

## <a name="see-also"></a>Ver también  
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [Graph processing with SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md) (Procesamiento de gráficos con SQL Server 2017)  
