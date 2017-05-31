---
title: "Índices de tablas con optimización para memoria | Microsoft Docs"
ms.custom:
- MSDN content
- MSDN - SQL DB
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.service: sql-database
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eecc5821-152b-4ed5-888f-7c0e6beffed9
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f55708bc9eaf8e94cf33ead19cf62cbc319e8e63
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="indexes-for-memory-optimized-tables"></a>Índices de tablas con optimización para memoria
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  
En este artículo se describen los tipos de índices que están disponibles para una tabla con optimización para memoria. El artículo:  
  
- Ofrece ejemplos de código corto que muestran la sintaxis de Transact-SQL.  
- Describe cómo se diferencian los índices con optimización para memoria de los índices tradicionales basados en disco.  
- Explica las circunstancias en las que cada tipo de índice con optimización para memoria resulta más adecuado.  
  
  
Los índices de*hash* se abordan con más detalle en un [artículo relacionado](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md).  
  
  
Los índices de*almacén de columnas* se tratan en [otro artículo](~/relational-databases/indexes/columnstore-indexes-overview.md).  
  
  
## <a name="a-syntax-for-memory-optimized-indexes"></a>A. Sintaxis de índices con optimización para memoria  
  
Cada instrucción CREATE TABLE para una tabla con optimización para memoria debe incluir entre 1 y 8 cláusulas para declarar los índices. El índice debe ser uno de los siguientes:  
  
- Índice de hash.  
- Índice no agrupado (es decir, la estructura interna predeterminada de un árbol B).  
  
  
Para declararse con el valor predeterminado de DURABILITY = SCHEMA_AND_DATA, la tabla con optimización para memoria debe tener una clave principal. La cláusula PRIMARY KEY NONCLUSTERED de la siguiente instrucción CREATE TABLE cumple dos requisitos:  
  
- Proporciona un índice para satisfacer el requisito mínimo de tener un índice en la instrucción CREATE TABLE.  
- Proporciona la clave principal necesaria para la cláusula SCHEMA_AND_DATA.  
  
  
  
    CREATE TABLE SupportEvent  
    (  
        SupportEventId   int NOT NULL  
            PRIMARY KEY NONCLUSTERED,  
        ...  
    )  
        WITH (  
            MEMORY_OPTIMIZED = ON,  
            DURABILITY = SCHEMA_AND_DATA);  
  
  
  
### <a name="a1-code-sample-for-syntax"></a>A.1 Ejemplo de código para sintaxis  
  
En este apartado se incluye un bloque de código de Transact-SQL que muestra la sintaxis para crear varios índices en una tabla con optimización para memoria. El código muestra lo siguiente:  
  
  
1. Crear una tabla con optimización para memoria.  
2. Usar instrucciones ALTER TABLE para agregar dos índices.  
3. Usar INSERT para insertar algunas filas de datos.  
  
  
  
    DROP TABLE IF EXISTS SupportEvent;  
    go  
  
    CREATE TABLE SupportEvent  
    (  
      SupportEventId   int               not null   identity(1,1)  
        PRIMARY KEY NONCLUSTERED,  
  
      StartDateTime        datetime2     not null,  
      CustomerName         nvarchar(16)  not null,  
      SupportEngineerName  nvarchar(16)      null,  
      Priority             int               null,  
      Description          nvarchar(64)      null  
    )  
      WITH (  
        MEMORY_OPTIMIZED = ON,  
        DURABILITY = SCHEMA_AND_DATA);  
    go  
      
        --------------------  
      
    ALTER TABLE SupportEvent  
      ADD CONSTRAINT constraintUnique_SDT_CN  
        UNIQUE NONCLUSTERED (StartDateTime DESC, CustomerName);  
    go  
  
    ALTER TABLE SupportEvent  
      ADD INDEX idx_hash_SupportEngineerName  
        HASH (SupportEngineerName) WITH (BUCKET_COUNT = 64);  -- Nonunique.  
    go  
      
        --------------------  
      
    INSERT INTO SupportEvent  
        (StartDateTime, CustomerName, SupportEngineerName, Priority, Description)  
      VALUES  
        ('2016-02-25 13:40:41:123', 'Abby', 'Zeke', 2, 'Display problem.'     ),  
        ('2016-02-25 13:40:41:323', 'Ben' , null  , 1, 'Cannot find help.'    ),  
        ('2016-02-25 13:40:41:523', 'Carl', 'Liz' , 2, 'Button is gray.'      ),  
        ('2016-02-25 13:40:41:723', 'Dave', 'Zeke', 2, 'Cannot unhide column.');  
    go  
  
  
  
## <a name="b-nature-of-memory-optimized-indexes"></a>B. Naturaleza de los índices con optimización para memoria  
  
En una tabla con optimización para memoria, todos los índices también son con optimización para memoria. Hay varias formas de diferenciar un índice en un índice con optimización para memoria de un índice tradicional en una tabla basada en disco.  
  
Cada índice con optimización para memoria existe únicamente en la memoria activa. Dicho índice no tiene representación en disco.  
  
- Los índices con optimización para memoria se vuelven a generar cuando la base de datos vuelve a estar en línea.  
  
  
Cuando una instrucción UPDATE de SQL modifica los datos de una tabla con optimización para memoria, los cambios correspondientes en sus índices no se escriben en el registro.  
  
  
Las entradas de un índice con optimización para memoria contienen una dirección de memoria directa a la fila de la tabla.  
  
- En cambio, las entradas de un índice de árbol B tradicional en disco contienen un valor de clave que el sistema debe usar en primer lugar para hallar la dirección de memoria a la fila de tabla asociada.  
  
  
Los índices con optimización para memoria no tienen ninguna página fija como sí tienen los índices basados en disco.  
  
- No acumulan el tipo tradicional de fragmentación dentro de una página, por lo que no tienen ningún factor de relleno.  
  
## <a name="c-duplicate-index-key-values"></a>C. Valores de clave de índice duplicados

Los valores de clave de índice duplicados pueden afectar al rendimiento de las operaciones en las tablas con optimización para memoria. Cuando el número de duplicados es elevado (más de 100, por ejemplo), la tarea de mantenimiento de un índice no es eficaz porque hay que atravesar cadenas duplicadas en la mayoría de las operaciones de índice. El impacto de esto se aprecia en operaciones INSERT, UPDATE y DELETE realizadas en tablas con optimización para memoria. Este problema es más patente en el caso de los índices de hash, debido tanto el menor costo por operación de este tipo de índices y a la interferencia de grandes cadenas duplicadas con la cadena de colisión de hash. Para reducir la duplicación en un índice, use un índice no agrupado y agregue más columnas (por ejemplo, desde la clave principal) al final de la clave de índice con el propósito de reducir el número de duplicados.

Pensemos, por ejemplo, en una tabla Customers con una clave principal en CustomerId y un índice en la columna CustomerCategoryID. Normalmente, habrá muchos clientes de una categoría determinada y, por tanto, muchos valores duplicados para una clave determinada en el índice de CustomerCategoryID. En este escenario, la recomendación es usar un índice no agrupado en (CustomerCategoryID, CustomerId). Este índice se puede usar en consultas que usan un predicado donde existe CustomerCategoryID y que no contienen duplicados y, en consecuencia, no provocan ineficiencias en el mantenimiento de índices.

La consulta siguiente muestra el promedio de valores clave de índice duplicados para el índice en `CustomerCategoryID` en la tabla `Sales.Customers`, en la base de datos de ejemplo [WideWorldImporters](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx).

```Transact-SQL
    SELECT AVG(row_count) FROM
       (SELECT COUNT(*) AS row_count 
        FROM Sales.Customers
        GROUP BY CustomerCategoryID) a
```

Para evaluar el promedio de duplicados de clave de índice para su propia tabla e índice, reemplace `Sales.Customers` por su nombre de la tabla y reemplace `CustomerCategoryID` por la lista de columnas de clave de índice.

## <a name="d-comparing-when-to-use-each-index-type"></a>D. Comparación del uso de cada tipo de índice  
  
  
La naturaleza de las consultas concretas determina qué tipo de índice es la mejor opción.  

Al implementar tablas con optimización para memoria en una aplicación existente, la recomendación general es comenzar por los índices no agrupados, ya que sus capacidades se parecen más a las de los índices agrupados y no agrupados tradicionales de las tablas basadas en disco. 
  
  
### <a name="d1-strengths-of-nonclustered-indexes"></a>D.1 Ventajas de los índices no agrupados  
  
  
Un índice no agrupado es preferible a un índice de hash cuando:  
  
- Las consultas tienen una cláusula ORDER BY en la columna indizada.  
- Las consultas en las que solo se comprueban las primeras columnas de un índice con varias columnas.  
- Las consultas prueban la columna indizada mediante el uso de una cláusula WHERE con:  
  - Una desigualdad: *WHERE StatusCode != 'Done'*  
  - Un rango de valores: *WHERE Quantity >= 100*  
  
  
En todas las instrucciones SELECT siguientes, es preferible un índice no agrupado a un índice de hash:  
  
  
  
    SELECT col2 FROM TableA  
        WHERE StartDate > DateAdd(day, -7, GetUtcDate());  
      
    SELECT col3 FROM TableB  
        WHERE ActivityCode != 5;  
      
    SELECT StartDate, LastName  
        FROM TableC  
        ORDER BY StartDate;  
      
    SELECT IndexKeyColumn2  
        FROM TableD  
        WHERE IndexKeyColumn1 = 42;  
  
  
  
### <a name="d2-strengths-of-hash-indexes"></a>D.2 Ventajas de los índices de hash  
  
  
Un [índice de hash](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md) es preferible a un índice no agrupado cuando:  
  
- Las consultas comprueban las columnas indexadas usando una cláusula WHERE con una equivalencia exacta en todas las columnas de clave de índice, como en el siguiente caso:  
  
  
  
    SELECT col9 FROM TableZ  
        WHERE Z_Id = 2174;  
  
  
  
### <a name="d3-summary-table-to-compare-index-strengths"></a>D.3 Tabla de resumen de comparación de ventajas de los índices  
  
  
En la tabla siguiente se enumeran todas las operaciones que son compatibles con distintos tipos de índices.  
  
  
| Operación | Con optimización para memoria, <br/> hash | Con optimización para memoria, <br/> no agrupados | Basada en disco, <br/> (no)agrupados |  
| :-------- | :--------------------------- | :----------------------------------- | :------------------------------------ |  
| Index scan, recupera todas las filas de la tabla. | Sí | Sí | Sí |  
| Index seek en predicados de igualdad (=). | Sí <br/> (Se requiere la clave completa). | Sí  | Sí |  
| Index seek en predicados de desigualdad y de intervalo <br/> (>, <, \<=, >=, BETWEEN). | No <br/> (Resultados de un examen de índice). | Sí | Sí |  
| Recuperar filas según un criterio de ordenación que coincida con la definición de índice. | No | Sí | Sí |  
| Recuperar filas según un criterio de ordenación que coincida con el opuesto de la definición de índice. | No | No | Sí |  
  
  
En la tabla, Sí se refiere a que el índice puede atender la solicitud con eficiencia y No se refiere a que el índice no puede satisfacer la solicitud con eficiencia.  


  
  
\<!--   
Indexes_for_Memory-Optimized_Tables.md, que es...  
guid MAYÚS: {eecc5821-152b-4ed5-888f-7c0e6beffed9}  
mt670614.aspx  
  
Application-Level%20Partitioning.xml , {162d1392-39d2-4436-a4d9-ee5c47864c5a}  
  
/Image/hekaton_tables_23d.png, fbc511a0-304c-42f7-807d-d59f3193748f  
  
  
Reemplaza dn511012.aspx, que es....  
guid MAYÚS: {86805eeb-6972-45d8-8369-16ededc535c7}  
  
GeneMi,  2016-05-05  miércoles 17:25 p..m  (contenido hash movido al nuevo artículo secundario, e922cc3a-3d6e-453b-8d32-f4b176e98488.)  
-->  
  
  
  



