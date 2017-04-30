---
title: "Índices de hash de tablas con optimización para memoria | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 08/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e922cc3a-3d6e-453b-8d32-f4b176e98488
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: de23d5625c883792f5c99de75dc90ccd1cabe326
ms.lasthandoff: 04/11/2017

---
# <a name="hash-indexes-for-memory-optimized-tables"></a>Índices de hash de tablas con optimización para memoria
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
En este artículo se describen los tipos de índice de *hash* disponibles para una tabla con optimización para memoria. El artículo:  
  
- Ofrece ejemplos de código corto que muestran la sintaxis de Transact-SQL.  
- Describe los aspectos básicos de los índices de hash.  
- Describe [cómo estimar un número de depósitos apropiado](#configuring_bucket_count).  
- Describe cómo diseñar y administrar los índices de hash.  
  
  
#### <a name="prerequisite"></a>Requisito previo  
  
Encontrará información de contexto importante para comprender este artículo en:  
  
- [Índices de tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. Sintaxis de índices con optimización para memoria  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 Ejemplo de código para sintaxis  
  
En este apartado se incluye un bloque de código de Transact-SQL que muestra las sintaxis disponibles para crear varios índices de hash en una tabla con optimización para memoria:  
  
- En el ejemplo se muestra que el índice de hash se declara dentro de la instrucción CREATE TABLE.  
  - En su lugar, puede declararlo en otra instrucción [ALTER TABLE...ADD INDEX](#h3-b2-declaration-limitations) .  
  
  
  
    DROP TABLE IF EXISTS SupportEventHash;  
    go  
      
    CREATE TABLE SupportIncidentRating_Hash  
    (  
      SupportIncidentRatingId   int      not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
      
      RatingLevel          int           not null,  
      
      SupportEngineerName  nvarchar(16)  not null,  
      Description          nvarchar(64)      null,  
      
      INDEX ix_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 100000)  
    )  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_ONLY);  
    go  
  

Para determinar el `BUCKET_COUNT` correcto para los datos, consulte [Configuración del número de depósitos de índice de hash](#configuring_bucket_count). 
  
## <a name="b-hash-indexes"></a>B. Índices de hash  
  
  
### <a name="b1-performance-basics"></a>B.1 Conceptos básicos de rendimiento  
  
El rendimiento de un índice de hash es:  
  
- Excelente cuando la cláusula WHERE contiene un valor *exacto* para cada columna de la clave de índice de hash.  
- Deficiente cuando la cláusula WHERE busca un *rango* de valores en la clave de índice.  
- Deficiente cuando la cláusula WHERE contiene un valor concreto para la primera columna de una clave de índice de hash de dos columnas, pero no para la *segunda* columna de la clave.  
  
  
<a name="h3-b2-declaration-limitations"></a>  
  
### <a name="b2-declaration-limitations"></a>B.2 Limitaciones de declaración  
  
Solo puede existir un índice de hash en una tabla con optimización para memoria. No puede existir en una tabla basada en disco.  
  
Un índice de hash se puede declarar como:  
  
- UNIQUE, o puede establecerse de forma predeterminada en Nonunique.  
- NONCLUSTERED, que es el valor predeterminado.   
  
  
Aquí se muestra una sintaxis de ejemplo para crear un índice de hash fuera de la instrucción CREATE TABLE:  
  
  
    ALTER TABLE MyTable_memop  
      ADD INDEX ix_hash_Column2 UNIQUE  
        HASH (Column2) WITH (BUCKET_COUNT = 64);  
  
  
  
### <a name="b3-buckets-and-hash-function"></a>B.3 Depósitos y función hash  
  
Un índice de hash delimita sus valores de clave en lo que llamamos una matriz de *depósitos* :  
  
- Cada depósito tiene 8 bytes, que se usan para almacenar la dirección de memoria de una lista de vínculos de entradas de índice.  
- Cada entrada es un valor correspondiente a una clave de índice, además de la dirección de su fila correspondiente en la tabla subyacente con optimización para memoria.  
  - Cada entrada apunta a la siguiente entrada en una lista de vínculos de entradas, todas ellas encadenadas al depósito actual.  
  
  
El algoritmo hash intenta distribuir todos los valores de clave únicos o distintos uniformemente entre los depósitos, pero la uniformidad total es imposible de lograr. Todas las instancias de un valor de clave determinado están encadenadas al mismo depósito. El depósito puede tener también una mezcla de todas las instancias de otro valor de clave.  
  
- Esta mezcla se conoce como *colisión de hash*. Las colisiones son frecuentes, pero no ideales.  
- Un objetivo realista es que el 30 % de los cubos contengan dos valores de clave diferentes.  
  
  
Hay que declarar cuántos depósitos debe tener el índice de hash.  
  
- Cuanto menor sea la proporción de depósitos con respecto a las filas de la tabla o valores distintos, mas larga será la lista de vínculos de depósito promedio.  
- Las listas de vínculos cortas se ejecutan más rápidamente que las listas de vínculos largas.  
  
  
SQL Server tiene una función hash que usa para todos los índices de hash:  
  
- La función hash es determinista: dado el mismo valor de clave de entrada, genera sistemáticamente la misma ranura de cubo.  
- Con llamadas repetidas, las salidas de la función hash suelen formar una distribución de curva de campana o Poisson, no una distribución plana lineal.  
  
  
La interacción del índice de hash y los cubos se resume en la siguiente imagen.  
  
  
![hekaton_tables_23d](../../relational-databases/in-memory-oltp/media/hekaton-tables-23d.png "Claves de índice, entrada en una función hash, el resultado es la dirección de un depósito de hash, que señala al principio de la cadena.")  
  
  
  
### <a name="b4-row-versions-and-garbage-collection"></a>B.4 Versiones de fila y recolección de elementos no utilizados  
  
  
En una tabla con optimización para memoria, cuando una fila se ve afectada por una instrucción UPDATE de SQL, la tabla crea una versión actualizada de la fila. Durante la transacción de actualización, es posible que otras sesiones puedan leer la versión anterior de la fila y, por tanto, evitar la degradación del rendimiento asociada a un bloqueo de fila.  
  
Puede que el índice de hash también tenga versiones diferentes de las entradas para dar cabida a la actualización.  
  
Más adelante cuando las versiones anteriores ya no se necesiten, un subproceso de recolección de elementos no utilizados (GC) recorre transversalmente los cubos y sus listas de vínculos para eliminar las entradas más antiguas. El subproceso GC funciona mejor si las longitudes de cadena de las listas de vínculo son cortas.   
  
<a name="configuring_bucket_count"></a>
  
## <a name="c-configuring-the-hash-index-bucket-count"></a>C. Configuración del número de depósitos de índice de hash  
  
El número de depósitos de índice de hash se especifica al crear el índice y se puede modificar con la sintaxis ALTER TABLE...ALTER INDEX REBUILD.  
  
En la mayoría de los casos, lo ideal es que el número de depósitos esté entre 1 y 2 veces el número de valores distintos de la clave de índice.   
No podrá siempre predecir cuántos valores puede tener o tendrá una clave de índice determinada. El rendimiento sigue siendo bueno por lo general si el valor **BUCKET_COUNT** está dentro de 10 veces el número real de valores de clave. A este respecto, suele ser mejor realizar estimaciones por lo alto que por lo bajo.  
  
Un número muy *pequeño* de cubos tiene las siguientes desventajas:  
  
- Más colisiones de hash de valores de clave distintos.  
  - Cada valor distinto está obligado a compartir el mismo cubo con otro valor distinto.  
  - Aumenta el promedio de longitud de cadena por cubo.  
  - Cuanto más larga sea la cadena de depósitos, menor será la velocidad de búsquedas de igualdad en el índice.  
  
Un número muy *alto* de cubos tiene las siguientes desventajas::  
  
- Un número excesivo de depósitos puede generar más depósitos vacíos.  
  - Los depósitos vacíos repercuten en el rendimiento de los exámenes de índice completos. Si se realizan con frecuencia, inclínese por un número de depósitos cercano al número de valores de clave de índice distintos.  
  - Los depósitos vacíos usan la memoria, aunque cada depósito emplea únicamente 8 bytes.  
    
  
> [!NOTE]
> Agregar más depósitos no hace nada para reducir el encadenamiento de entradas que comparten un valor duplicado. La tasa de duplicación de valores sirve para decidir si un tipo de índice de hash es el adecuado, no para calcular el número de depósitos.  
  
  
  
### <a name="c1-practical-numbers"></a>C.1 Números prácticos  
  
Aunque el **BUCKET_COUNT** esté moderadamente por debajo o por encima del rango preferido, es probable que el rendimiento del índice de hash sea tolerable o aceptable. No se crea ninguna crisis.  
  
Asigne al índice de hash un **BUCKET_COUNT** aproximadamente igual al número de filas que prevé que terminará teniendo la tabla con optimización para memoria.  
  
Suponga que la tabla en aumento tiene 2 000 000 filas, pero prevé que dicha cantidad crecerá 10 veces hasta 20 000 000 filas. Comience por un número de depósitos que sea 10 veces el número de filas de la tabla. Esto deja espacio para una mayor cantidad de filas.  
  
- Lo ideal es aumentar el número de depósitos cuando la cantidad de filas alcanza el número de depósitos inicial.  
- Aunque la cantidad de filas aumente hasta 5 veces más que el número de depósitos, el rendimiento seguirá siendo bueno casi siempre.  
  
Suponga que un índice de hash tiene 10 000 000 valores de claves distintos.  
  
- Un número de depósitos de 2 000 000 sería la menor cantidad que podría aceptar. El grado de degradación del rendimiento puede ser tolerable.  
  
### <a name="c2-too-many-duplicate-values-in-the-index"></a>C.2 ¿Demasiados valores duplicados en el índice?  
  
Si los valores de hash indizados tienen una alta tasa de duplicados, los depósitos de hash toleran cadenas más largas.  
  
Suponga que tiene la misma tabla SupportEvent del bloque de código anterior de la sintaxis de T-SQL. El código de T-SQL siguiente muestra cómo buscar y mostrar la proporción de *todos* los valores con respecto a los valores *únicos* :  
  
        -- Calculate ratio of:  Rows / Unique_Values.  
    DECLARE @allValues float(8) = 0.0, @uniqueVals float(8) = 0.0;  
      
    SELECT @allValues = Count(*) FROM SupportEvent;  
      
    SELECT @uniqueVals = Count(*) FROM  
      (SELECT DISTINCT SupportEngineerName  
         FROM SupportEvent) as d;  
      
        -- If (All / Unique) >= 10.0, use a nonclustered index, not a hash.   
    SELECT Cast((@allValues / @uniqueVals) as float) as [All_divby_Unique];  
    go  
  
- Una proporción de 10,0 o superior significa que un tipo de índice de hash sería deficiente. Sopese la posibilidad de usar un índice no agrupado en su lugar.   
  
## <a name="d-troubleshooting-hash-index-bucket-count"></a>D. Solución de problemas de número de depósitos de índice de hash  
  
En esta sección se explica cómo resolver problemas relativos al número de depósitos del índice de hash.  
  
### <a name="d1-monitor-statistics-for-chains-and-empty-buckets"></a>D.1 Supervisión de estadísticas de cadenas y depósitos vacíos  
  
Puede supervisar el mantenimiento estadístico de los índices de hash ejecutando la siguiente instrucción SELECT de T-SQL. SELECT usa la vista de administración de datos (DMV) denominada **sys.dm_db_xtp_hash_index_stats**.  
  
  
```t-sql
  SELECT  
    QUOTENAME(SCHEMA_NAME(t.schema_id)) + N'.' + QUOTENAME(OBJECT_NAME(h.object_id)) as [table],   
    i.name                   as [index],   
    h.total_bucket_count,  
    h.empty_bucket_count,  
      
    FLOOR((  
      CAST(h.empty_bucket_count as float) /  
        h.total_bucket_count) * 100)  
                             as [empty_bucket_percent],  
    h.avg_chain_length,   
    h.max_chain_length  
  FROM  
         sys.dm_db_xtp_hash_index_stats  as h   
    JOIN sys.indexes                     as i  
            ON h.object_id = i.object_id  
           AND h.index_id  = i.index_id  
    JOIN sys.memory_optimized_tables_internal_attributes ia ON h.xtp_object_id=ia.xtp_object_id
    JOIN sys.tables t on h.object_id=t.object_id
  WHERE ia.type=1
  ORDER BY [table], [index];  
```
  
  
Compare los resultados de SELECT con las siguientes directrices estadísticas:  
  
- Depósitos vacíos:  
  - 33 % es un buen valor de destino, pero un porcentaje mayor (incluso el 90 %) suele funcionar correctamente.  
  - Cuando el número de depósitos es igual al número de valores de clave distintos, aproximadamente un 33 % de los cubos están vacíos.  
  - Un valor inferior al 10 % es demasiado bajo.  
- Cadenas dentro de cubos:  
  - Una longitud media de cadena de 1 es ideal en caso de que no haya valores de clave de índice duplicados. Las longitudes de cadena de hasta 10 suelen ser aceptables.  
  - Si la longitud promedio de la cadena es superior a 10 y el porcentaje de depósitos vacíos es superior al 10 %, los datos tienen tantos duplicados que es posible que un índice de hash no sea el tipo más adecuado.  
  

  
### <a name="d2-demonstration-of-chains-and-empty-buckets"></a>D.2 Demostración de cadenas y depósitos vacíos  
  
  
El siguiente bloque de código de T-SQL constituye un sencillo método de comprobar una instrucción `SELECT * FROM sys.dm_db_xtp_hash_index_stats;`. El bloque de código se completa en 1 minuto. Estas son las fases del código de bloque en cuestión:  
  
  
1. Crea una tabla con optimización para memoria que tiene algunos índices hash.  
2. Rellena la tabla con miles de filas.  
    A. Se usa un operador de módulo para configurar la tasa de valores duplicados en la columna StatusCode.  
    B. Con INSERT el bucle inserta 262 144 filas en aproximadamente 1 minuto.  
3. PRINT imprime un mensaje pidiéndole que ejecute la instrucción SELECT anterior en **sys.dm_db_xtp_hash_index_stats**.  
  
  
```t-sql
    DROP TABLE IF EXISTS SalesOrder_Mem;  
    go  
      
      
    CREATE TABLE SalesOrder_Mem  
    (  
      SalesOrderId   uniqueidentifier  NOT NULL  DEFAULT newid(),  
      OrderSequence  int               NOT NULL,  
      OrderDate      datetime2(3)      NOT NULL,  
      StatusCode     tinyint           NOT NULL,  
      
      PRIMARY KEY NONCLUSTERED  
          HASH (SalesOrderId)  WITH (BUCKET_COUNT = 262144),  
      
      INDEX ix_OrderSequence  
          HASH (OrderSequence) WITH (BUCKET_COUNT = 20000),  
      
      INDEX ix_StatusCode  
          HASH (StatusCode)    WITH (BUCKET_COUNT = 8),  
      
      INDEX ix_OrderDate       NONCLUSTERED (OrderDate DESC)  
    )  
      WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
    go  
      
        --------------------  
      
    SET NoCount ON;  
      
      -- Same as PK bucket_count.  68 seconds to complete.  
    DECLARE @i int = 262144;  
      
    BEGIN TRANSACTION;  
      
    WHILE @i > 0  
    Begin  
      
      INSERT SalesOrder_Mem  
          (OrderSequence, OrderDate, StatusCode)  
        Values  
          (@i, GetUtcDate(), @i % 8);  -- Modulo technique.  
      
      SET @i -= 1;  
    End  
    COMMIT TRANSACTION;  
      
    PRINT 'Next, you should query:  sys.dm_db_xtp_hash_index_stats .';  
    go  
```  
  
  
El bucle INSERT anterior hace lo siguiente:  
  
- Inserta valores únicos en el índice de clave principal y en ix_OrderSequence.  
- Inserta un par de cientos de miles de filas que solo representan 8 valores distintos para StatusCode. Por lo tanto, hay una alta tasa de duplicación de valores en el índice ix_StatusCode.  
  
Para solucionar problemas cuando el número de depósitos no es óptimo, examine la salida siguiente de la instrucción SELECT en **sys.dm_db_xtp_hash_index_stats**. Para estos resultados, hemos agregado `WHERE Object_Name(h.object_id) = 'SalesOrder_Mem'` a la instrucción SELECT que copiamos de la sección D.1.  
  
  
  
Los resultados de nuestra instrucción SELECT se muestran después del código, divididos artificialmente en dos tablas de resultados más estrechas para poder verlos mejor.  
  
- Estos son los resultados del *número de depósitos*.  
  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent |  
| :-------- | -----------------: | -----------------: | -----------------: |  
| ix_OrderSequence | 32768 | 13 | 0 |  
| ix_StatusCode | 8 | 4 | 50 |  
| PK_SalesOrd_B14003... | 262144 | 96525 | 36 |  
  
  
- Luego tenemos los resultados de *longitud de la cadena*.  
  
  
| IndexName | avg_chain_length | max_chain_length |  
| :-------- | ---------------: | ---------------: |  
| ix_OrderSequence | 8 | 26 |  
| ix_StatusCode | 65536 | 65536 |  
| PK_SalesOrd_B14003... | 1 | 8 |  
  
  
  
  
Vamos a interpretar la tabla de resultados anterior para los tres índices de hash:  
  
*ix_StatusCode:*  
  
- El 50 % de los depósitos están vacíos, lo que es adecuado.  
- Sin embargo, el promedio de longitud de cadena es muy elevado (65 536).  
  - Esto indica una alta tasa de valores duplicados.  
  - Por consiguiente, el uso de un índice de hash no es adecuado en este caso. Se debe usar un índice no clúster en su lugar.  
  
*ix_OrderSequence:*  
  
- El 0 % de los depósitos están vacíos, lo que es demasiado bajo.  
- La longitud promedio de la cadena es 8, aunque todos los valores de este índice sean únicos.  
  - Por lo tanto, el número de depósitos debe aumentarse para reducir el promedio de longitud de cadena a un valor más cercano a 2 o 3.  
- Como la clave de índice tiene 262 144 valores únicos, el número de depósitos debe ser al menos 262 144.  
  - Si se espera un aumento futuro, el número de depósitos debe ser superior.  
  
*Índice de clave principal (PK_SalesOrd_...):*  
  
- El 36 % de los depósitos están vacíos, lo que es adecuado.  
- El promedio de longitud de cadena es 1, lo que también es adecuado. No se requieren cambios.  
  
  
### <a name="d3-balancing-the-trade-off"></a>D.3 Equilibrio de ventajas y desventajas  
  
Las cargas de trabajo de OLTP se centran en filas individuales. Los recorridos de tabla completos no suelen estar en la ruta crítica de rendimiento para cargas de trabajo de OLTP. Por lo tanto, las ventajas y desventajas que debe equilibrar son entre:  
  
- Cantidad de uso de memoria; frente a  
- Rendimiento de las pruebas de igualdad y de las operaciones de inserción.  
  
  
*Si el uso de memoria es la mayor preocupación:*  
  
- Elija un número de depósitos cercano al número de registros de clave de índice.  
- El número de depósitos no debería ser significativamente menor que el número de valores de clave de índice, puesto que esto afecta a la mayoría de las operaciones de DML así como al tiempo que lleva recuperar la base de datos después de reiniciar el servidor.  
  
  
*Si las pruebas de rendimiento de igualdad es la mayor preocupación:*  
  
- Un número mayor de depósitos, de dos o tres veces el número de valores de índice únicos, es adecuado. Un número mayor significa:  
  - Recuperaciones más rápidas cuando se busca un valor específico.  
  - Mayor uso de memoria.  
  - Aumento del tiempo necesario para un examen completo del índice de hash.  
  
  
  
  
## <a name="e-strengths-of-hash-indexes"></a>E. Puntos fuertes de los índices de hash  
  
  
Un índice de hash es preferible a un índice de hash cuando:  
  
- Las consultas prueban la columna indizada mediante el uso de una cláusula WHERE con una igualdad, como en el caso siguiente:  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="e1-multi-column-hash-index-keys"></a>E.1 Claves de índice de hash con varias columnas  
  
  
Nuestro índice de dos columnas puede ser un índice no agrupado o un índice de hash. Supongamos que las columnas de índice son col1 y col2. Si tenemos la siguiente instrucción SQL SELECT, solo el índice no agrupado sería útil para el optimizador de consultas:  
  
  
    SELECT col1, col3  
        FROM MyTable_memop  
        WHERE col1 = 'dn';  
  
  
El índice de hash requiere que la cláusula WHERE contenga una prueba de igualdad para cada una de las columnas en la clave. De lo contrario, dicho índice no tendrá ninguna utilidad para el optimizador.  
  
Ningún tipo de índice resultará útil si solo se especifica la segunda columna de la clave de índice en la cláusula WHERE.  
  
  
  
\<!--   
Hash_Indexes_for_Memory-Optimized_Tables.md , que es....  
guid MAYÚS: {e922cc3a-3d6e-453b-8d32-f4b176e98488}  
guid MAYÚS del elemento primario: {eecc5821-152b-4ed5-888f-7c0e6beffed9}  
  
  
  
  
| IndexName | total_bucket_count | empty_bucket_count | EmptyBucketPercent | avg_chain_length | max_chain_length |  
| :-------- | -----------------: | -----------------: | -----------------: | ---------------: | ---------------: |  
| ix_OrderSequence | 32768 | 13 | 0 | 8 | 26 |  
| ix_StatusCode | 8 | 4 | 50 | 65536 | 65536 |  
| PK_SalesOrd_B14003E308C1A23C | 262144 | 96525 | 36 | 1 | 8 |  
  
  
  
  
GeneMi  ,  2016-05-05  Thursday  15:01pm  
-->  
  
  
  


