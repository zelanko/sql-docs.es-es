---
title: Directrices para usar índices en tablas optimizadas para memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- hash indexes
ms.assetid: 16ef63a4-367a-46ac-917d-9eebc81ab29b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 71d26e3f46034019d51bd69b86686f40eb9ce63e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779229"
---
# <a name="guidelines-for-using-indexes-on-memory-optimized-tables"></a>Directrices para usar índices en las tablas con optimización para memoria
  Los índices se utilizan para tener acceso a los datos de forma eficaz en las tablas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Especificar los índices adecuados puede mejorar drásticamente el rendimiento de las consultas. Considere, por ejemplo, la consulta:  
  
```sql  
SELECT c1, c2 FROM t WHERE c1 = 1;  
```  
  
 Si no hay ningún índice en la columna c1, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] necesitará examinar toda la tabla t y, a continuación, filtrar en las filas que cumplen la condición c1=1. Sin embargo, si tiene un índice en la columna c1, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede buscar directamente en el valor 1 y recuperar las filas.  
  
 Para buscar los registros que tienen un valor específico o un intervalo de valores para una o varias columnas de la tabla, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede utilizar un índice en dichas columnas para buscar rápidamente los registros correspondientes. Tanto las tablas optimizadas para memoria como las basadas en disco se benefician de los índices. Sin embargo, hay algunas diferencias entre las estructuras de índice que deben tenerse en cuenta al utilizar las tablas optimizadas para memoria. (Los índices en tablas optimizadas para memoria se denominan índices optimizados para memoria.) Algunas de las principales diferencias son:  
  
-   Los índices optimizados para memoria deben crearse con [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql). Los índices basados en disco se pueden crear con `CREATE TABLE` y `CREATE INDEX`.  
  
-   Los índices con optimización para memoria solo existen en la memoria. Las estructuras de índice no permanecen en el disco y las operaciones de índice no se graban en el registro de transacciones. Se crea la estructura de índice cuando la tabla optimizada para memoria se crea en la memoria, durante la operación CREATE TABLE y durante el inicio de la base de datos.  
  
-   Los índices con optimización para memoria tienen cobertura de forma intrínseca. El alcance implica que todas las columnas se incluyen virtualmente en el índice y las búsquedas de marcadores no son necesarias en las tablas optimizadas para memoria. En lugar de una referencia a la clave principal, los índices optimizados para memoria simplemente contienen un puntero de memoria a la fila real en la estructura de datos de la tabla.  
  
-   La fragmentación y el factor de relleno no se aplican a los índices optimizados para memoria. En los índices basados en disco, la fragmentación hace referencia a las páginas del árbol B que se están escribiendo en el disco que no funciona. Los índices con optimización para memoria no se escriben ni se leen del disco. El factor de relleno en los índices de árbol b basado en disco hace referencia al grado en que las estructuras de páginas físicas se rellenan con datos reales. Las estructuras de índice optimizado para memoria no tienen páginas de tamaño fijo.  
  
 Hay dos tipos de índices optimizados para memoria:  
  
-   Los índices de hash no clúster, que son convenientes para las búsquedas de puntos. Para obtener más información acerca de los índices de hash, vea [índices Hash](hash-indexes.md).  
  
-   Los índices no clúster, que son para exámenes de intervalo y exámenes ordenados.  
  
 Con un índice hash, se accede a los datos a través de una tabla hash en memoria. Los índices hash no tienen páginas y son siempre de un tamaño fijo. Sin embargo, un índice hash puede tener cubos de hash vacíos, lo que da lugar a un espacio desaprovechado limitado. Los valores devueltos de una consulta con un índice hash no están ordenadas. Los índices hash se optimizan para las búsquedas de índice en predicados de igualdad y también admiten exploraciones de índice completas.  
  
 Los índices no clúster (no los índices hash) admiten lo mismo que los índices hash, además de operaciones de búsqueda en predicados de desigualdad como mayor que o menor que, así como el criterio de ordenación. Las filas se pueden recuperar en el orden especificado para la creación de los índices. Si el criterio de ordenación del índice coincide con el orden requerido para una consulta determinada, por ejemplo, si la clave del índice coincide con la cláusula ORDER BY, no es necesario ordenar las filas como parte de la ejecución de la consulta. Los índices no clúster con optimización para memoria son unidireccionales: no permiten recuperar filas con un criterio de ordenación inverso al del índice. Por ejemplo, para un índice especificado como (c1 ASC) no es posible examinar el índice en orden inverso, como (c1 DESC).  
  
 Cada índice utiliza memoria. Los índices hash utilizan una cantidad fija de memoria, que es una función del número de cubos. Para los índices no clúster, el consumo de memoria depende del número de filas y del tamaño de las columnas de clave de índice, con una sobrecarga adicional que depende de la carga de trabajo. La memoria para los índices optimizados para memoria es adicional e independiente de la memoria usada para almacenar las filas de las tablas optimizadas para memoria.  
  
 Los valores de clave duplicados comparten siempre el mismo depósito de hash. Si un índice hash contiene muchos valores clave duplicados, las cadenas para el hash largas resultantes repercutirán negativamente en el rendimiento. Las colisiones de hash, que se producen en los índices hash, reducirán aún más el rendimiento en este escenario. Por ese motivo, si el número de claves de índice únicas es al menos 100 veces menor que el recuento de filas, puede reducir el riesgo de colisiones de hash mediante la realización del depósito contar mucho más grande (al menos ocho veces el número de claves de índice únicas; vea [determinar el El número correcto de depósitos para los índices Hash](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md) para obtener más información) o bien puede eliminar las colisiones de hash completamente mediante el uso de un índice no agrupado.  
  
## <a name="determining-which-indexes-to-use-for-a-memory-optimized-table"></a>Determinar qué índices se deben usar para una tabla con optimización para memoria  
 Cada tabla optimizada para memoria debe tener al menos un índice. Tenga en cuenta que cada restricción PRIMARY KEY crea implícitamente un índice. Por consiguiente, si una tabla tiene una clave principal, tiene un índice. Una clave principal es un requisito para una tabla optimizada para memoria perdurable.  
  
 Al consultar una tabla optimizada para memoria, los índices hash funcionan mejor cuando la cláusula de predicado solo contiene predicados de igualdad. El predicado debe incluir todas las columnas de clave de índice hash. Un índice hash revertirá a un recorrido dado un predicado de desigualdad.  
  
 Una columna de una tabla optimizada para memoria puede formar parte de un índice hash y de un índice no clúster.  
  
 Al consultar una tabla optimizada para memoria con predicados de desigualdad, los índices no clúster se comportarán mejor que los índices de hash no clúster.  
  
 El índice hash requiere una clave (de hash) para buscar en el índice. Si la clave de índice consta de dos columnas y solo proporciona la primera, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no tiene una clave completa para aplicar el algoritmo hash. Esto generará un plan de consulta de examen de índice. El uso determina qué columnas deben ser indizadas.  
  
 Cuando una columna de un índice no clúster tiene el mismo valor en muchas filas (las columnas de clave de índice tienen muchos valores duplicados), el rendimiento puede reducirse para las actualizaciones, las inserciones y las eliminaciones.  Una manera de mejorar el rendimiento en este escenario es agregar otra columna al índice no clúster.  
  
### <a name="operations-on-memory-optimized-and-disk-based-indexes"></a>Operaciones de índices basados en disco y optimizados para memoria.  
  
|Operación|Índice no clúster, hash, con optimización para memoria|Índice no clúster con optimización para memoria|Índice basado en disco|  
|---------------|-------------------------------------------------|------------------------------------------|-----------------------|  
|Index scan, recupera todas las filas de la tabla.|Sí|Sí|Sí|  
|Index seek en predicados de igualdad (=).|Sí<br /><br /> (Clave completa necesaria.)|Sí <sup>1</sup>|Sí|  
|Index seek en predicados de desigualdad (>, <, \<=, > =, BETWEEN).|No (resultados en un examen de índice)|Sí <sup>1</sup>|Sí|  
|Recupere las filas en un orden que coincida con la definición de índice.|Sin|Sí|Sí|  
|Recupere las filas en un orden que coincida con el opuesto de la definición de índice.|Sin|Sin|Sí|  
  
 En la tabla, Sí se refiere a que el índice puede prestar servicio correctamente a la solicitud y No se refiere a que el índice no se puede usar correctamente para atender la solicitud.  
  
 <sup>1</sup> para un índice no agrupado optimizado para memoria, no se requiere la clave completa para realizar una búsqueda de índice. Sin embargo, dado el orden de las columnas de la clave de índice, se producirá un examen si el valor de una columna viene después de una columna que falta.  
  
## <a name="index-count"></a>Contador de índice  
 Una tabla optimizada para memoria puede tener hasta ocho índices, incluido el creado con la clave principal.  
  
 En relación con el número de índices creados en una tabla optimizada para memoria, considere lo siguiente:  
  
-   Especifique los índices que necesita al crear la tabla. No puede crear un índice para una tabla optimizada para memoria después de crear la tabla. Si desea agregar un índice a una tabla optimizada para memoria, quite la tabla y vuelva a crearla.  
  
-   No cree un índice que use poco:  
  
     La recolección de elementos no utilizados funciona mejor si todos los índices de la tabla se utilizan con frecuencia. Los índices que se usan poco pueden hacer que el sistema de recopilación de elementos no utilizados no se comporten de forma óptimo en las versiones de fila anteriores.  
  
## <a name="creating-a-memory-optimized-index-code-samples"></a>Crear un índice optimizado para memoria: Ejemplos de código  
 Índice hash de nivel de columna:  
  
```sql  
CREATE TABLE t1   
   (c1 INT NOT NULL INDEX idx HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Índice hash de nivel de tabla:  
  
```sql  
CREATE TABLE t1_1   
   (c1 INT NOT NULL,   
   INDEX IDX HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Índice hash de la clave principal de nivel de columna:  
  
```sql  
CREATE TABLE t2   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Índice hash de la clave principal de nivel de tabla:  
  
```sql  
CREATE TABLE t2_2   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Índice no clúster de nivel de columna:  
  
```sql  
CREATE TABLE t3   
   (c1 INT NOT NULL INDEX ID)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Índice no clúster de nivel de tabla:  
  
```sql  
CREATE TABLE t3_3   
   (c1 INT NOT NULL,   
   INDEX IDX NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 Índice no clúster de la clave principal de nivel de columna:  
  
```sql  
CREATE TABLE t4   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Índice no clúster de la clave principal de nivel de tabla:  
  
```sql  
CREATE TABLE t4_4   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 Índice de varias columnas definido después de definir las columnas:  
  
```sql  
create table t (  
       a int not null constraint ta primary key nonclustered,  
       b int not null,  
       c int not null,  
       d int not null,  
       index idx_t_b_c_d nonclustered (b, c asc, d desc)  
) with (memory_optimized = on, durability = SCHEMA_AND_DATA)  
go  
```  
  
## <a name="see-also"></a>Vea también  
 [Índices en tablas optimizadas para memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Determinar el número correcto de depósitos para los índices Hash](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md)   
 [Índices de hash](hash-indexes.md)  
  
  
