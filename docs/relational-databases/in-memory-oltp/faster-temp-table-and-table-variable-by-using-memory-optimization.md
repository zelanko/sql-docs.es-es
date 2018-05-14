---
title: Tabla temporal y variable de tabla más rápidas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 38512a22-7e63-436f-9c13-dde7cf5c2202
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 27fe2515694f9045ff917be93ee7864c418c06d0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="faster-temp-table-and-table-variable-by-using-memory-optimization"></a>Tabla temporal y variable de tabla más rápidas con optimización para memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
Si usa tablas temporales, variables de tabla o parámetros con valores de tabla, tenga en cuenta sus conversiones para aprovechar las tablas optimizadas para memoria y las variables de tabla para mejorar el rendimiento. Los cambios de código normalmente son mínimos.  
  
En este artículo se explica:  
  
- Escenarios que argumentan en favor de la conversión a en memoria.  
- Pasos técnicos necesarios para implementar las conversiones a en memoria.  
- Requisitos previos antes de la conversión a en memoria.  
- Un ejemplo de código que resalta las ventajas de rendimiento de la optimización de memoria.
  
  
## <a name="a-basics-of-memory-optimized-table-variables"></a>A. Aspectos básicos de las variables de tabla optimizada para memoria  
  
Una variable de tabla optimizada para memoria ofrece una gran eficacia al usar la mismas estructuras de algoritmos y datos optimizados para memoria que emplean las tablas optimizadas para memoria. La eficacia se maximiza si se accede a la variable de tabla desde un módulo compilado de forma nativa.  
  
  
Una variable de tabla optimizada para memoria:  
  
- Solo se almacena en memoria y no tiene ningún componente en el disco.  
- No implica ninguna actividad de E/S.  
- No conlleva ningún uso o contención de tempdb.  
- Se puede pasar a un procedimiento almacenado como un parámetro con valores de tabla (TVP).  
- Debe tener al menos un índice, ya sea hash o no agrupado.  
  - En el caso de un índice de hash, el número de cubos idealmente debería ser entre una y dos veces el número de claves de índice únicas esperadas, aunque la sobrestimación de este número suele funcionar correctamente (hasta diez veces). Para obtener detalles, vea [Indexes for Memory-Optimized Tables (Índices de tablas con optimización para memoria)](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md).  

  
  
#### <a name="object-types"></a>Tipos de objetos  
  
OLTP en memoria proporciona los siguientes objetos que se pueden usar para la optimización de memoria de las tablas temporales y las variables de tabla:  
  
- Tablas con optimización para memoria  
  - Durability = SCHEMA_ONLY  
- Variables de tabla con optimización para memoria  
  - Se debe declarar en dos pasos (en lugar de en línea):  
    - `CREATE TYPE my_type AS TABLE ...;` , entonces  
    - `DECLARE @mytablevariable my_type;`.  
  
  
## <a name="b-scenario-replace-global-tempdb-x23x23table"></a>B. Escenario: Reemplazar la tabla temporal global &#x23;&#x23;  
  
Reemplazar una tabla temporal global por una tabla optimizada para memoria SCHEMA_ONLY es bastante sencillo. El cambio más importante es que hay que crear la tabla durante la implementación, y no durante la ejecución. La creación de tablas optimizadas para memoria requiere más tiempo que la de las tablas convencionales debido a las optimizaciones del tiempo de compilación. Si creáramos y colocáramos tablas optimizadas para memoria como parte de una carga de trabajo en línea, el impacto sobre el rendimiento de la carga de trabajo sería significativo, como también lo sería en el caso del rendimiento de la puesta al día de bases de datos secundarias de AlwaysOn y la recuperación de bases de datos.

Imagine que tiene la siguiente tabla temporal global.  
  
  
  
  
    CREATE TABLE ##tempGlobalB  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
  
  
  
  
Considere reemplazar la tabla temporal global por la siguiente tabla optimizada para memoria que tiene DURABILITY = SCHEMA_ONLY.  
  
  
  
  
    CREATE TABLE dbo.soGlobalB  
    (  
        Column1   INT   NOT NULL   INDEX ix1 NONCLUSTERED,  
        Column2   NVARCHAR(4000)  
    )  
        WITH  
            (MEMORY_OPTIMIZED = ON,  
            DURABILITY        = SCHEMA_ONLY);  
  
  
  
  
#### <a name="b1-steps"></a>B.1 Pasos  
  
La conversión de temporal global en SCHEMA_ONLY tiene los siguientes pasos:  
  
  
1. Cree la tabla **dbo.soGlobalB** una vez, como haría con cualquier tabla en disco tradicional.  
2. En Transact-SQL, quite la instrucción CREATE de la tabla **&#x23;&#x23;tempGlobalB**.  Es importante crear la tabla optimizada para memoria durante la implementación, y no durante la ejecución, para evitar la sobrecarga de la compilación que implica la creación de tablas.
3. En T-SQL, reemplace todas las menciones a **&#x23;&#x23;tempGlobalB** por **dbo.soGlobalB**.  
  
  
## <a name="c-scenario-replace-session-tempdb-x23table"></a>C. Escenario: Reemplazar la tabla temporal de sesión &#x23;  
  
Los preparativos para reemplazar una tabla temporal de sesión implican más T-SQL que para el escenario anterior de tabla temporal global. Afortunadamente, el T-SQL adicional no significa ningún otro esfuerzo adicional para realizar la conversión.  

Como en el caso de la tabla temporal global, el cambio más importante es que hay que crear la tabla durante la implementación, y no durante la ejecución, para evitar la sobrecarga de la compilación.
  
Imagine que tiene la siguiente tabla temporal de sesión.  
  
  
  
  
    CREATE TABLE #tempSessionC  
    (  
        Column1   INT   NOT NULL ,  
        Column2   NVARCHAR(4000)  
    );  
  
  
  
  
En primer lugar, cree la siguiente función con valores de tabla para filtrar en **@@spid**. Todas las tablas SCHEMA_ONLY que convierta desde tablas temporales de sesión podrán usar la función.  
  
  
  
  
    CREATE FUNCTION dbo.fn_SpidFilter(@SpidFilter smallint)  
        RETURNS TABLE  
        WITH SCHEMABINDING , NATIVE_COMPILATION  
    AS  
        RETURN  
            SELECT 1 AS fn_SpidFilter  
                WHERE @SpidFilter = @@spid;  
  
  
  
  
En segundo lugar, cree la tabla SCHEMA_ONLY, además de una directiva de seguridad en la tabla.  
  
  
Observe que cada tabla optimizada para memoria debe tener al menos un índice.  
  
- Para dbo.soSessionC, podría ser mejor un índice de HASH, si se calcula el valor BUCKET_COUNT adecuado. Pero en este ejemplo se simplifica con un índice NONCLUSTERED.  
  
  
  
  
    CREATE TABLE dbo.soSessionC  
    (  
        Column1     INT         NOT NULL,  
        Column2     NVARCHAR(4000)  NULL,  
  
        SpidFilter  SMALLINT    NOT NULL   DEFAULT (@@spid),  
  
        INDEX ix_SpidFiler NONCLUSTERED (SpidFilter),  
        --INDEX ix_SpidFilter HASH  
        --    (SpidFilter) WITH (BUCKET_COUNT = 64),  
          
        CONSTRAINT CHK_soSessionC_SpidFilter  
            CHECK ( SpidFilter = @@spid ),  
    )  
        por  
            (MEMORY_OPTIMIZED = ON,  
             DURABILITY = SCHEMA_ONLY);  
    GO  
  
  
    CREATE SECURITY POLICY dbo.soSessionC_SpidFilter_Policy  
        ADD FILTER PREDICATE dbo.fn_SpidFilter(SpidFilter)  
        ON dbo.soSessionC  
        WITH (STATE = ON);  
    GO  
  
  
  
  
En tercer lugar, en el código T-SQL general:  
  
1. Cambie todas las referencias a la tabla temporal en las instrucciones de Transact-SQL a la nueva tabla optimizada para memoria:
    - _Antiguo:_ &#x23;tempSessionC  
    - _Nuevo:_ dbo.soSessionC  
2. Reemplace las instrucciones `CREATE TABLE #tempSessionC` en el código por `DELETE FROM dbo.soSessionC` para garantizar que la sesión no se vea expuesta al contenido de la tabla insertada mediante una sesión anterior con el mismo identificador de sesión. Es importante crear la tabla optimizada para memoria durante la implementación, y no durante la ejecución, para evitar la sobrecarga de la compilación que implica la creación de tablas.
3. Quite las instrucciones `DROP TABLE #tempSessionC` del código (opcionalmente, puede insertar una instrucción `DELETE FROM dbo.soSessionC`, por si el tamaño de la memoria es un posible problema).
  
  
  
  
## <a name="d-scenario-table-variable-can-be-memoryoptimizedon"></a>D. Escenario: Una variable de tabla puede ser MEMORY_OPTIMIZED=ON  
  
  
Una variable de tabla tradicional representa una tabla de la base de datos tempdb. Para un rendimiento mucho más rápido, puede optimizar la memoria de la variable de tabla.  
  
Este es el T-SQL de una variable de tabla tradicional. Su ámbito finaliza cuando finaliza el lote o la sesión.  
  
  
  
  
    DECLARE @tvTableD TABLE  
        ( Column1   INT   NOT NULL ,  
          Column2   CHAR(10) );  
  
  
  
  
#### <a name="d1-convert-inline-to-explicit"></a>D.1 Convertir en línea en explícito  
  
Se dice que la sintaxis anterior crea la variable de tabla *en línea*. La sintaxis en línea no admite la optimización de memoria. Por eso se va convertir la sintaxis en línea en sintaxis explícita para TYPE.  
  
*Ámbito:* la definición de TYPE creada por el primer lote delimitado por la instrucción GO persiste incluso después de que el servidor se apague y se reinicie. Pero después del primer delimitador GO, la tabla declarada @tvTableC persiste hasta que se alcanza la siguiente instrucción GO y el lote finaliza.  
  
  
  
  
    CREATE TYPE dbo.typeTableD  
        AS TABLE  
        (  
            Column1  INT   NOT NULL ,  
            Column2  CHAR(10)  
        );  
    go  
          
    SET NoCount ON;  
    DECLARE @tvTableD dbo.typeTableD  
    ;  
    INSERT INTO @tvTableD (Column1) values (1), (2)  
    ;  
    SELECT * from @tvTableD;  
    go  
  
  
  
  
#### <a name="d2-convert-explicit-on-disk-to-memory-optimized"></a>D.2 Convertir explícito en disco en optimización para memoria  
  
Una variable de tabla optimizada para memoria no reside en tempdb. La optimización de memoria produce aumentos de velocidad que suelen ser 10 veces más rápidos o más.  
  
La conversión a una tabla optimizada para memoria se consigue en un solo paso. Mejore la creación de TYPE explícita para que sea la siguiente, que agrega:  
  
- Un índice. De nuevo, cada tabla optimizada para memoria debe tener al menos un índice.  
- MEMORY_OPTIMIZED = ON.  
  
  
  
  
    CREATE TYPE dbo.typeTableD  
        AS TABLE  
        (  
            Column1  INT   NOT NULL   INDEX ix1,  
            Column2  CHAR(10)  
        )  
        por  
            (MEMORY_OPTIMIZED = ON);  
  
  
  
  
Listo.  
  
  
## <a name="e-prerequisite-filegroup-for-sql-server"></a>E. FILEGROUP como requisito previo para SQL Server  
  
En Microsoft SQL Server, para usar las características de optimización para memoria, la base de datos debe tener un FILEGROUP declarado con **MEMORY_OPTIMIZED_DATA**.  
  
- La base de datos SQL de Azure no necesita crear este FILEGROUP.  
  
  
*Requisito previo:* el siguiente código Transact-SQL para un FILEGROUP es un requisito previo para los ejemplos de código largos de T-SQL en secciones posteriores de este artículo.  
  
1. Debe usar SSMS.exe u otra herramienta que pueda enviar T-SQL.  
2. Pegue el código T-SQL de FILEGROUP de ejemplo en SSMS.  
3. Edite el T-SQL para cambiar sus nombres y rutas de acceso a directorios concretos a su gusto.  
  - Todos los directorios del valor FILENAME deben existir de antemano, excepto el último.  
4. Ejecute el T-SQL editado.  
  - No hay necesidad de ejecutar el T-SQL de FILEGROUP más de una vez, aunque ajuste repetidamente y vuelva a ejecutar el T-SQL de comparación de velocidad de la siguiente subsección.  
  
  
  
 
  
    ALTER DATABASE InMemTest2  
        ADD FILEGROUP FgMemOptim3  
            CONTAINS MEMORY_OPTIMIZED_DATA;  
    GO  
    ALTER DATABASE InMemTest2  
        ADD FILE  
        (  
            NAME = N'FileMemOptim3a',  
            FILENAME = N'C:\DATA\FileMemOptim3a'  
                     --  C:\DATA\    preexisted.  
        )  
        TO FILEGROUP FgMemOptim3;  
    GO  
  
  
El script siguiente crea el grupo de archivos y configura los valores recomendados de la base de datos: [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)
  
Para obtener más información sobre `ALTER DATABASE ... ADD` para FILE y FILEGROUP, vea:  
  
- [Opciones File y Filegroup de ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
- [El grupo de archivos con optimización para memoria](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)    
  
  
## <a name="f-quick-test-to-prove-speed-improvement"></a>F. Prueba rápida para demostrar la mejora de velocidad  
  
  
En esta sección se proporciona código Transact-SQL que se puede ejecutar para probar y comparar el aumento de velocidad de INSERT-DELETE con el uso de una variable de tabla optimizada para memoria. El código se compone de dos mitades que son casi iguales, salvo que en la primera mitad el tipo de la tabla sea optimizada para memoria.  
  
La comparación dura unos 7 segundos. Para ejecutar el ejemplo:  
  
1. *Requisito previo:* ya debe haber ejecutado el T-SQL FILEGROUP de la sección anterior.  
2. Ejecute el siguiente script de T-SQL INSERT-DELETE.  
  - Observe la instrucción “GO 5001”, que vuelve a enviar el T-SQL 5001 veces. Puede ajustar el número y volver a ejecutar.  
  
Al ejecutar el script en una base de datos SQL de Azure, asegúrese de ejecutar desde una máquina virtual en la misma región.
  
  
    PRINT ' ';  
    PRINT '---- Next, memory-optimized, faster. ----';  
  
    DROP TYPE IF EXISTS dbo.typeTableC_mem;  
    go  
    CREATE TYPE dbo.typeTableC_mem  -- !!  Memory-optimized.  
         AS TABLE  
         (  
              Column1  INT NOT NULL INDEX ix1,  
              Column2  CHAR(10)  
         )  
         WITH  
              (MEMORY_OPTIMIZED = ON);  
    go  
    DECLARE @dateString_Begin nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_Begin, '  = Begin time, _mem.');  
    go  
    SET NoCount ON;  
    DECLARE @tvTableC dbo.typeTableC_mem;  -- !!  
  
    INSERT INTO @tvTableC (Column1) values (1), (2);  
    INSERT INTO @tvTableC (Column1) values (3), (4);  
    DELETE @tvTableC;  
  
    GO 5001  
  
    DECLARE @dateString_End nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_End, '  = End time, _mem.');  
    go  
    DROP TYPE IF EXISTS dbo.typeTableC_mem;  
    go  
  
    ---- End memory-optimized.  
    -------------------------------------------------  
    ---- Start traditional on-disk.  
  
    PRINT ' ';  
    PRINT '---- Next, tempdb based, slower. ----';  
  
    DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
    go  
    CREATE TYPE dbo.typeTableC_tempdb  -- !!  Traditional tempdb.  
        AS TABLE  
        (  
            Column1  INT NOT NULL ,  
            Column2  CHAR(10)  
        );  
    go  
    DECLARE @dateString_Begin nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_Begin, '  = Begin time, _tempdb.');  
    go  
    SET NoCount ON;  
    DECLARE @tvTableC dbo.typeTableC_tempdb;  -- !!  
  
    INSERT INTO @tvTableC (Column1) values (1), (2);  
    INSERT INTO @tvTableC (Column1) values (3), (4);  
    DELETE @tvTableC;  
  
    GO 5001  
  
    DECLARE @dateString_End nvarchar(64) =  
        Convert(nvarchar(64), GetUtcDate(), 121);  
    PRINT Concat(@dateString_End, '  = End time, _tempdb.');  
    go  
    DROP TYPE IF EXISTS dbo.typeTableC_tempdb;  
    go  
    ----  
  
    PRINT '---- Tests done. ----';  
  
    go  
  
    /*** Actual output, SQL Server 2016:  
  
    ---- Next, memory-optimized, faster. ----  
    2016-04-20 00:26:58.033  = Begin time, _mem.  
    Beginning execution loop  
    Batch execution completed 5001 times.  
    2016-04-20 00:26:58.733  = End time, _mem.  
  
    ---- Next, tempdb based, slower. ----  
    2016-04-20 00:26:58.750  = Begin time, _tempdb.  
    Beginning execution loop  
    Batch execution completed 5001 times.  
    2016-04-20 00:27:05.440  = End time, _tempdb.  
    ---- Tests done. ----  
    ***/  
  

  
  
  
## <a name="g-predict-active-memory-consumption"></a>G. Predecir el consumo de memoria activa  
  
Puede aprender a predecir las necesidades de memoria activa de las tablas optimizadas para memoria con los siguientes recursos:  
  
- [Estimar los requisitos de memoria para las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [Tamaño de tabla y fila de las tablas con optimización para memoria: cálculo de ejemplo](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
En variables de tabla más grandes, los índices no agrupados usan más memoria que con las *tablas* optimizadas para memoria. Cuanto mayor sea el recuento de filas y la clave de índice, más aumentará la diferencia.  
  
Si se accede a la variable de tabla optimizada para memoria solo con un valor de clave exacto por acceso, un índice de hash puede ser una opción mejor que un índice no agrupado. Pero si no puede calcular el valor BUCKET_COUNT adecuado, un índice NONCLUSTERED es una buena segunda opción.  
  
## <a name="h-see-also"></a>H. Vea también  
  
- [Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)
- [Definir la durabilidad de los objetos con optimización para memoria](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
