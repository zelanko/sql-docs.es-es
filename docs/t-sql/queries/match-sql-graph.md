---
title: "COINCIDENCIA (gráfico SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/05/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MATCH
- MATCH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
ms.assetid: 
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: db211fa0988f2dbe6a72291f898d670d44d3f215
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="match-transact-sql"></a>COINCIDENCIA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  Especifica una condición de búsqueda para un gráfico. COINCIDENCIA puede usarse sólo con las tablas de nodo y borde gráfico, en la instrucción SELECT como parte de la cláusula WHERE. 
  
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
Especifica el patrón de búsqueda o ruta de acceso para recorrer en el gráfico. Este patrón utiliza sintaxis de carátulas de ASCII para recorrer una ruta de acceso en el gráfico. El patrón de tránsito de un nodo a otro a través de un borde, en la dirección de la flecha proporcionada. Borde nombres o los alias se proporcionan dentro de paréntesis. Nombres de nodo o alias aparecen en los dos extremos de la flecha. La flecha puede ir en ambas direcciones en el patrón.

*node_alias*  
Nombre o alias de una tabla de nodo que se proporcionan en la cláusula FROM.

*edge_alias*  
Nombre o alias de una tabla irregular proporcionada en la cláusula FROM.


## <a name="remarks"></a>Comentarios  
Se pueden repetir los nombres de nodo dentro de la coincidencia.  En otras palabras, un nodo puede atravesar un número arbitrario de veces en la misma consulta.  
No se puede repetir el nombre de un borde dentro de la coincidencia.  
Puede señalar un borde en cualquier dirección, pero debe tener una dirección explícita.  
O y no se admiten operadores NOT en el patrón de coincidencia. COINCIDENCIA se puede combinar con otras expresiones con y en la cláusula WHERE. Sin embargo, combinarla con otras expresiones mediante OR o no se admite. 

## <a name="examples"></a>Ejemplos  
### <a name="a--find-a-friend"></a>A.  Buscar a un amigo 
 En el ejemplo siguiente se crea una tabla de nodos de la persona y la tabla irregular de amigos, inserta algunos datos y, a continuación, usa a coincidencia para buscar a elementos friend de Alicia, una persona en el gráfico.

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

 ### <a name="b--find-friend-of-a-friend"></a>B.  Buscar a elemento friend de un amigo
 En el ejemplo siguiente se intenta encontrar a friend de un elemento friend de Alicia. 

 ```
SELECT Person3.name AS FriendName 
FROM Person Person1, friend, Person Person2, friend friend2, Person Person3
WHERE MATCH(Person1-(friend)->Person2-(friend2)->Person3)
AND Person1.name = 'Alice';

 ```

### <a name="c--more-match-patterns"></a>C.  Más `MATCH` patrones
 A continuación se indican algunas formas más en el que puede especificarse un patrón dentro de la coincidencia.

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
 

## <a name="see-also"></a>Vea también  
 [Crear tabla &#40; Gráfico SQL &#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (gráfico SQL)](../../t-sql/statements/insert-sql-graph.md)]  
 [Gráfico de procesamiento con SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md)  

