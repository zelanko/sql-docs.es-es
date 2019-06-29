---
title: Ruta de acceso más corta (gráfico SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
f1_keywords:
- SHORTEST PATH
- SHORTEST_PATH
dev_langs:
- TSQL
helpviewer_keywords:
- MATCH statement [SQL Server], SQL graph
- SQL graph, MATCH statement
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ef8f38acbf621a9c73a0d85bca579c8b7c87aa13
ms.sourcegitcommit: 9d3ece500fa0e4a9f4fefc88df4af1db9431c619
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463541"
---
# <a name="shortestpath-transact-sql"></a>SHORTEST_PATH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver2015-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  Especifica una condición de búsqueda para un gráfico, que es busca de forma recursiva o repetidamente. SHORTEST_PATH puede utilizarse dentro de MATCH con las tablas de nodo y borde gráfico, en la instrucción SELECT. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="shortest-path"></a>Ruta de acceso más corta
La función SHORTEST_PATH permite buscar:    
* Una ruta de acceso más corta entre dos nodos y las entidades especificadas
* Rutas de acceso más corta de origen único.
* Ruta de acceso más corta de varios nodos de origen a varios nodos de destino.

Toma un modelo de longitud arbitraria como entrada y devuelve una ruta de acceso más corta que existe entre dos nodos. Esta función sólo puede utilizarse dentro de MATCH. La función devuelve solo una ruta más corta entre dos nodos determinados. Si existe, dos o más rutas de acceso más corta de la misma longitud entre cualquier par de nodos de origen y destino, la función devuelve solo una ruta de acceso que se ha encontrado la primera durante el recorrido. Tenga en cuenta que, solo se puede especificar un patrón de longitud arbitraria dentro de una función SHORTEST_PATH. 

Hacer referencia a la [coincidencia (gráfico SQL)](../../t-sql/queries/match-sql-graph.md) para conocer la sintaxis. 

## <a name="for-path"></a>PARA LA RUTA DE ACCESO
PARA la ruta de acceso debe usarse con cualquier nombre de tabla de nodo o perimetral en la cláusula FROM, que se va a participar en un patrón de longitud arbitraria. PARA la ruta de acceso indica al motor que la tabla de nodo o perimetral devolverá una colección ordenada que representa la lista de nodos o bordes a lo largo del camino recorrido. Los atributos de dichas tablas no se puede proyectar directamente en la cláusula SELECT. Debe usarse al proyecto los atributos de estas tablas, funciones de agregado de la ruta de acceso del gráfico.  

## <a name="arbitrary-length-pattern"></a>Patrón de longitud arbitraria
Este patrón incluye los nodos y bordes que se deben recorrer repetidamente hasta que se alcance el nodo deseado o hasta que el número máximo de iteraciones que se especifica en el patrón se cumple. Cada vez que se ejecuta la consulta, el resultado de ejecutar este patrón será una colección ordenada de los nodos y bordes recorridos a lo largo de la ruta de acceso desde el nodo inicial al nodo final. Se trata de un modelo de sintaxis de estilo de expresión regular y se admiten los cuantificadores dos patrón siguiente:

* **‘+’** : Repita el patrón 1 o más veces. Finalizar tan pronto como se encuentra una ruta de acceso más corta.
* **{1,n}** : Repita el patrón 1 para "n" veces. Finalizar tan pronto como se encuentra una más corta.

## <a name="lastnode"></a>LAST_NODE
Función LAST_NODE() permite el encadenamiento de dos patrones de recorrido de longitud arbitraria. Se puede usar en escenarios donde:    
* Se utilizan varios patrones de ruta de acceso más corta en una consulta y un patrón comienza en el último nodo del patrón anterior.
* Combinación dos patrones de ruta de acceso más corta en el mismo LAST_NODE().

## <a name="graph-path-order"></a>Orden de la ruta de acceso de Graph
Orden de la ruta de acceso de gráfico hace referencia al orden de los datos en la ruta de acceso de salida. El orden de la ruta de acceso de salida siempre se inicia en la parte no recursiva del patrón seguido de los nodos/bordes que aparecen en la parte recursiva. El orden en el que se recorre el gráfico durante la ejecución de la optimización de consulta no tiene nada que ver con el orden que se imprime en la salida. De forma similar, la dirección de la flecha en el patrón recursivo también no influye en el orden de la ruta de acceso de gráfico. 

## <a name="graph-path-aggregate-functions"></a>Funciones de agregado de ruta de acceso de Graph
Puesto que los nodos y bordes implicada en el patrón de longitud arbitraria devuelto una colección (de nodos y bordes de esa ruta de acceso), los usuarios no pueden proyectar los atributos directamente mediante la sintaxis tablename.attributename convencional. Las consultas donde sea necesario para los valores de atributo de proyecto de las tablas de nodo o perimetral intermedias en la ruta de acceso atravesados, use el siguiente las funciones de agregado de ruta de acceso de gráfico: STRING_AGG, LAST_VALUE, SUM, AVG, MIN, MAX y COUNT. La sintaxis general para utilizar estas funciones de agregado en la cláusula SELECT es:

```
<GRAPH_PATH_AGGREGATE_FUNCTION>(<expression> , <separator>)  <order_clause>

    <order_clause> ::=
        { WITHIN GROUP (GRAPH PATH) }

    <GRAPH_PATH_AGGREGATE_FUNCTION> ::=
          STRING_AGG
        | LAST_VALUE
        | SUM
        | COUNT
        | AVG
        | MIN
        | MAX

```

### <a name="stringagg"></a>STRING_AGG
La función STRING_AGG toma una expresión y un separador como entrada y devuelve una cadena. Los usuarios pueden usar esta función en la cláusula SELECT para los atributos del proyecto desde los nodos intermedios o bordes en el camino recorrido. 

### <a name="lastvalue"></a>LAST_VALUE
Para los atributos del último nodo de ruta de acceso atravesado, función de agregado de LAST_VALUE se pueden usar el proyecto. Es un error para proporcionar el alias de la tabla perimetral como entrada a esta función, solo los nombres de tabla de nodo o se pueden usar el alias.

**Último nodo**: El último nodo hace referencia al nodo que aparece en último lugar en el camino recorrido, con independencia de la dirección de la flecha en el predicado de coincidencia. Por ejemplo: `MATCH(SHORTEST_PATH(n(-(e)->p)+) )`. Aquí el último nodo en la ruta de acceso será el último nodo P visitado. 

Mientras que el último nodo es el último nodo n en la ruta de acceso del gráfico de salida para este patrón: `MATCH(SHORTEST_PATH((n<-(e)-)+p))`    

### <a name="sum"></a>SUM
Esta función devuelve la suma de los valores de atributo de nodo o perimetral proporcionado o una expresión que aparece en la ruta de acceso recorrido.

### <a name="count"></a>COUNT
Esta función devuelve el número de valores distintos de null del atributo de nodo o borde deseado en la ruta de acceso. La función COUNT es compatible con el ' *' operador con un alias de tabla de nodo o perimetral. Sin el alias de tabla de nodo o perimetral, el uso de * es ambiguo y se producirá un error.

    {  COUNT( <expression> | <node_or_edge_alias>.* )  <order_clause>  }


### <a name="avg"></a>AVG
Devuelve el promedio de los valores de atributo de nodo o perimetral proporcionado o una expresión que aparece en la ruta de acceso recorrido.

### <a name="min"></a>MIN
Devuelve el valor mínimo de los valores de atributo de nodo o perimetral proporcionado expresión que aparece en la ruta de acceso recorrido.

### <a name="max"></a>MAX
Devuelve el valor máximo de los valores de atributo de nodo o perimetral proporcionado expresión que aparece en la ruta de acceso recorrido.

## <a name="remarks"></a>Comentarios  
función shortest_path sólo puede utilizarse dentro de MATCH.     
LAST_NODE solo se admite dentro de shortest_path.     
No se admite la búsqueda de ruta más corta ponderada, todas las rutas de acceso o todas las rutas de acceso más corta.         
En algunos casos, los planes incorrectos pueden generarse para consultas con mayor número de saltos, lo que resulta en tiempos de ejecución de consulta superior. Usar una sugerencia de combinación hash puede ayudar.    


## <a name="examples"></a>Ejemplos 
Para las consultas de ejemplo se muestra a continuación, vamos ot utilizan el nodo y las tablas perimetrales crean en [ejemplo de gráfico de SQL](./sql-graph-sample.md)

### <a name="a--find-shortest-path-between-2-people"></a>A.  Busque la ruta más corta entre las 2 personas
 En el ejemplo siguiente, encontramos una ruta más corta entre Jacob y Alicia. Necesitaremos el nodo Person y edge FriendOf creado a partir de script de ejemplo de gráfico. 

 ```
SELECT PersonName, Friends
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

 ### <a name="b--find-shortest-path-from-a-given-node-to-all-other-nodes-in-the-graph"></a>b.  Encontrar la ruta más corta de un nodo determinado en los demás nodos del gráfico. 
 El ejemplo siguiente busca todas las personas que Jacob está conectado en el gráfico y la ruta de acceso más corta a partir de Jacob a todas las personas. 

 ```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
AND Person1.name = 'Jacob'
 ```

### <a name="c--count-the-number-of-hopslevels-traversed-to-go-from-one-person-to-another-in-the-graph"></a>C.  Contar el número de saltos/niveles recorrido para pasar de una persona a otra en el gráfico.
 El siguiente ejemplo busca la ruta de acceso más corta entre Jacob y Alicia e imprime el número de saltos que se tarda en pasar de Jacob a Alice. 

 ```
 SELECT PersonName, Friends, levels
FROM (  
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        LAST_VALUE(Person2.name) WITHIN GROUP (GRAPH PATH) AS LastNode,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2)+))
    AND Person1.name = 'Jacob'
) AS Q
WHERE Q.LastNode = 'Alice'
 ```

### <a name="d-find-people-1-3-hops-away-from-a-given-person"></a>D. Buscar a personas saltos 1-3 de una persona determinada
El ejemplo siguiente busca la ruta de acceso más corta entre Jacob y todas las personas está conectado a en los saltos de gráfico 1-3 fuera de él. 

```
SELECT
    Person1.name AS PersonName, 
    STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends
FROM
    Person AS Person1,
    friendOf FOR PATH AS fo,
    Person FOR PATH  AS Person2
WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
AND Person1.name = 'Jacob'
```

### <a name="e-find-people-exactly-2-hops-away-from-a-given-person"></a>E. Buscar a personas exactamente 2 saltos de una persona determinada
El ejemplo siguiente busca la ruta de acceso más corta entre Jacob y las personas que son exactamente 2 saltos fuera de él en el gráfico. 

```
SELECT PersonName, Friends
FROM (
    SELECT
        Person1.name AS PersonName, 
        STRING_AGG(Person2.name, '->') WITHIN GROUP (GRAPH PATH) AS Friends,
        COUNT(Person2.name) WITHIN GROUP (GRAPH PATH) AS levels
    FROM
        Person AS Person1,
        friendOf FOR PATH AS fo,
        Person FOR PATH  AS Person2
    WHERE MATCH(SHORTEST_PATH(Person1(-(fo)->Person2){1,3}))
    AND Person1.name = 'Jacob'
) Q
WHERE Q.levels = 2
```

## <a name="see-also"></a>Vea también  
 [MATCH (gráfico SQL)](../../t-sql/queries/match-sql-graph.md)    
 [CREATE TABLE &#40;SQL Graph&#41;](../../t-sql/statements/create-table-sql-graph.md)   
 [INSERT (SQL Graph)](../../t-sql/statements/insert-sql-graph.md)]  
 [Graph processing with SQL Server 2017](../../relational-databases/graphs/sql-graph-overview.md) (Procesamiento de gráficos con SQL Server 2017)     
 
