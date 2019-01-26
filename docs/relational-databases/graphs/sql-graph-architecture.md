---
title: Arquitectura SQL Graph | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e4c7c5bae386f142dff45be8a1b1371f104cfab3
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044551"
---
# <a name="sql-graph-architecture"></a>Arquitectura SQL Graph  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Obtenga información sobre cómo se ha diseñado como gráfico SQL. Conocer los aspectos básicos le resultará más fácil entender otros artículos de gráfico SQL.
 
## <a name="sql-graph-database"></a>Base de datos SQL Graph
Los usuarios pueden crear un gráfico por cada base de datos. Un gráfico es una colección de tablas perimetrales y de nodo. Las tablas de nodo o perimetral pueden crearse en cualquier esquema de la base de datos, pero que pertenezcan a un gráfico de la lógico. Una tabla de nodo es la colección de un tipo similar de nodos. Por ejemplo, una tabla de nodo Person contiene todos los nodos de la persona que pertenecen a un gráfico. De forma similar, una tabla perimetral es una colección de un tipo similar de bordes. Por ejemplo, una tabla irregular de amigos contiene todos los bordes que se conectan a una persona a otra persona. Dado que los nodos y bordes se almacenan en tablas, admite la mayoría de las operaciones admitidas en las tablas normales en las tablas de nodo o perimetral. 
 
 
![arquitectura de SQL graph](../../relational-databases/graphs/media/sql-graph-architecture.png "arquitectura de base de datos de Sql graph")   

Figura 1: Arquitectura de la base de datos de SQL Graph
 
## <a name="node-table"></a>Tabla de nodo
Una tabla de nodo representa una entidad en un esquema de gráfico. Cada vez que una tabla de nodo se crea, junto con las columnas definidas por el usuario, implícita `$node_id` creada, que identifica de forma única un nodo determinado en la base de datos. Los valores de `$node_id` se generan automáticamente y son una combinación de `object_id` de esa tabla de nodo y un valor bigint generado internamente. Sin embargo, cuando la `$node_id` columna está seleccionada, se muestra un valor calculado en forma de una cadena JSON. Además, `$node_id` es una pseudocolumna, que se asigna a un nombre interno con una cadena hexadecimal en ella. Al seleccionar `$node_id` de la tabla, el nombre de columna aparecerá como `$node_id_<hex_string>`. Usar nombres de columna pseudo en consultas es la manera recomendada de consultas interno `$node_id` columna y el uso de nombres interna con la cadena hexadecimal deben evitarse.

Se recomienda que los usuarios creación una restricción unique o de índice en la `$node_id` columna en el momento de creación de tabla de nodo, pero si uno no está creado, un valor predeterminado que automáticamente se crea el índice no agrupado único. Sin embargo, se crea un índice en una pseudocolumna del gráfico en las columnas subyacentes internas. Es decir, un índice creado en el `$node_id` columna, aparecerá en el interno `graph_id_<hex_string>` columna.   


## <a name="edge-table"></a>Tabla irregular
Una tabla perimetral representa una relación en un gráfico. Bordes siempre se dirigen y conectan los dos nodos. Una tabla irregular permite a los usuarios para modelar las relaciones de varios a varios en el gráfico. Una tabla perimetral puede o no tenga ningún atributo definido por el usuario en ella. Cada vez que se crea una tabla irregular, junto con los atributos definidos por el usuario, se crean tres columnas implícitas en la tabla irregular:

|Nombre de columna    |Descripción  |
|---   |---  |
|`$edge_id`   |Identifica un borde determinado en la base de datos. Es una columna generada y el valor es una combinación de object_id de la tabla irregular y un valor bigint generado internamente. Sin embargo, cuando la `$edge_id` columna está seleccionada, se muestra un valor calculado en forma de una cadena JSON. `$edge_id` es una pseudocolumna, que se asigna a un nombre interno con una cadena hexadecimal en ella. Al seleccionar `$edge_id` de la tabla, el nombre de columna aparecerá como `$edge_id_\<hex_string>`. Usar nombres de columna pseudo en consultas es la manera recomendada de consultas interno `$edge_id` columna y el uso de nombres interna con la cadena hexadecimal deben evitarse. |
|`$from_id`   |Almacena el `$node_id` del nodo, desde donde se origina el borde.  |
|`$to_id`   |Almacena el `$node_id` del nodo, en el que finaliza el borde. |

Los nodos que se puede conectar a un borde determinado se rige por los datos insertados en el `$from_id` y `$to_id` columnas. En la primera versión, no es posible definir restricciones en la tabla irregular, para impedir que conecta los dos tipos de nodos. Es decir, un borde puede conectar dos nodos en el gráfico, independientemente de sus tipos.

Similar a la `$node_id` columna, se recomienda que los usuarios crear una restricción o índice único en la `$edge_id` columna en el momento de creación de la tabla irregular, pero si uno no está creado, un valor predeterminado que automáticamente se crea el índice no agrupado único en Esta columna. Sin embargo, se crea un índice en una pseudocolumna del gráfico en las columnas subyacentes internas. Es decir, un índice creado en el `$edge_id` columna, aparecerá en el interno `graph_id_<hex_string>` columna. También se recomienda, para escenarios OLTP, que los usuarios crean un índice en (`$from_id`, `$to_id`) columnas para las búsquedas más rápidas en la dirección del borde.  

Figura 2 se muestra cómo se almacenan las tablas perimetrales y de nodo en la base de datos. 

![tablas de amigos de persona](../../relational-databases/graphs/media/person-friends-tables.png "nodo Person y amigos perimetral tablas")   

Figura 2: Representación de tabla de nodo y borde



## <a name="metadata"></a>Metadatos
Utilice estas vistas de metadatos para ver los atributos de una tabla de nodo o perimetral.
 
### <a name="systables"></a>sys.tables
Los siguientes nuevos, tipo de bit, se agregarán columnas sys. TABLAS. Si `is_node` está establecido en 1, que indica que la tabla es una tabla de nodo y si `is_edge` está establecido en 1, que indica que la tabla es una tabla irregular.
 
|Nombre de la columna |Tipo de datos |Descripción |
|--- |---|--- |
|is_node |bit |1 = se trata de una tabla de nodo |
|is_edge |bit |1 = se trata de una tabla irregular |
 
### <a name="syscolumns"></a>sys.columns
El `sys.columns` vista contiene columnas adicionales `graph_type` y `graph_type_desc`, que indican el tipo de la columna en las tablas perimetrales y de nodo.
 
|Nombre de la columna |Tipo de datos |Descripción |
|--- |---|--- |
|graph_type |INT |Columna interno con un conjunto de valores. Los valores están entre 1-8 para las columnas del gráfico y NULL para otros usuarios.  |
|graph_type_desc |nvarchar(60)  |columna interna con un conjunto de valores |
 
La tabla siguiente enumeran los valores válidos para `graph_type` columna

|Valor de columna  |Descripción  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` también almacena información acerca de las columnas implícitas creadas en las tablas de nodo o perimetral. Siguiendo la información se puede recuperar desde sys.columns, sin embargo, los usuarios no pueden seleccionar estas columnas de una tabla de nodo o perimetral. 

Columnas implícitas de una tabla de nodo

|Nombre de la columna    |Tipo de datos  |is_hidden  |Comentario  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |interno `graph_id` columna  |
|$node_id_\<hex_string> |NVARCHAR   |0  |Nodo externo `node_id` columna  |

Columnas implícitas de una tabla irregular

|Nombre de la columna    |Tipo de datos  |is_hidden  |Comentario  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |interno `graph_id` columna  |
|$edge_id_\<hex_string> |NVARCHAR   |0  |externo `edge_id` columna  |
|from_obj_id_\<hex_string>  |INT    |1  |interno del nodo `object_id`  |
|from_id_\<hex_string>  |bigint |1  |interno del nodo `graph_id`  |
|$from_id_\<hex_string> |NVARCHAR   |0  |externo del nodo `node_id`  |
|to_obj_id_\<hex_string>    |INT    |1  |interno de nodo `object_id`  |
|to_id_\<hex_string>    |bigint |1  |interno de nodo `graph_id`  |
|$to_id_\<hex_string>   |NVARCHAR   |0  |externo al nodo `node_id`  |
 
### <a name="system-functions"></a>Funciones del sistema
Se agregan las siguientes funciones integradas. Le ayudarán a los usuarios extraer información de las columnas generadas. Tenga en cuenta que, estos métodos no validará la entrada del usuario. Si el usuario especifica no es válido `sys.node_id` extraerá la parte adecuada y devolverlo al método. Por ejemplo, OBJECT_ID_FROM_NODE_ID tardará un `$node_id` como entrada y devolverá el object_id de la tabla, pertenece este nodo. 
 
|Integrada   |Descripción  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |Extraer el object_id de un `node_id`  |
|GRAPH_ID_FROM_NODE_ID  |Extraer el graph_id desde un `node_id`  |
|NODE_ID_FROM_PARTS |Construir un node_id desde un `object_id` y un `graph_id`  |
|OBJECT_ID_FROM_EDGE_ID |Extraer `object_id` desde `edge_id`  |
|GRAPH_ID_FROM_EDGE_ID  |Extraer la identidad de `edge_id`  |
|EDGE_ID_FROM_PARTS |Construir `edge_id` desde `object_id` e identidad  |



## <a name="transact-sql-reference"></a>Referencia de Transact-SQL 
Obtenga información sobre la [!INCLUDE[tsql-md](../../includes/tsql-md.md)] extensiones incluidas en SQL Server y Azure SQL Database, que permiten crear y consultar objetos de grafos. Las extensiones de lenguaje de consulta ayudan a consultas y recorren el grafo con la sintaxis de arte ASCII.
 
### <a name="data-definition-language-ddl-statements"></a>Instrucciones de lenguaje de definición (DDL) de datos

|Tarea   |Artículo relacionado  |Notas
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE ` Ahora se amplía para admitir la creación de una tabla como nodo o PERIMETRAL AS. Tenga en cuenta que una tabla perimetral puede o no tener ningún atributo definido por el usuario.  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|Se pueden modificar las tablas perimetrales y de nodo del mismo modo que una tabla relacional, usa el `ALTER TABLE`. Los usuarios pueden agregar o modificar las columnas definidas por el usuario, los índices o restricciones. Sin embargo, como la modificación de las columnas de gráfico interno, `$node_id` o `$edge_id`, se producirá un error.  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |Los usuarios pueden crear índices en columnas pseudo y definido por el usuario en las tablas perimetrales y de nodo. Se admiten todos los tipos de índices, incluidos los índices de almacén de columnas en clúster y no clúster.  |
|CREAR LAS RESTRICCIONES PERIMETRALES    |[EDGE CONSTRAINTS &#40;Transact-SQL&#41;](../../relational-databases/tables/graph-edge-constraints.md)  |Los usuarios pueden ahora crear las restricciones perimetrales en las tablas perimetrales para exigir la semántica específica y también mantener la integridad de datos  |
|DROP TABLE |[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |Se pueden quitar las tablas perimetrales y de nodo del mismo modo que una tabla relacional, usa el `DROP TABLE`. Sin embargo, en esta versión, no hay ninguna restricción para asegurarse de que ningún bordes apuntar a un nodo eliminado y no se admite la eliminación en cascada de bordes, tras la eliminación de un nodo o una tabla de nodo. Se recomienda que si se quita una tabla de nodo, los usuarios quitar los bordes que se conecta a los nodos de esa tabla de nodo manualmente para mantener la integridad del gráfico.  |


### <a name="data-manipulation-language-dml-statements"></a>Instrucciones de lenguaje de manipulación (DML) de datos

|Tarea   |Artículo relacionado  |Notas
|---  |---  |---  |
|INSERT |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|Insertar en una tabla de nodo no es diferente a insertar en una tabla relacional. Los valores de `$node_id` columna se genera automáticamente. Intentar insertar un valor en `$node_id` o `$edge_id` columna se producirá un error. Los usuarios deben proporcionar valores para `$from_id` y `$to_id` columnas al insertar en una tabla perimetral. `$from_id` y `$to_id` son el `$node_id` valores de los nodos que se conecta un borde determinado.  |
|SUPRIMIR | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|Datos de tablas de nodo o perimetral pueden eliminarse en la misma manera como se elimina de tablas relacionales. Sin embargo, en esta versión, no hay ninguna restricción para asegurarse de que ningún bordes apuntar a un nodo eliminado y no se admite la eliminación en cascada de bordes, tras la eliminación de un nodo. Se recomienda que cada vez que se elimina un nodo, todos los bordes de conexión a dicho nodo también se eliminan, para mantener la integridad del gráfico.  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |Los valores de columnas definido por el usuario pueden actualizarse mediante la instrucción UPDATE. Actualizando las columnas de gráfico interno `$node_id`, `$edge_id`, `$from_id` y `$to_id` no está permitido.  |
|MERGE |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` se admite la instrucción en una tabla de nodo o perimetral.  |


### <a name="query-statements"></a>Instrucciones de consulta

|Tarea   |Artículo relacionado  |Notas
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|Los nodos y bordes se almacenan internamente como tablas, por lo tanto, admite la mayoría de las operaciones admitidas en una tabla en SQL Server o Azure SQL Database en las tablas perimetrales y de nodo  |
|MATCH  | [MATCH &#40;Transact-SQL&#41;](../../t-sql/queries/match-sql-graph.md)|COINCIDENCIA integrados se introdujeron para admitir la coincidencia de patrones y recorrido a través del gráfico.  |



## <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos  
Existen ciertas limitaciones en las tablas perimetrales y de nodo en esta versión:
* Tablas temporales locales o globales no pueden ser tablas de nodo o perimetral.
* Tipos de tablas y las variables de tabla no se puede declarar como una tabla de nodo o perimetral. 
* No se puede crear tablas perimetrales y de nodo como tablas temporales con versión del sistema.   
* Las tablas perimetrales y de nodo no pueden ser tablas optimizadas para memoria.  
* Los usuarios no se pueden actualizar el `$from_id` y `$to_id` columnas de un borde mediante la instrucción UPDATE. Para actualizar los nodos que un borde conecta, los usuarios tendrán que inserte el borde nuevo que apunte a los nuevos nodos y elimine la anterior.
* Entre la base de datos no se admiten las consultas en objetos del gráfico. 


## <a name="next-steps"></a>Pasos siguientes
Para empezar a trabajar con la nueva sintaxis, vea [gráfico SQL Database: ejemplo](./sql-graph-sample.md)
 

