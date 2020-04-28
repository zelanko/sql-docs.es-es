---
title: Guía del procesamiento de consultas para tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 065296fe-6711-4837-965e-252ef6c13a0f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34fdc72cfbb341e7b7d998a76036e6e2b060e7d8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "79112244"
---
# <a name="a-guide-to-query-processing-for-memory-optimized-tables"></a>Guía del procesamiento de consultas para tablas con optimización para memoria
  OLTP en memoria incluye en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] los procedimientos almacenados compilados de forma nativa y las tablas optimizadas para memoria. Este artículo proporciona información general del procesamiento de consultas tanto para las tablas optimizadas para memoria como para los procedimientos almacenados compilados de forma nativa.  
  
 En el documento se explica cómo se compilan y ejecutan las consultas en tablas optimizadas para memoria, incluido:  
  
-   La canalización de procesamiento de consultas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para las tablas basadas en disco.  
  
-   Optimización de consultas; el rol de las estadísticas en las tablas optimizadas para memoria así como instrucciones para solucionar problemas de planes de consulta no válidos.  
  
-   El uso de [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado para tener acceso a tablas optimizadas para memoria.  
  
-   Consideraciones sobre la optimización de consultas para el acceso a tablas optimizadas para memoria.  
  
-   Compilación y procesamiento de procedimientos almacenados de forma nativa.  
  
-   Estadísticas usadas para la estimación del costo por el optimizador.  
  
-   Formas de solucionar los planes de consulta no válidos.  
  
## <a name="example-query"></a>Consulta de ejemplo  
 El ejemplo siguiente se utilizará para mostrar los conceptos del procesamiento de consultas descritos en este artículo.  
  
 Consideramos dos tablas, Customer y Order. El siguiente script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] contiene las definiciones de estas dos tablas y los índices asociados, en su formato basado en disco (tradicional):  
  
```sql  
CREATE TABLE dbo.[Customer] (  
  CustomerID nchar (5) NOT NULL PRIMARY KEY,  
  ContactName nvarchar (30) NOT NULL   
)  
GO  
  
CREATE TABLE dbo.[Order] (  
  OrderID int NOT NULL PRIMARY KEY,  
  CustomerID nchar (5) NOT NULL,  
  OrderDate date NOT NULL  
)  
GO  
CREATE INDEX IX_CustomerID ON dbo.[Order](CustomerID)  
GO  
CREATE INDEX IX_OrderDate ON dbo.[Order](OrderDate)  
GO  
```  
  
 Para crear los planes de consulta mostrados en este artículo, las dos tablas se rellenaron con datos de ejemplo de la base de datos de ejemplo Northwind, que puede descargar desde [Bases de datos de ejemplo Northwind y pubs para SQL Server 2000](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs).  
  
 Considere la siguiente consulta, que combina las tablas Customer y Order y devuelve el identificador del pedido y la información del cliente asociada:  
  
```sql  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 El plan de ejecución estimado como se muestra en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] es el siguiente:  
  
 ![Plan de consulta para una combinación de tablas basadas en disco.](../../database-engine/media/hekaton-query-plan-1.gif "Plan de consulta para una combinación de tablas basadas en disco.")  
Plan de consulta para una combinación de tablas basadas en disco.  
  
 Acerca de este plan de consulta:  
  
-   Las filas de la tabla Customer se recuperan del índice clúster, que es la estructura de datos principal y tiene los datos completos de la tabla.  
  
-   Los datos de la tabla Order se recuperan usando el índice no agrupado en la columna CustomerID. Este índice contiene la columna CustomerID, que se utiliza para la combinación, y la columna de clave principal OrderID, que se devuelve al usuario. Devolver columnas adicionales de la tabla Order requeriría búsquedas en el índice clúster de la tabla Order.  
  
-   El operador físico `Inner Join` implementa el operador lógico `Merge Join`. Los otros tipos de combinación físicos son `Nested Loops` y `Hash Join`. El operador `Merge Join` se aprovecha del hecho de que ambos índices están ordenados por la columna de combinación CustomerID.  
  
 Considere una ligera variación en esta consulta, que devuelve todas las filas de la tabla Order, no solo OrderID:  
  
```sql  
SELECT o.*, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 El plan estimado de esta consulta es:  
  
 ![Plan de consulta para una combinación hash de tablas basadas en disco.](../../database-engine/media/hekaton-query-plan-2.gif "Plan de consulta para una combinación hash de tablas basadas en disco.")  
Plan de consulta para una combinación hash de tablas basadas en disco.  
  
 En esta consulta, las filas de la tabla Order se recuperan con el índice clúster. Ahora se utiliza el operador físico `Hash Match` para `Inner Join`. El índice clúster en la tabla Order no está ordenado en CustomerID y, por lo tanto, `Merge Join` requeriría un operador de ordenación, lo que afectaría al rendimiento. Tenga en cuenta el costo relativo del operador `Hash Match` (75 %) en comparación con el costo del operador `Merge Join` del ejemplo anterior (46 %). El optimizador habría considerado el operador `Hash Match` también en el ejemplo anterior pero concluyó que el operador `Merge Join` proporcionaba un rendimiento mejor.  
  
## <a name="ssnoversion-query-processing-for-disk-based-tables"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Procesamiento de consultas para las tablas basadas en disco  
 El siguiente diagrama muestra el flujo de procesamiento de consultas en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para las consultas ad hoc:  
  
 ![Canalización de procesamiento de consultas de SQL Server](../../database-engine/media/hekaton-query-plan-3.gif "Canalización de procesamiento de consultas de SQL Server")  
Canalización de procesamiento de consultas de SQL Server  
  
 En este escenario:  
  
1.  El usuario emite una consulta.  
  
2.  El analizador y el algebrizador construyen un árbol de consulta con operadores lógicos según el texto de [!INCLUDE[tsql](../../../includes/tsql-md.md)] enviado por el usuario.  
  
3.  El optimizador crea un plan de consulta optimizado que contiene los operadores físicos (por ejemplo, la combinación de bucles anidados). Después de la optimización, el plan se puede almacenar en la memoria caché de planes. Se omite este paso si la memoria caché de planes ya contiene un plan para esta consulta.  
  
4.  El motor de ejecución de consultas procesa una interpretación del plan de consulta.  
  
5.  Para cada operador de recorrido de tabla, búsqueda de índice y recorrido de índice, el motor de ejecución solicita las filas de las estructuras respectivas de índice y tabla de Access Methods.  
  
6.  Access Methods recupera las filas de las páginas de datos e índices del grupo de búferes y carga las páginas del disco al grupo de búferes según sea necesario.  
  
 Para la primera consulta del ejemplo, el motor de ejecución solicita filas del índice agrupado en la tabla Customer y el índice no agrupado en la tabla Order de Access Methods. Access Methods atraviesa las estructuras de índice del árbol B para recuperar las filas solicitadas. En este caso, todas las filas se recuperan como las llamadas de plan para los recorridos de índice completos.  
  
## <a name="interpreted-tsql-access-to-memory-optimized-tables"></a>Acceso de [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado a las tablas con optimización para memoria  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] también se denominan [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Interpretado hace referencia al hecho de que el plan de consulta es interpretado por el motor de ejecución de consulta para cada operador del plan de consultas. El motor de ejecución lee el operador y sus parámetros y realiza la operación.  
  
 [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado se puede utilizar para tener acceso a tablas optimizadas para memoria y a tablas basadas en disco. La ilustración siguiente muestra el procesamiento de consultas para el acceso de [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado a las tablas optimizadas para memoria:  
  
 ![Canalización de procesamiento de consulta para tsql interpretado.](../../database-engine/media/hekaton-query-plan-4.gif "Canalización de procesamiento de consulta para tsql interpretado.")  
Canalización de procesamiento de consultas para acceso de Transact-SQL interpretado a tablas optimizadas para memoria.  
  
 Como se muestra en la ilustración, la canalización del procesamiento de consultas permanece principalmente sin cambios:  
  
-   El analizador y el algebrizador construyen el árbol de consulta.  
  
-   El optimizador crea el plan de ejecución.  
  
-   El motor de ejecución de consultas interpreta el plan de ejecución.  
  
 La diferencia principal con la canalización de procesamiento de consultas tradicional (la ilustración 2) es que las filas de las tablas optimizadas para memoria no se recuperan del grupo de búferes mediante Access Methods. En su lugar, las filas se recuperan de las estructuras de datos en memoria a través del motor OLTP en memoria. Las diferencias en las estructuras de datos hacen que el optimizador elija distintos planes en algunos casos, como se muestra en el ejemplo siguiente.  
  
 El siguiente script de [!INCLUDE[tsql](../../../includes/tsql-md.md)] contiene las versiones optimizadas para memoria de las tablas Order y Customer, con índices hash:  
  
```sql  
CREATE TABLE dbo.[Customer] (  
  CustomerID nchar (5) NOT NULL PRIMARY KEY NONCLUSTERED,  
  ContactName nvarchar (30) NOT NULL   
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
CREATE TABLE dbo.[Order] (  
  OrderID int NOT NULL PRIMARY KEY NONCLUSTERED,  
  CustomerID nchar (5) NOT NULL INDEX IX_CustomerID HASH(CustomerID) WITH (BUCKET_COUNT=100000),  
  OrderDate date NOT NULL INDEX IX_OrderDate HASH(OrderDate) WITH (BUCKET_COUNT=100000)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
```  
  
 Considere la misma consulta ejecutada en tablas optimizadas para memoria:  
  
```sql  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 El plan estimado es el siguiente:  
  
 ![Plan de consulta para una combinación de tablas con optimización para memoria.](../../database-engine/media/hekaton-query-plan-5.gif "Plan de consulta para una combinación de tablas optimizadas para memoria.")  
Plan de consulta para una combinación de tablas optimizadas para memoria.  
  
 Observe las siguientes diferencias con el plan para la misma consulta en las tablas basadas en disco (ilustración 1):  
  
-   Este plan contiene un recorrido de tabla en lugar de un recorrido de índice clúster para la tabla Customer:  
  
    -   La definición de la tabla no contiene un índice clúster.  
  
    -   Los índices clúster no se admiten con tablas optimizadas para memoria. En su lugar, cada tabla optimizada para memoria debe tener al menos un índice no clúster y todos los índices de las tablas optimizadas para memoria pueden tener acceso eficazmente a todas las columnas de la tabla sin tener que almacenarlas en el índice o hacer referencia a un índice clúster.  
  
-   Este plan contiene una `Hash Match` en lugar de una `Merge Join`. Los índices en las tablas Order y Customer son índices hash y, por tanto, no se ordenan. Una `Merge Join` requeriría operadores de ordenación que reducirían el rendimiento.  
  
## <a name="natively-compiled-stored-procedures"></a>procedimientos almacenados compilados de forma nativa  
 Los procedimientos almacenados compilados de forma nativa son procedimientos almacenados de [!INCLUDE[tsql](../../../includes/tsql-md.md)] compilados con código máquina, en lugar de interpretados por el motor de ejecución de consultas. El siguiente script crea un procedimiento almacenado compilado de forma nativa que ejecuta la consulta de ejemplo (de la sección Consulta de ejemplo).  
  
```sql  
CREATE PROCEDURE usp_SampleJoin  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = 'english')  
  
  SELECT o.OrderID, c.CustomerID, c.ContactName   
FROM dbo.[Order] o INNER JOIN dbo.[Customer] c   
  ON c.CustomerID = o.CustomerID  
  
END  
```  
  
 Los procedimientos almacenados compilados de forma nativa se compilan en el momento de su creación, mientras que los procedimientos almacenados interpretados se compilan la primera vez que se ejecutan. (Una parte de la compilación, en particular el análisis y la algebrización, tienen lugar en la creación. Sin embargo, para los procedimientos almacenados interpretados, la optimización de los planes de consulta tiene lugar en la primera ejecución). La lógica de la recompilación es similar. Los procedimientos almacenados compilados de forma nativa se recompilan en la primera ejecución del procedimiento si el servidor se reinicia. Los procedimientos almacenados interpretados se recompilan si el plan ya no está en la memoria caché de planes. En la tabla siguiente se resumen los casos de compilación y de recompilación tanto para los procedimientos almacenados interpretados como para los compilados de forma nativa:  
  
||Compilado de forma nativa|Acceso de|  
|-|-----------------------|-----------------|  
|Compilación inicial|En el momento de la creación.|En la primera ejecución.|  
|Recompilación automática|En la primera ejecución del procedimiento después del reinicio de la base de datos o del servidor.|Al reiniciar el servidor. O bien, se expulsa de la memoria caché de planes, generalmente según los cambios de esquema o de estadísticas, o por presión en la memoria.|  
|Recompilación manual|No se admite. La solución es quitar y volver a crear el procedimiento almacenado.|Mediante `sp_recompile`. Puede expulsar manualmente el plan de la memoria caché, por ejemplo con DBCC FREEPROCCACHE. También puede crear el procedimiento almacenado WITH RECOMPILE y el procedimiento almacenado se recompilará en cada ejecución.|  
  
### <a name="compilation-and-query-processing"></a>Compilación y procesamiento de consultas  
 El siguiente diagrama muestra el proceso de compilación para los procedimientos almacenados compilados de forma nativa:  
  
 ![Compilación nativa de procedimientos almacenados.](../../database-engine/media/hekaton-query-plan-6.gif "Compilación nativa de procedimientos almacenados.")  
Compilación nativa de procedimientos almacenados.  
  
 El proceso se describe como  
  
1.  El usuario emite una instrucción `CREATE PROCEDURE` a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
2.  El analizador y el algebrizador crean el flujo de procesamiento del procedimiento, así como los árboles de consulta para las consultas de [!INCLUDE[tsql](../../../includes/tsql-md.md)] del procedimiento almacenado.  
  
3.  El optimizador crea planes optimizados de ejecución de consultas para todas las consultas en el procedimiento almacenado.  
  
4.  El compilador OLTP en memoria toma el flujo de procesamiento con los planes de consulta optimizados incrustados y genera un archivo DLL que contiene el código máquina para ejecutar el procedimiento almacenado.  
  
5.  El archivo DLL generado se carga en memoria.  
  
 La invocación de un procedimiento almacenado compilado de forma nativa se traduce en la llamada a una función del archivo DLL.  
  
 ![Ejecución de los procedimientos almacenados compilados de forma nativa.](../../database-engine/media/hekaton-query-plan-7.gif "Ejecución de los procedimientos almacenados compilados de forma nativa.")  
Ejecución de los procedimientos almacenados compilados de forma nativa.  
  
 La invocación de un procedimiento almacenado compilado de forma nativa se describe como sigue:  
  
1.  El usuario emite una `EXEC`instrucción *usp_myproc* .  
  
2.  El analizador extrae los parámetros del nombre y del procedimiento almacenado.  
  
     Si la instrucción se preparó, por ejemplo con `sp_prep_exec`, el analizador no necesita extraer el nombre y los parámetros de los procedimientos en tiempo de ejecución.  
  
3.  El runtime de OLTP en memoria encuentra el punto de entrada del archivo DLL para el procedimiento almacenado.  
  
4.  El código máquina del archivo DLL se ejecuta y los resultados se devuelven al cliente.  
  
 **Examen de parámetros**  
  
 Los procedimientos almacenados de [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado se compilan en la primera ejecución, a diferencia de los procedimientos almacenados compilados de forma nativa, que se compilan en el momento de su creación. Cuando los procedimientos almacenados interpretados se compilan al invocarlos, el optimizador usa los valores de los parámetros proporcionados para esta invocación al generar el plan de ejecución. Este uso de parámetros durante la compilación se denomina examen de parámetros.  
  
 El examen de parámetros no se utiliza para compilar procedimientos almacenados compilados de forma nativa. Todos los parámetros para el procedimiento almacenado se considera que tienen valores UNKNOWN. Al igual que sucede con los procedimientos almacenados interpretados, los procedimientos almacenados compilados de forma nativa también admiten la sugerencia `OPTIMIZE FOR`. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query).  
  
### <a name="retrieving-a-query-execution-plan-for-natively-compiled-stored-procedures"></a>Recuperar un plan de ejecución de consultas para los procedimientos almacenados compilados de forma nativa  
 El plan de ejecución de consulta para un procedimiento almacenado compilado de forma nativa se puede recuperar con un **Plan de ejecución estimado** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]o con la opción SHOWPLAN_XML en [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Por ejemplo:  
  
```sql  
SET SHOWPLAN_XML ON  
GO  
EXEC dbo.usp_myproc  
GO  
SET SHOWPLAN_XML OFF  
GO  
```  
  
 El plan de ejecución generado por el optimizador de consultas está compuesto de un árbol con operadores de consulta en los nodos y en las hojas de árbol. La estructura del árbol determina la interacción (el flujo de filas de un operador a otro) entre los operadores. En la vista gráfica de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], el flujo es de derecha a izquierda. Por ejemplo, el plan de consulta de la ilustración 1 contiene dos operadores de examen de índices, lo que proporciona filas para un operador de combinación de mezcla. El operador merge join proporciona filas para un operador select. El operador select, finalmente, devuelve las filas al cliente.  
  
### <a name="query-operators-in-natively-compiled-stored-procedures"></a>Operadores de consulta en procedimientos almacenados compilados de forma nativa  
 En la tabla siguiente se resumen los operadores de consulta admitidos dentro de procedimientos almacenados compilados de forma nativa:  
  
|Operator|Consulta de ejemplo|  
|--------------|------------------|  
|SELECT|`SELECT OrderID FROM dbo.[Order]`|  
|INSERT|`INSERT dbo.Customer VALUES ('abc', 'def')`|  
|UPDATE|`UPDATE dbo.Customer SET ContactName='ghi' WHERE CustomerID='abc'`|  
|Delete|`DELETE dbo.Customer WHERE CustomerID='abc'`|  
|Compute Scalar|Este operador se usa tanto para las funciones intrínsecas como para las conversiones de tipos. No todas las funciones y conversiones de tipos se admiten en los procedimientos almacenados compilados de forma nativa.<br /><br /> `SELECT OrderID+1 FROM dbo.[Order]`|  
|Combinación de bucles anidados|Nested Loops es el único operador de combinación admitido en los procedimientos almacenados compilados de forma nativa. Todos los planes que contienen combinaciones utilizarán el operador Nested Loops, incluso si el plan para la misma consulta ejecutada como [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado contiene una combinación de mezcla o hash.<br /><br /> `SELECT o.OrderID, c.CustomerID`  <br /> `FROM dbo.[Order] o INNER JOIN dbo.[Customer] c`|  
|Sort|`SELECT ContactName FROM dbo.Customer`  <br /> `ORDER BY ContactName`|  
|TOP|`SELECT TOP 10 ContactName FROM dbo.Customer`|  
|Top-sort|La expresión `TOP` (número de filas que se van a devolver) no puede superar 8000 filas. Si hay también en la consulta operadores de combinación y agregación, habrá menos filas. Las combinaciones y agregaciones suelen reducir el número de filas que se van a ordenar, en comparación con el recuento de filas de las tablas base.<br /><br /> `SELECT TOP 10 ContactName FROM dbo.Customer`  <br /> `ORDER BY ContactName`|  
|Stream Aggregate|Observe que el operador Hash Match no se admite para la agregación. Por consiguiente, toda la agregación en los procedimientos almacenados compilados de forma nativa utiliza el operador Stream Aggregate, incluso si el plan para la misma consulta en [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado utiliza el operador Hash Match.<br /><br /> `SELECT count(CustomerID) FROM dbo.Customer`|  
  
## <a name="column-statistics-and-joins"></a>Combinaciones y estadísticas de columnas  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mantiene estadísticas en los valores de columnas de clave de índice para ayudar a evaluar el costo de ciertas operaciones, como el examen de índice y las búsquedas de índice. ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] también crea estadísticas en columnas de clave sin índice si se crean explícitamente o si el optimizador de consultas las crea en respuesta a una consulta con predicado). La métrica principal en la estimación del costo es el número de filas procesadas por un único operador. Tenga en cuenta que para las tablas basadas en disco, el número de páginas a las que tiene acceso un operador determinado es importante en la estimación de costos. Sin embargo, como el recuento de páginas no es importante para las tablas optimizadas para memoria (siempre es cero), esta explicación se centra en el recuento de filas. La estimación comienza por los operadores de examen y búsqueda de índice en el plan, y se extiende después para incluir los otros operadores, como el operador de combinación. El número estimado de filas que va a procesar un operador de combinación se basa en la estimación de los operadores de examen, índice y búsqueda subyacentes. Para que [!INCLUDE[tsql](../../../includes/tsql-md.md)] interpretado pueda obtener acceso a las tablas optimizadas para memoria, puede seguir el plan de ejecución real para ver la diferencia entre los recuentos de filas estimado y real de los operadores del plan.  
  
 Para el ejemplo en la ilustración 1,  
  
-   El examen de índice clúster en Customer ha estimado 91; reales 91.  
  
-   El examen de índice no clúster en CustomerID ha estimado 830; reales 830.  
  
-   El operador Merge Join ha estimado 815; reales 830.  
  
 Las estimaciones de los exámenes de índice son precisas. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mantiene el recuento de filas en las tablas basadas en disco. Las estimaciones para los recorridos de índice y de la tabla completa siempre son precisas. La estimación de la combinación es bastante precisa también.  
  
 Si estas estimaciones cambian, las consideraciones de costo para las diferentes alternativas de plan también cambian. Por ejemplo, si uno de los lados de la combinación tiene un recuento estimado de filas de 1 o menos, usar las combinaciones de bucles anidados es menos costoso.  
  
 A continuación se muestra el plan de la consulta:  
  
```  
SELECT o.OrderID, c.* FROM dbo.[Customer] c INNER JOIN dbo.[Order] o ON c.CustomerID = o.CustomerID  
```  
  
 Después de eliminar todas las filas menos una en la tabla Customer:  
  
 ![Combinaciones y estadísticas de columnas.](../../database-engine/media/hekaton-query-plan-9.gif "Combinaciones y estadísticas de columnas.")  
  
 Acerca de este plan de consulta:  
  
-   Hash Match se ha reemplazado por un operador de combinación anidada Nested Loops.  
  
-   El examen de índice completo en IX_CustomerID se ha reemplazado por index seek. Esto provocó el examen de 5 filas en lugar de las 830 necesarias para el examen de índice completo.  
  
### <a name="statistics-and-cardinality-for-memory-optimized-tables"></a>Estadísticas y cardinalidad para las tablas con optimización para memoria  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mantiene las estadísticas de nivel de columna de las tablas optimizadas para memoria. Además, mantiene el recuento de filas real de la tabla. Sin embargo, a diferencia de las tablas basadas en disco, las estadísticas de las tablas optimizadas para memoria no se actualizan automáticamente. Por tanto, las estadísticas se deben actualizar manualmente cuando se produzcan cambios significativos en las tablas. Para obtener más información, vea [Estadísticas para las tablas con optimización para memoria](memory-optimized-tables.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tablas con optimización para memoria](memory-optimized-tables.md)  
  
  
