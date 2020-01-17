---
title: OLTP en memoria para acelerar el rendimiento de Transact-SQL
ms.custom: seo-dt-2019
ms.date: 09/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 1c25a164-547d-43c4-8484-6b5ee3cbaf3a
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ca32d98270a6eea4bd918c12c6b45279a05628e5
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412501"
---
# <a name="survey-of-initial-areas-in-in-memory-oltp"></a>Encuesta de áreas iniciales de OLTP en memoria

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  
Este artículo está destinado a los desarrolladores que necesitan aprender rápidamente los conceptos básicos de las características de rendimiento de OLTP en memoria de Microsoft SQL Server y Base de datos SQL de Azure.  
  
Para OLTP en memoria, este artículo incluye lo siguiente:  
  
- Breves explicaciones de las características.  
- Ejemplos de código principal que implementan las características.  
  
  
SQL Server y Base de datos SQL presentan solo pequeñas variaciones en su compatibilidad con tecnologías en memoria.  
  
  
En su ámbito, algunos blogueros hacen referencia a las características de OLTP en memoria como *Hekaton*.  
  
  
<a name="benefits-of-in-memory-features-21a"></a>  
  
## <a name="benefits-of-in-memory-features"></a>Ventajas de las características en memoria  
  
SQL Server proporciona características en memoria que pueden mejorar considerablemente el rendimiento de muchos sistemas de aplicaciones. En esta sección se describen las consideraciones más sencillas.  
  
  
### <a name="features-for-oltp-online-transactional-processing"></a>Características de OLTP (procesamiento de transacciones en línea)  
  
  
Los sistemas que deben procesar simultáneamente grandes cantidades de instrucciones INSERT de SQL son los candidatos perfectos para las características de OLTP.  
  
- Nuestras pruebas comparativas muestran que la velocidad se puede multiplicar entre 5 y 20 veces con la adopción de las características en memoria.  
  
  
Los sistemas que procesan cálculos intensivos en Transact-SQL son candidatos ideales.  
  
- Un procedimiento almacenado que se dedica a cálculos intensivos se puede ejecutar hasta 99 veces más rápido.  
  
  
Más tarde tal vez le interese visitar los siguientes artículos, que ofrecen demostraciones de las mejoras de rendimiento de OLTP en memoria:  
  
- [Demostración: mejora de rendimiento de OLTP en memoria](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) ofrece una demostración a pequeña escala de las posibles mejoras de rendimiento más grandes.  
- [Sample Database for In-Memory OLTP (Base de datos de ejemplo para OLTP en memoria)](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) ofrece una demostración de escala mayor.  
  
  
  
### <a name="features-for-operational-analytics"></a>Características de análisis operativo  
  
El análisis en memoria hace referencia a instrucciones SELECT de SQL que agregan datos transaccionales, normalmente mediante la inclusión de una cláusula GROUP BY. El tipo de índice denominado *columnstore* es fundamental para el análisis operativo.  
  
Hay dos escenarios principales:  
  
- El*análisis operativo por lotes* hace referencia a los procesos de agregación que se ejecutan cuando finaliza el horario laboral o bien en hardware secundario que tiene copias de los datos transaccionales.  
  - El[Almacenamiento de datos SQL de Azure](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-overview-what-is/) también está relacionado con el análisis operativo por lotes.  
- El*análisis operativo en tiempo real* hace referencia a los procesos de agregación que se ejecutan en horario laboral y en el hardware principal que se usa para cargas de trabajo transaccionales.  
  
  
El presente artículo se centra en OLTP y no en el análisis. Para obtener información sobre cómo los índices de almacén de columnas llevan el análisis a SQL, vea:  
  
- [Introducción al almacén de columnas para análisis operativos en tiempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)  
- [Descripción de los índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md)  
  
  
> [!NOTE]
> Hay disponible un vídeo de dos minutos sobre las características en memoria en [Azure SQL Database - In-Memory Technologies (Base de datos SQL de Azure: tecnologías en memoria)](https://channel9.msdn.com/Blogs/Windows-Azure/Azure-SQL-Database-In-Memory-Technologies). El vídeo tiene fecha de diciembre de 2015.  


### <a name="columnstore"></a>columnstore

Una secuencia de entradas de blog excelentes explica de manera elegante los índices de almacén de columnas desde varias perspectivas. En la mayoría de las publicaciones se describe más el concepto de análisis operacional en tiempo real, que es compatible con el almacén de columnas.  Sunil Agarwal, director de programas en Microsoft, creó estas entradas en marzo de 2016.

#### <a name="real-time-operational-analytics"></a>análisis operativo en tiempo real

1. [Análisis operativos en tiempo real mediante la tecnología In-Memory](https://blogs.technet.microsoft.com/dataplatforminsider/2015/12/09/real-time-operational-analytics-using-in-memory-technology/)
2. [Análisis operativos en tiempo real: información general del índice de almacén de columnas no agrupado (NCCI)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-using-nonclustered-columnstore-index/)
3. [Análisis operativos en tiempo real: ejemplo sencillo de uso de un índice de almacén de columnas no agrupado (NCCI) en SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/29/real-time-operational-analytics-simple-example-using-nonclustered-clustered-columnstore-index-ncci/)
4. [Análisis operativos en tiempo real: operaciones de DML e índice de almacén de columnas no agrupado (NCCI) en SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/04/real-time-operational-analytics-dml-operations-and-nonclustered-columnstore-index-ncci-in-sql-server-2016/)
5. [Análisis operativos en tiempo real: índices de almacén de columnas no agrupados y filtrados (NCCI)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-filtered-nonclustered-columnstore-index-ncci/)
6. [Análisis operativos en tiempo real: opción de retraso de compresión del índice de almacén de columnas no agrupado (NCCI)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-for-nonclustered-columnstore-index-ncci/)
7. [Análisis operativos en tiempo real: opción de retraso de compresión con NCCI y el rendimiento](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/06/real-time-operational-analytics-compression-delay-option-with-ncci-and-the-performance/)
8. [Análisis operativos en tiempo real: índice de almacén de columnas y tablas optimizadas para memoria](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/real-time-operational-analytics-memory-optimized-table-and-columnstore-index/)

#### <a name="defragment-a-columnstore-index"></a>Desfragmentar un índice de almacén de columnas.

1. [Desfragmentación del índice de almacén de columnas mediante el comando REORGANIZE](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/07/columnstore-index-defragmentation-using-reorganize-command/)
2. [Directiva de combinación del índice de almacén de columnas para REORGANIZE](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)

#### <a name="bulk-importation-of-data"></a>Importación masiva de datos

1. [Almacén de columnas agrupadas: carga masiva](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2014/07/27/clustered-column-store-index-bulk-loading-the-data/)
2. [Índice de almacén de columnas agrupado: optimizaciones de carga de datos: registro mínimo](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/10/clustered-columnstore-index-data-load-optimizations-minimal-logging/)
3. [Índice de almacén de columnas agrupado: optimizaciones de carga de datos: importación masiva en paralelo](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/02/28/clustered-columnstore-index-parallel-bulk-import/)





<a name="features-on-in-memory-oltp-13b"></a>  
  
## <a name="features-of-in-memory-oltp"></a>Característica de OLTP en memoria  
  
Veamos las características principales de OLTP en memoria.  
  
  
#### <a name="memory-optimized-tables"></a>Tablas optimizadas para memoria  
  
La palabra clave MEMORY_OPTIMIZED de T-SQL, en la instrucción CREATE TABLE, indica que se crea una tabla en la memoria activa, en lugar de en disco.  
  
  
Las [tablas con optimización para memoria](../../relational-databases/in-memory-oltp/memory-optimized-tables.md) tienen una representación de sí mismas en la memoria activa y una copia secundaria en el disco.  
  
- La copia del disco es para recuperación rutinaria después de un cierre y reinicio del servidor o de la base de datos. Esta dualidad de disco más memoria está oculta automáticamente y no se ve en el código.  
  
  
#### <a name="natively-compiled-modules"></a>Módulos compilados de forma nativa  
  
La palabra clave NATIVE_COMPILATION de T-SQL, en la instrucción CREATE PROCEDURE, indica que se crea un procedimiento almacenado compilado de forma nativa. Las instrucciones de T-SQL se compilan en el código máquina la primera vez que se usa el procedimiento nativo cada vez que la base de datos se recorre en línea. Las instrucciones de T-SQL ya no aguantan la interpretación lenta de cada instrucción.  
  
- Hemos visto el resultado de compilación nativa en duraciones de 1/100 de la duración interpretada.  
  
  
Un módulo nativo solamente puede hacer referencia a tablas optimizadas para memoria, y no a tablas basadas en disco.  
  
Hay tres tipos de módulos compilados de forma nativa:  
  
- [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
- Funciones definidas por el usuario (UDF) compiladas de forma nativa, que son escalares.  
- Desencadenadores compilados de forma nativa.  
  
  
#### <a name="availability-in-azure-sql-database"></a>Disponibilidad en Base de datos SQL de Azure  
  
OLTP en memoria y Almacén de columnas están disponibles en Azure SQL Database. Para detalles, consulte [Optimize Performance using In-Memory Technologies in SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory) (Optimizar el rendimiento con las tecnologías In-Memory en SQL Database).
  
  
<a name="ensure-compatibility-level-gteq-130-99c"></a>  
  
## <a name="1-ensure-compatibility-level--130"></a>1. Garantizar un compatibilidad >= 130  
  
  
Esta sección es la primera de una serie de secciones numeradas que muestran la sintaxis de Transact-SQL que puede usar para implementar características de OLTP en memoria.  
  
  
En primer lugar, es importante que la base de datos se establezca en un nivel de compatibilidad de al menos 130. A continuación figura el código de T-SQL para ver el nivel de compatibilidad actual en el que está establecida la base de datos actual.  
  
```sql
SELECT d.compatibility_level
    FROM sys.databases as d
    WHERE d.name = Db_Name();
```
  
  
  
A continuación figura el código de T-SQL para actualizar el nivel, si es necesario.  
  
  
  
```sql
ALTER DATABASE CURRENT
    SET COMPATIBILITY_LEVEL = 130;
```
  
  
  
<a name="elevate-to-snapshot-26n"></a>  
  
## <a name="2-elevate-to-snapshot"></a>2. Elevar a SNAPSHOT  
  
  
Cuando una transacción implica una tabla basada en disco y una tabla optimizada para memoria, la llamamos *transacción entre contenedores*. En una transacción de este tipo es esencial que la parte optimizada para memoria de la transacción funcione en el nivel de aislamiento de la transacción llamado SNAPSHOT.  
  
Para exigir de forma confiable este nivel para tablas optimizadas para memoria en una transacción entre contenedores, [modifique la configuración de la base de datos](../../t-sql/statements/alter-database-transact-sql-set-options.md) ejecutando el siguiente código T-SQL.  
  
  
  
```sql
ALTER DATABASE CURRENT
    SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
```
  
  
  
<a name="create-an-optimized-filegroup-24r"></a>  
  
## <a name="3-create-an-optimized-filegroup"></a>3. Crear un grupo de archivos optimizado  
  
  
En Microsoft SQL Server, antes de poder crear una tabla optimizada para memoria debe crear un grupo de archivos que declara CONTAINS MEMORY_OPTIMIZED_DATA. El grupo de archivos se asigna a la base de datos. Para obtener detalles, vea:  
  
- [FILEGROUP con optimización para memoria](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
  
En Azure SQL Database, no es necesario y no se puede crear tal grupo de archivos.  

El siguiente ejemplo de script T-SQL habilita una base de datos para OLTP en memoria y configura todos los ajustes recomendados. Funciona con SQL Server y Azure SQL Database: [enable-in-memory-oltp.sql](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/in-memory-database/in-memory-oltp/t-sql-scripts/enable-in-memory-oltp.sql).

Tenga en cuenta que no todas las características de SQL Server son compatibles con las bases de datos que tienen un grupo de archivos MEMORY_OPTIMIZED_DATA. Para obtener más información sobre las limitaciones, vea: [Características de SQL Server no admitidas para OLTP en memoria](unsupported-sql-server-features-for-in-memory-oltp.md)
  
<a name="create-a-memory-optimized-table-26y"></a>  
  
## <a name="4-create-a-memory-optimized-table"></a>4. Crear una tabla optimizada para memoria  
  
La palabra clave de Transact-SQL fundamental es la palabra clave MEMORY_OPTIMIZED.  
  
  
  
```sql
CREATE TABLE dbo.SalesOrder
    (
        SalesOrderId   integer   not null   IDENTITY
            PRIMARY KEY NONCLUSTERED,
        CustomerId   integer    not null,
        OrderDate    datetime   not null
    )
        WITH
            (MEMORY_OPTIMIZED = ON,
            DURABILITY = SCHEMA_AND_DATA);
```
  
  
  
Las instrucciones INSERT y SELECT de Transact-SQL en una tabla optimizada para memoria son las mismos que para una tabla normal.  
  
#### <a name="alter-table-for-memory-optimized-tables"></a>ALTER TABLE para tablas con optimización para memoria  
  
ALTER TABLE... ADD/DROP puede agregar o quitar una columna de una tabla optimizada para memoria o un índice.  
  
- CREATE INDEX y DROP INDEX no se pueden ejecutar en una tabla optimizada para memoria, use ALTER TABLE ... ADD/DROP INDEX en su lugar.  
- Para obtener detalles, vea [Modificar tablas con optimización para memoria](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md).  
  
  
#### <a name="plan-your-memory-optimized-tables-and-indexes"></a>Planear sus índices y tablas optimizadas para memoria  
  
  
- [Índices de tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)  
- [Construcciones de Transact-SQL no admitidas en In-Memory OLTP.](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
  
<a name="create-a-natively-compiled-stored-procedure-native-proc-29u"></a>  
  
## <a name="5-create-a-natively-compiled-stored-procedure-native-proc"></a>5. Crear un procedimiento almacenado compilado de forma nativa (procedimiento nativo)  
  
  
La palabra clave fundamental es NATIVE_COMPILATION.  
  
  
  
```sql
CREATE PROCEDURE ncspRetrieveLatestSalesOrderIdForCustomerId  
        @_CustomerId   INT  
        WITH  
            NATIVE_COMPILATION,  
            SCHEMABINDING  
    AS  
    BEGIN ATOMIC  
        WITH  
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'us_english')  
      
        DECLARE @SalesOrderId int, @OrderDate datetime;
      
        SELECT TOP 1  
                @SalesOrderId = s.SalesOrderId,  
                @OrderDate    = s.OrderDate  
            FROM dbo.SalesOrder AS s  
            WHERE s.CustomerId = @_CustomerId  
            ORDER BY s.OrderDate DESC;  
      
        RETURN @SalesOrderId;  
    END;  
```
  
  
  
La palabra clave SCHEMABINDING significa que las tablas a las que se hace referencia en el procedimiento nativo no se puede quitar a menos que dicho procedimiento se quite primero. Para obtener detalles, vea [Crear procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md).  
  
Tenga en cuenta que no es necesario crear un procedimiento almacenado compilado de forma nativa para tener acceso a una tabla optimizada en memoria. También puede hacer referencia a tablas optimizadas en memoria desde procedimientos almacenados tradicionales y desde lotes ad hoc.
  
<a name="execute-the-native-proc-31e"></a>  
  
## <a name="6-execute-the-native-proc"></a>6. Ejecutar el procedimiento nativo  
  
  
Rellene la tabla con dos filas de datos.  
  
  
  
```sql
INSERT into dbo.SalesOrder  
        ( CustomerId, OrderDate )  
    VALUES  
        ( 42, '2013-01-13 03:35:59' ),
        ( 42, '2015-01-15 15:35:59' );
```
  
  
  
Después seguirá una llamada EXECUTE al procedimiento almacenado compilado de forma nativa.  
  
  
  
```sql
DECLARE @LatestSalesOrderId int, @mesg nvarchar(128);
      
EXECUTE @LatestSalesOrderId =  
    ncspRetrieveLatestSalesOrderIdForCustomerId 42;
      
SET @mesg = CONCAT(@LatestSalesOrderId,  
    ' = Latest SalesOrderId, for CustomerId = ', 42);
PRINT @mesg;  
```
      
    -- Here is the actual PRINT output:  
    -- 2 = Latest SalesOrderId, for CustomerId = 42  
  
  
  
  
<a name="guide-to-the-documentation-and-next-steps-32w"></a>  
  
### <a name="guide-to-the-documentation-and-next-steps"></a>Guía de la documentación y pasos siguientes  
  
  
Los ejemplos anteriores sin formato constituyen una base para aprender las características más avanzadas de OLTP en memoria. Las secciones siguientes constituyen una guía a las consideraciones especiales que convendría conocer y dónde puede encontrar los detalles sobre cada una de ellas.  
  
  
  
<a name="how-do-in-memory-oltp-features-work-so-much-faster-33v"></a>  
  
## <a name="how-in-memory-oltp-features-work-so-much-faster"></a>¿Cómo funcionan las características de OLTP en memoria tan rápido?  
  
  
Las siguientes subsecciones describen brevemente cómo funcionan las características de OLTP en memoria internamente para proporcionar un rendimiento mejorado.  
  
  
<a name="how-do-memory-optimized-tables-perform-faster-34q"></a>  
  
### <a name="how-memory-optimized-tables-perform-faster"></a>¿Cómo funcionan las tablas optimizadas para memoria más rápido?  
  
  
**Naturaleza doble:** una tabla optimizada para memoria tiene una naturaleza doble: una representación en memoria activa y la otra en el disco duro. Cada transacción se confirma con ambas representaciones de la tabla. Las transacciones funcionan en la representación memoria activa mucho más rápida. Las tablas con optimización para memoria se benefician de la mayor velocidad de la memoria activa en comparación con el disco. Además, la mayor agilidad de la memoria activa hace práctica una estructura de tabla más avanzada que se optimiza para velocidad. La estructura avanzada tampoco tiene páginas, por lo que evita la sobrecarga y la contención de bloqueos temporales y bloqueos por subproceso.  
  
  
**No hay bloqueos:** la tabla optimizada para memoria se basa en un enfoque *optimista* de los objetivos de la competencia de integridad de datos frente a la simultaneidad y el alto rendimiento. Durante la transacción, la tabla no coloca bloqueos en ninguna versión de las filas de datos actualizadas. Esto puede reducir considerablemente la contención en algunos sistemas de gran volumen.  
  
  
**Versiones de fila:** en lugar de bloqueos, la tabla optimizada para memoria agrega una versión nueva de una fila actualizada en la propia tabla, no en tempdb. La fila original se mantiene hasta que se confirma la transacción. Durante la transacción, otros procesos pueden leer la versión original de la fila.  
  
- Cuando se crean varias versiones de una fila para una tabla basada en disco, las versiones de fila se almacenan temporalmente en tempdb.  
  
  
**Menos tareas de registro:** las versiones anterior y posterior de las filas actualizadas se mantienen en la tabla optimizada para memoria. El par de filas proporciona gran parte de la información que tradicionalmente se escribe en el archivo de registro. Esto permite al sistema escribir menos información y con menos frecuencia en el registro. Aún así, la integridad transaccional está garantizada.  
  
  
<a name="how-do-native-procs-perform-faster-35x"></a>  
  
### <a name="how-native-procs-perform-faster"></a>¿Cómo funcionan los procedimientos nativos más rápido?  
  
Convertir un procedimiento almacenado interpretado normal en un procedimiento almacenado compilado de forma nativa, reduce considerablemente el número de instrucciones que se ejecutan en tiempo de ejecución.  
  
  
<a name="trade-offs-of-in-memory-features-36j"></a>  
  
## <a name="trade-offs-of-in-memory-features"></a>Ventajas e inconvenientes de las características en memoria  
  
  
Como es habitual en informática, las mejoras de rendimiento que ofrecen las características en memoria son una solución de compromiso. Las mejores características ofrecen beneficios que son más valiosos que los costos adicionales de la característica. Puede encontrar instrucciones completas sobre los compromisos en:

- [Planear la adopción de características de OLTP en memoria en SQL Server](../../relational-databases/in-memory-oltp/plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)

En el resto de esta sección se enumeran algunas de las consideraciones principales de planeación y compromiso.
  
<a name="trade-offs-of-memory-optimized-tables-37d"></a>  
  
### <a name="trade-offs-of-memory-optimized-tables"></a>Ventajas e inconvenientes de las tablas optimizadas para memoria  
  
  
**Calcular la memoria:** debe calcular la cantidad de memoria activa que consumirá la tabla optimizada para memoria. El equipo debe tener la capacidad de memoria suficiente para hospedar una tabla optimizada para memoria. Para obtener detalles, vea:  
  
- [Supervisar y solucionar problemas de uso de memoria](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)  
- [Estimar los requisitos de memoria para las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)  
- [Tamaño de tabla y fila de las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)  
  
  
**Dividir la tabla grande:** una manera de satisfacer la demanda de grandes cantidades de memoria activa es dividir la tabla grande en partes en memoria que almacenen filas de datos *recientes frecuentes* frente a otras partes en el disco que almacenen filas *heredadas inactivas* (por ejemplo, pedidos de ventas que se han enviado y completado totalmente). Esta división es un proceso manual de diseño e implementación. Consulte:  
  
- [Creación de particiones en el nivel de aplicación](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
- [Patrón de aplicación para crear particiones de tablas con optimización para memoria](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
<a name="trade-offs-of-native-procs-38p"></a>  
  
### <a name="trade-offs-of-native-procs"></a>Ventajas e inconvenientes de los procedimientos nativos  
  
- Un procedimiento almacenado compilado de forma nativa no puede acceder a una tabla basada en disco. Un procedimiento nativo solo puede acceder a tablas optimizadas en memoria.  
- Cuando se ejecuta un procedimiento nativo por primera vez después de que el servidor o base de datos vuelve a estar en línea, el procedimiento nativo se debe compilar de nuevo una vez. Esto provoca un retraso antes de que el procedimiento nativo empieza a ejecutarse.  
  
<a name="advanced-considerations-for-memory-optimized-tables-39n"></a>  
  
## <a name="advanced-considerations-for-memory-optimized-tables"></a>Consideraciones avanzadas sobre tablas optimizadas para memoria  
  
Los[índices de tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md) difieren en algunos aspectos de los índices de las tablas en disco tradicionales. Los índices de hash solo están disponibles en las tablas optimizadas para memoria.
    
- [Índices de hash de tablas con optimización para memoria](../../relational-databases/sql-server-index-design-guide.md#hash_index)
- [Índice no agrupado de tablas optimizadas para memoria](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index) 
  
Debe tener un plan para asegurarse de que haya suficiente memoria activa para la tabla optimizada para memoria planeada y sus índices. Consulte:  
  
- [Crear y administrar el almacenamiento de objetos optimizados para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
Es posible declarar una tabla optimizada para memoria con DURABILITY = SCHEMA_ONLY:  
  
- Esta sintaxis indica al sistema que descarte todos los datos de la tabla optimizada para memoria cuando la base de datos se desconecta. Solo se conserva la definición de tabla.  
- Cuando la base de datos vuelva a estar en línea, la tabla optimizada para memoria se vuelve a cargar en la memoria activa, vacía de datos.  
- Las tablas SCHEMA_ONLY pueden ser una mejor [alternativa a las tablas temporales](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) en tempdb, cuando hay implicados varios miles de filas.  
  
Las variables de tabla también pueden declararse como optimizadas para memoria. Consulte:  
  
- [Tabla temporal y variable de tabla más rápidas con optimización para memoria](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)  
  
<a name="advanced-considerations-for-natively-compiled-modules-40k"></a>  
  
## <a name="advanced-considerations-for-natively-compiled-modules"></a>Consideraciones avanzadas para módulos compilados de forma nativa  
  
Los tipos de módulos compilados de forma nativa disponibles a través de Transact-SQL son:  
  
- Procedimientos almacenados compilados de forma nativa (procedimientos nativos).  
- [Funciones escalares definidas por el usuario](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)compiladas de forma nativa.  
- Desencadenadores compilados de forma nativa (desencadenadores nativos).  
  - Solo los desencadenadores compilados de forma nativa se permiten en tablas optimizadas para memoria.  
- [Funciones con valores de tabla](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)compiladas de forma nativa.  
  - [Mejora del rendimiento de la tabla temporal y de variable de tabla mediante optimización de memoria](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)  
  
Una función definida por el usuario (UDF) compilada de forma nativa se ejecuta más rápido que una UDF interpretada. Debe tener en cuenta lo siguiente con respecto a las UDF:  
  
- Cuando una instrucción SELECT de T-SQL usa una UDF, siempre se llama una vez a la UDF por cada fila devuelta.  
  - Las UDF nunca se ejecutan en línea, sino que siempre se llaman.  
  - La distinción compilada es menos significativa de lo que es la sobrecarga de llamadas repetidas que es inherente a todas las UDF.  
  - A pesar de ello, la sobrecarga de llamadas a UDF suele ser aceptable en la práctica.  
  
Para obtener datos de prueba y una explicación del rendimiento de UDF nativas, vea:  
  
  - [Suavizar el impacto de RBAR con UDF compiladas de forma nativa en SQL Server 2016](https://blogs.msdn.microsoft.com/sqlcat/2016/02/17/soften-the-rbar-impact-with-native-compiled-udfs-in-sql-server-2016/)  
  - Entrada de blog [Natively Compiled User Defined Functions](https://sqlinthewild.co.za/index.php/2016/01/12/natively-compiled-user-defined-functions/) (Funciones definidas por el usuario compiladas de forma nativa) de Gail Shaw, con fecha de enero de 2016.  
  
<a name="documentation-guide-for-memory-optimized-tables-41z"></a>  
  
## <a name="documentation-guide-for-memory-optimized-tables"></a>Guía de documentación para tablas optimizadas para memoria  
  
Consulte estos otros artículos que tratan consideraciones especiales para tablas optimizadas para memoria:  
  
- [Migrar a OLTP en memoria](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  - [Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)  
  - El informe de análisis rendimiento de transacciones de SQL Server Management Studio ayuda a evaluar si OLTP en memoria mejorará el rendimiento de la aplicación de base de datos.  
  - Utilice el [Asesor de optimización de memoria](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) que le ayudarán a migrar la tabla de base de datos basada en disco a OLTP en memoria.   
- [Hacer copia de seguridad, restaurar y recuperar tablas con optimización para memoria](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  - El almacenamiento usado por las tablas optimizadas para memoria puede ser mucho mayor que el tamaño de la memoria y eso afecta al tamaño de la copia de seguridad de la base de datos.  
- [Transacciones con tablas con optimización para memoria](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)  
  - Incluye información sobre la lógica de reintento en T-SQL para las transacciones en tablas optimizadas para memoria.  
- [Compatibilidad de Transact-SQL con OLTP en memoria](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  - Los tipos de datos y T-SQL admitidos y no admitidos, para tablas optimizadas para memoria y procedimientos nativos.  
- [Enlazar una base de datos con tablas con optimización para memoria a un grupo de recursos de servidor](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md), que analiza una consideración avanzada opcional.  

<a name="documentation-guide-for-native-procs-42b"></a>  
  
## <a name="documentation-guide-for-native-procs"></a>Guía de documentación para procedimientos nativos  

El siguiente artículo, y los artículos secundarios en la tabla de contenido (TOC), explican los detalles sobre los procedimientos almacenados compilados de forma nativa.

- [Procedimientos almacenados compilados de forma nativa](natively-compiled-stored-procedures.md)
  
<a name="related-links-43f"></a>  
  
## <a name="related-links"></a>Vínculos relacionados  
  
- Artículo inicial: [In-Memory OLTP (optimización In-Memory)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
    
Los artículos siguientes incluyen código para demostrar las mejoras de rendimiento que se pueden lograr con el uso de OLTP en memoria:  
  
- [Demostración: mejora de rendimiento de OLTP en memoria](../../relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp.md) ofrece una demostración a pequeña escala de las posibles mejoras de rendimiento más grandes.  
- [Sample Database for In-Memory OLTP (Base de datos de ejemplo para OLTP en memoria)](../../relational-databases/in-memory-oltp/sample-database-for-in-memory-oltp.md) ofrece una demostración de escala mayor.  
