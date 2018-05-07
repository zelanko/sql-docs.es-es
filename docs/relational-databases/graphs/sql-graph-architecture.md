---
title: Arquitectura de gráfico SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 04/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 7cfba1fc79e44bb28a433c3b31fe5f4236037d6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-graph-architecture"></a>Arquitectura de gráfico SQL  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Obtenga información acerca de cómo se ha diseñado el gráfico de SQL. Conocer los conceptos básicos le resultará más fácil de entender otros artículos de gráfico de SQL.
 
## <a name="sql-graph-database"></a>Base de datos de gráfico SQL
Los usuarios pueden crear un gráfico por cada base de datos. Un gráfico es una colección de tablas de nodo y de borde. Se pueden crear tablas de borde o nodo en cualquier esquema de la base de datos, pero que pertenezcan a un gráfico de la lógico. Una tabla de nodo es la colección de un tipo similar de nodos. Por ejemplo, una tabla de nodo de la persona que contiene todos los nodos de la persona que pertenecen a un gráfico. De forma similar, una tabla irregular es una colección de un tipo similar de bordes. Por ejemplo, una tabla irregular de amigos contiene todos los bordes que se conectan a una persona a otra persona. Puesto que los nodos y bordes se almacenan en tablas, la mayoría de las operaciones admitidas en las tablas normales se admite en tablas de borde o nodo. 
 
 
![arquitectura de gráfico de SQL](../../relational-databases/graphs/media/sql-graph-architecture.png "arquitectura de base de datos de gráfico de Sql")   

La figura 1: Arquitectura de base de datos gráfico SQL
 
## <a name="node-table"></a>Tabla de nodos
Una tabla de nodo representa una entidad en un esquema de gráfico. Cada vez que nodo se crea una tabla, junto con las columnas definidas por el usuario, implícita `$node_id` creada columna, que identifica de forma única un nodo determinado en la base de datos. Los valores de `$node_id` se generan automáticamente y son una combinación de `object_id` de esa tabla de nodo y un valor generado internamente bigint. Sin embargo, cuando la `$node_id` columna está seleccionada, se muestra un valor calculado en forma de una cadena JSON. Además, `$node_id` es una pseudocolumna, que se asigna a un nombre interno con una cadena hexadecimal en ella. Cuando se selecciona `$node_id` de la tabla, el nombre de columna aparecerá como `$node_id_<hex_string>`. Usar nombres de columna pseudo en consultas es la manera recomendada de la consulta interna `$node_id` columna y con nombre interno a cadena hexadecimal deben evitarse.

Se recomienda que los usuarios crear una restricción unique o un índice en la `$node_id` columna en el momento de creación de tabla de nodo, pero si uno no está creado, valor predeterminado se crea automáticamente índice único, no agrupado. Sin embargo, los índices de una pseudocolumna gráfico se crean en las columnas subyacentes internas. Es decir, un índice creado en el `$node_id` columna, aparecerá en el fax interno `graph_id_<hex_string>` columna.   


## <a name="edge-table"></a>Tabla irregular
Una tabla irregular representa una relación en un gráfico. Bordes siempre se dirigen y conectan los dos nodos. Una tabla irregular permite a los usuarios para modelar las relaciones de varios a varios en el gráfico. Una tabla irregular puede o no puede tener atributos definidos por el usuario en ella. Cada vez que se crea una tabla irregular, junto con los atributos definidos por el usuario, se crean tres columnas implícitas de la tabla irregular:

|Nombre de columna    |Description  |
|---   |---  |
|`$edge_id`   |Identifica de forma única un borde determinado en la base de datos. Es una columna generada y el valor es una combinación de object_id de la tabla irregular y un valor generado internamente bigint. Sin embargo, cuando la `$edge_id` columna está seleccionada, se muestra un valor calculado en forma de una cadena JSON. `$edge_id` es una pseudocolumna, que se asigna a un nombre interno con una cadena hexadecimal en ella. Cuando se selecciona `$edge_id` de la tabla, el nombre de columna aparecerá como `$edge_id_\<hex_string>`. Usar nombres de columna pseudo en consultas es la manera recomendada de la consulta interna `$edge_id` columna y con nombre interno a cadena hexadecimal deben evitarse. |
|`$from_id`   |Almacena el `$node_id` del nodo, desde donde se origina el borde.  |
|`$to_id`   |Almacena el `$node_id` del nodo, en el que finaliza el borde. |

Los nodos que se puede conectar a un borde determinado se rige por los datos insertados en la `$from_id` y `$to_id` columnas. En la primera versión, no es posible definir restricciones en la tabla irregular para impedir que conecta los dos tipos de nodos. Es decir, un borde puede conectar dos nodos en el gráfico, con independencia de sus tipos.

Similar a la `$node_id` columna, se recomienda que los usuarios crear un índice único o restricción en la `$edge_id` columna en el momento de creación de la tabla irregular, pero si uno no está creado, índice único, no agrupado se crea automáticamente en valor predeterminado Esta columna. Sin embargo, los índices de una pseudocolumna gráfico se crean en las columnas subyacentes internas. Es decir, un índice creado en el `$edge_id` columna, aparecerá en el fax interno `graph_id_<hex_string>` columna. También se recomienda, para escenarios OLTP, que los usuarios crear un índice en (`$from_id`, `$to_id`) de las columnas, para las búsquedas más rápidas en la dirección del borde.  

La figura 2 muestra cómo se almacenan las tablas de nodo y de borde en la base de datos. 

![tablas de amigos persona](../../relational-databases/graphs/media/person-friends-tables.png "nodo Person y amigos arista tablas")   

La figura 2: Representación de tabla de nodo y el borde



## <a name="metadata"></a>Metadatos
Utilice estas vistas de metadatos para ver los atributos de una tabla de nodo o borde.
 
### <a name="systables"></a>sys.tables
Las siguientes funciones, tipo de bit, se agregarán columnas a SYS. TABLAS. Si `is_node` está establecido en 1, que indica que la tabla es una tabla de nodo y si `is_edge` está establecido en 1, que indica que la tabla es una tabla irregular.
 
|Nombre de la columna |Tipo de datos |Description |
|--- |---|--- |
|is_node |bit |1 = se trata de una tabla de nodo |
|is_edge |bit |1 = se trata de una tabla irregular |
 
### <a name="syscolumns"></a>sys.columns
El `sys.columns` vista contiene columnas adicionales `graph_type` y `graph_type_desc`, que indican el tipo de la columna de tablas de nodo y de borde.
 
|Nombre de la columna |Tipo de datos |Description |
|--- |---|--- |
|graph_type |int |Columna interna con un conjunto de valores. Los valores están comprendidos entre 1-8 para las columnas del gráfico y NULL para otros usuarios.  |
|graph_type_desc |nvarchar(60)  |columna interna con un conjunto de valores |
 
En la tabla siguiente se enumera los valores válidos para `graph_type` columna

|Valor de la columna  |Description  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` también almacena información acerca de las columnas implícitas creados en las tablas de borde o nodo. Después de la información se pueden recuperar desde sys.columns, sin embargo, los usuarios no pueden seleccionar estas columnas de una tabla de nodo o borde. 

Columnas implícitas en una tabla de nodo  
|Nombre de la columna    |Tipo de datos  |is_hidden  |Comentario  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |columna de graph_id interno  |
|$node_id_\<cadena_hex > |NVARCHAR   |0  |Columna de Id. de nodo externo  |

Columnas implícitas en una tabla irregular  
|Nombre de la columna    |Tipo de datos  |is_hidden  |Comentario  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |columna de graph_id interno  |
|$edge_id_\<cadena_hex > |NVARCHAR   |0  |columna de Id. de borde externo  |
|from_obj_id_\<hex_string>  |INT    |1  |interno de Id. de objeto de nodo  |
|from_id_\<cadena_hex >  |bigint |1  |Interno de nodo graph_id  |
|$from_id_\<cadena_hex > |NVARCHAR   |0  |desde Id. de nodo  |
|to_obj_id_\<hex_string>    |INT    |1  |Id. de objeto de nodo interno  |
|to_id_\<hex_string>    |bigint |1  |Nodo graph_id interno  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |fuera del Id. de nodo  |
 
### <a name="system-functions"></a>Funciones del sistema
Se agregan las siguientes funciones integradas. Le ayudarán a los usuarios extraer información de las columnas generadas. Tenga en cuenta que, estos métodos no valida la entrada del usuario. Si el usuario especifica un válido `sys.node_id` el método extraer la parte adecuada y devolverlo. Por ejemplo, llevará a cabo OBJECT_ID_FROM_NODE_ID una `$node_id` como entrada y devolverá el object_id de la tabla, pertenece este nodo. 
 
|Integrada   |Description  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Extraer el object_id de un node_id  |
|GRAPH_ID_FROM_NODE_ID  |Extraiga el graph_id un node_id  |
|NODE_ID_FROM_PARTS |Construir un node_id desde un object_id y un graph_id  |
|OBJECT_ID_FROM_EDGE_ID |Extraiga object_id edge_id  |
|GRAPH_ID_FROM_EDGE_ID  |Extraer la identidad de edge_id  |
|EDGE_ID_FROM_PARTS |Construir edge_id de object_id e identidad  |



## <a name="transact-sql-reference"></a>Referencia de Transact-SQL 
Obtenga información acerca de la [!INCLUDE[tsql-md](../../includes/tsql-md.md)] las extensiones que se introdujo en SQL Server y base de datos de SQL Azure, que permiten crear y consultar objetos de gráfico. Las extensiones de lenguaje de consulta ayudan a consultas y recorren el gráfico con la sintaxis de arte ASCII.
 
### <a name="data-definition-language-ddl-statements"></a>Instrucciones de lenguaje de definición (DDL) de datos
|Tarea   |Tema relacionado  |Notas
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE ` Ahora se ha ampliado para admitir la creación de una tabla en el borde de AS o nodo de AS. Tenga en cuenta que una tabla irregular puede o que no haya ningún usuario definido atributos.  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Se pueden modificar tablas de borde y el nodo del mismo modo que una tabla relacional, usa el `ALTER TABLE`. Los usuarios pueden agregar o modificar las columnas definidas por el usuario, índices o restricciones. Sin embargo, modificar las columnas de gráfico interno, como `$node_id` o `$edge_id`, se producirá un error.  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |Los usuarios pueden crear índices en pseudocolumnas y las columnas definidas por el usuario en tablas de nodo y de borde. Se admiten todos los tipos de índices, incluidos los índices de almacén de columnas agrupados y no agrupados.  |
|DROP TABLE |[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |Pueden quitar tablas de nodo y el borde del mismo modo que una tabla relacional, usa el `DROP TABLE`. Sin embargo, en esta versión, no hay ninguna restricción para asegurarse de que ningún bordes apuntar a un nodo se eliminó y no se admite la eliminación en cascada de bordes, tras la eliminación de un nodo o una tabla de nodos. Se recomienda que, si se quita una tabla de nodo, los usuarios quitar los bordes que se conecta a los nodos de esa tabla nodo manualmente para mantener la integridad del gráfico.  |


### <a name="data-manipulation-language-dml-statements"></a>Instrucciones de lenguaje de manipulación (DML) de datos
|Tarea   |Tema relacionado  |Notas
|---  |---  |---  |
|INSERT |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|Insertar en una tabla de nodo es similar a insertar en una tabla relacional. Los valores de `$node_id` columna se genera automáticamente. Ha intentado insertar un valor en `$node_id` o `$edge_id` columna se producirá un error. Los usuarios deben proporcionar valores para `$from_id` y `$to_id` columnas al insertar en una tabla irregular. `$from_id` y `$to_id` son el `$node_id` valores de los nodos que se conecta un borde determinado.  |
|DELETE | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Datos de tablas de borde o nodo pueden eliminarse igual se eliminan de las tablas relacionales. Sin embargo, en esta versión, no hay ninguna restricción para asegurarse de que ningún bordes apuntar a un nodo se eliminó y no se admite la eliminación en cascada de bordes, tras la eliminación de un nodo. Se recomienda que cada vez que se elimina un nodo, todos los bordes de conexión a dicho nodo también se eliminan, para mantener la integridad del gráfico.  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |Valores en columnas definidas por el usuario pueden actualizarse mediante la instrucción UPDATE. Actualizar las columnas de gráfico interno, `$node_id`, `$edge_id`, `$from_id` y `$to_id` no está permitido.  |
|MERGE |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` no se admite la instrucción en una tabla de nodo o borde.  |


### <a name="query-statements"></a>Instrucciones de consulta
|Tarea   |Tema relacionado  |Notas
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|Nodos y bordes se almacenan internamente como tablas, por lo tanto, admite la mayoría de las operaciones admitidas en una tabla de SQL Server o base de datos de SQL Azure en las tablas de nodo y de borde  |
|MATCH  | [COINCIDENCIA &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)|COINCIDENCIA integrados se introdujeron para admitir la coincidencia de patrones y recorrido a través del gráfico.  |



## <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos  
Existen ciertas limitaciones en el nodo y el borde de las tablas en esta versión:
* Tablas temporales locales o globales no pueden ser el borde o el nodo tablas.
* Tipos de tablas y las variables de tabla no pueden declararse como una tabla de nodo o borde. 
* No se puede crear tablas de nodo y borde como tablas temporales con versión del sistema.   
* Tablas de borde y de nodo no pueden ser tablas optimizadas en memoria.  
* Los usuarios no pueden actualizar las from_id $ y $to_id columnas de un borde mediante la instrucción UPDATE. Para actualizar los nodos que un borde conecta, los usuarios tendrán que el borde nueva señalando a nuevos nodos de inserción y eliminación anterior.
* Entre la base de datos no se admiten las consultas en objetos de gráfico. 


## <a name="next-steps"></a>Pasos siguientes
Para empezar a usar la nueva sintaxis, vea [base de datos de gráfico de SQL - ejemplo](./sql-graph-sample.md)
 

