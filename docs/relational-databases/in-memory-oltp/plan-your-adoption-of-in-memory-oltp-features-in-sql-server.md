---
title: "Planeación de la adopción de características de OLTP en memoria en SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 041b428f-781d-4628-9f34-4d697894e61e
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4404ee4d70ed16ddaad5d0600f5d37225897d455
ms.lasthandoff: 04/11/2017

---
# <a name="plan-your-adoption-of-in-memory-oltp-features-in-sql-server"></a>Planear la adopción de características de OLTP en memoria en SQL Server
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]


En este artículo se describen las maneras en las que la adopción de características en memoria afecta a otros aspectos del sistema empresarial.



## <a name="a-adoption-of-in-memory-oltp-features"></a>A. Adopción de características de OLTP en memoria


En las siguientes subsecciones se tratan los factores que debe considerar cuando planee adoptar e implementar características en memoria. Puede encontrar información explicativa disponible en:

- [Uso de In-Memory OLTP (vista previa) para mejorar el rendimiento de la aplicación de Azure SQL Database](https://azure.microsoft.com/documentation/articles/sql-database-in-memory-oltp-migration/)



### <a name="a1-prerequisites"></a>A.1 Requisitos previos

Un requisito previo para usar las características en memoria puede implicar el nivel de servicio o la edición del producto SQL. Para este y otros requisitos previos, consulte:

- [Requisitos para utilizar las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)
    - [Ediciones y componentes de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
    - [Recomendaciones sobre el nivel de precios de bases de datos SQL](https://azure.microsoft.com/documentation/articles/sql-database-service-tier-advisor/)


### <a name="a2-forecast-the-amount-of-active-memory"></a>A.2 Previsión de la cantidad de memoria activa

¿Tiene su sistema suficiente memoria activa para admitir una tabla nueva con optimización para memoria?

#### <a name="microsoft-sql-server"></a>Microsoft SQL Server

Una tabla con optimización para memoria que contiene 200 GB de datos requiere que más de 200 GB de memoria activa se dediquen a su soporte. Antes de implementar una tabla con optimización para memoria que contenga gran cantidad de datos, debe prever la cantidad de memoria activa adicional que va a necesitar agregar a su equipo servidor. Para obtener una guía de estimación, consulte:

- [Estimar los requisitos de memoria para las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)

#### <a name="azure-sql-database"></a>Base de datos SQL de Azure

Para una base de datos hospedada en el servicio en la nube de Base de datos SQL de Azure, el nivel de servicio elegido afecta a la cantidad de memoria activa que la base de datos puede consumir. Debe planear la supervisión del uso de memoria de la base de datos mediante una alerta. Para obtener detalles, consulte:

- [Supervisión del almacenamiento OLTP en memoria](https://azure.microsoft.com/documentation/articles/sql-database-in-memory-oltp-monitoring/)

#### <a name="memory-optimized-table-variables"></a>Variables de tabla con optimización para memoria

A veces, una variable de tabla que se declara como tabla con optimización para memoria es preferible a una #TempTable tradicional que resida en la base de datos **tempdb** . Dichas variables de tabla pueden proporcionar mejoras de rendimiento significativas sin usar grandes cantidades de memoria activa.

### <a name="a3-table-must-be-offline-to-convert-to-memory-optimized"></a>A.3 La tabla debe estar sin conexión para convertirse en una con optimización para memoria

Algunas características de ALTER TABLE están disponibles para las tablas con optimización para memoria. Pero no puede emitir una instrucción ALTER TABLE para convertir una tabla basada en disco en una tabla con optimización para memoria. En su lugar, debe usar un conjunto de pasos más manual. Lo que se muestra a continuación son varias maneras en las que puede convertir su tabla basada en disco en una con optimización para memoria.

#### <a name="manual-scripting"></a>Scripting manual

Una manera de convertir su tabla basada en disco en una con optimización para memoria es codificar los pasos de Transact-SQL necesarios.


1. Suspenda la actividad de la aplicación.

2. Realice una copia de seguridad completa.

3. Cambie el nombre de la tabla basada en disco.

4. Emita una instrucción CREATE TABLE para crear su nueva tabla con optimización para memoria.

5. Inserte en la tabla con optimización para memoria con una instrucción sub-SELECT desde la tabla basada en disco.

6. Quite la tabla basada en disco.

7. Realice otra copia de seguridad completa.

8. Reanude la actividad de la aplicación.


#### <a name="memory-optimization-advisor"></a>Asesor de optimización de memoria

La herramienta Asistente de optimización de memoria puede generar un script para ayudarle a implementar la conversión de una tabla basada en disco a una tabla con optimización para memoria. La herramienta se instala como parte de SQL Server Data Tools (SSDT).

- [Asesor de optimización de memoria](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md)
- [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)


#### <a name="dacpac-file"></a>archivo .dacpac

Puede actualizar su base de datos local mediante un archivo .dacpac administrado por SSDT. En SSDT, puede especificar los cambios en el esquema que está codificado en el archivo .dacpac.

Trabaja con archivos .dacpac en el contexto de un proyecto de Visual Studio de tipo *Database*.

- [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md) y archivos .dacpac



### <a name="a4-guidance-for-whether-in-memory-oltp-features-are-right-for-your-application"></a>A.4 Instrucciones sobre si las características de OLTP en memoria son adecuadas para su aplicación

Para obtener instrucciones sobre si las características en memoria pueden mejorar el rendimiento de su aplicación particular, consulte:

- [OLTP en memoria (optimización en memoria)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)



## <a name="b-unsupported-features"></a>B. Características no admitidas

Las características que no se admiten en determinados escenarios en memoria se describen en:

- [Características de SQL Server no admitidas para OLTP en memoria](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


En las siguientes subsecciones se destacan algunas de las características no admitidas más importantes.


### <a name="b1-snapshot-of-a-database"></a>B.1 Instantánea de una base de datos

Después de que cualquier módulo o tabla con optimización para memoria se cree por primera vez en una base de datos determinada, nunca puede tomarse ninguna [instantánea](../../relational-databases/databases/database-snapshots-sql-server.md) de la base de datos. La razón específica es que:

- El primer elemento con optimización para memoria hace imposible quitar alguna vez el último archivo del grupo de archivos con optimización para memoria; y
- Ninguna base de datos que tenga un archivo en un grupo de archivos con optimización para memoria puede admitir una instantánea.

Normalmente, una instantánea puede ser útil para las iteraciones de pruebas rápidas.


### <a name="b2-cross-database-queries"></a>B.2 Consultas entre bases de datos

Las tablas con optimización para memoria no admiten las transacciones [entre bases de datos](../../relational-databases/in-memory-oltp/cross-database-queries.md) . No puede tener acceso a otra base de datos desde la misma transacción o desde la misma consulta que tiene acceso también a una tabla con optimización para memoria.

Las variables de tabla no son transaccionales. Por tanto, las [variables de tabla con optimización para memoria](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) pueden usarse en consultas entre bases de datos.


### <a name="b3-readpast-table-hint"></a>B.3 Sugerencia de tabla READPAST

Ninguna consulta puede aplicar la [sugerencia de tabla](../../t-sql/queries/hints-transact-sql-table.md) READPAST a ninguna tabla con optimización para memoria.

La sugerencia READPAST es útil en escenarios donde varias sesiones están teniendo acceso y modificando el mismo conjunto pequeño de filas, como en el procesamiento de una cola.


### <a name="b4-rowversion-sequence"></a>B.4 RowVersion, Sequence

- Ninguna columna puede etiquetarse para [RowVersion](../../t-sql/data-types/rowversion-transact-sql.md) en una tabla con optimización para memoria.


- Un objeto [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) no puede usarse con ninguna tabla con optimización para memoria.


## <a name="c-administrative-maintenance"></a>C. Mantenimiento administrativo


En esta sección se describen las diferencias en la administración de base de datos donde se usan las tablas con optimización para memoria.


### <a name="c1-identity-seed-reset-increment--1"></a>C.1 Restablecimiento del valor de inicialización de la identidad, incremento > 1

Para reinicializar una columna IDENTITY, [DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md) no puede usarse en una tabla con optimización para memoria.

El valor de incremento está restringido a exactamente 1 para una columna IDENTITY en una tabla con optimización para memoria.


### <a name="c2-dbcc-checkdb-cannot-validate-memory-optimized-tables"></a>C.2 DBCC CHECKDB no puede validar tablas con optimización para memoria

El comando [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) no hace nada cuando su destino es una tabla con optimización para memoria. Los pasos siguientes son una solución alternativa:


1. [Realice una copia de seguridad del registro de transacciones](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).

2. Realice una copia de seguridad de los archivos del grupo de archivos con optimización para memoria en un dispositivo NULL. El proceso de copia de seguridad invoca una validación de suma de comprobación.

    Si se encuentran daños, siga con los pasos siguientes.

3. Copie los datos de sus tablas con optimización para memoria en tablas basadas en disco para un almacenamiento temporal.

4. Restaure los archivos del grupo de archivos con optimización para memoria.

5. Inserte en la tabla con optimización para memoria los datos que ha almacenado temporalmente en las tablas basadas en disco.

6. Quite las tablas basadas en disco que contenían los datos de manera temporal.



## <a name="d-performance"></a>D. Rendimiento

En esta sección se describen situaciones en las que el excelente rendimiento de las tablas con optimización para memoria se mantiene por debajo de todo su potencial.


### <a name="d1-index-considerations"></a>D.1 Consideraciones de índice

Todos los índices de una tabla con optimización para memoria se crean y administran mediante las instrucciones CREATE TABLE y ALTER TABLE relacionadas con las tablas. No puede dirigirse a una tabla con optimización para memoria con una instrucción CREATE INDEX.

El índice no agrupado tradicional de árbol B a menudo es la elección sencilla y razonable cuando implementa una tabla con optimización para memoria por primera vez. Después, cuando vea cómo actúa la aplicación, puede considerar la posibilidad de cambiar a otro tipo de índice.

Dos tipos de índices especiales necesitan tratarse en el contexto de una tabla con optimización para memoria: los índices de hash y los índices de almacén de columnas.

Para obtener información general de los índices de las tablas con optimización para memoria, consulte:

- [Índices de tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)


#### <a name="hash-indexes"></a>Índices de hash

Los índices de hash pueden ser el formato más rápido para tener acceso a una fila específica por su valor exacto de clave principal mediante el operador '**=**'.

- Los operadores inexactos como '**!=**', '**>**' o '**BETWEEN**' perjudicarían el rendimiento si se usaran con un índice de hash.

- Un índice de hash puede que no sea la mejor opción si la tasa de duplicación del valor principal es demasiado alta.

- Sea precavido a la hora de subestimar cuántos *depósitos* puede necesitar su índice de hash para evitar largas cadenas en depósitos individuales. Para obtener detalles, consulte:
    - [Índices de hash de tablas con optimización para memoria](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)


#### <a name="nonclustered-columnstore-indexes"></a>Índices no agrupados de almacén de columnas

Las tablas con optimización para memoria proporcionan un alto rendimiento de los datos típicos transaccionales empresariales, en el paradigma que denominamos *procesamiento de transacciones en línea* u *OLTP*. Los índices de almacén de columnas proporcionan un alto rendimiento de agregaciones y un procesamiento similar denominado *Analytics*. En los últimos años, el mejor enfoque disponible para satisfacer las necesidades de OLTP y Analytics era tener tablas independientes con un gran movimiento de datos, y con un cierto grado de duplicación de datos. Hoy en día, está disponible una **solución híbrida** más sencilla: tener un índice de almacén de columnas en una tabla con optimización para memoria.


- Un [índice de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md) puede crearse en una tabla basada en disco, incluso como el índice agrupado. Pero en una tabla con optimización para memoria no puede agruparse un índice de almacén de columnas.


- Las columnas no consecutivas o de LOB de una tabla con optimización para memoria evitan la creación de un índice de almacén de columnas en la tabla.


- No puede ejecutarse ninguna instrucción ALTER TABLE en una tabla con optimización para memoria mientras exista un índice de almacén de columnas en la tabla.
    - Desde agosto de 2016, Microsoft tiene planes a corto plazo para mejorar el rendimiento a la hora de volver a crear el índice de almacén de columnas.



### <a name="d2-lob-and-off-row-columns"></a>D.2 Columnas no consecutivas y de LOB

Los objetos grandes (LOB) son columnas de tipos como varchar(**max**). Probablemente, tener un par de columnas de LOB en una tabla con optimización para memoria no perjudica el rendimiento lo suficiente para que sea preocupante. Pero evite tener más columnas de LOB de las que necesitan sus datos. El mismo consejo se aplica a las columnas no consecutivas. No defina una columna como nvarchar(3072) si varchar(512) es suficiente.


Puede encontrar más información sobre columnas no consecutivas y de LOB en:

- [Tamaño de tabla y fila de las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)
- [Tipos de datos admitidos para OLTP en memoria](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)



## <a name="e-limitations-of-native-procs"></a>E. Limitaciones de los procedimientos nativos


No se admiten determinados elementos de Transact-SQL en procedimientos almacenados compilados de forma nativa.

Para obtener consideraciones al migrar un script de Transact-SQL a un procedimiento nativo, consulte:

- [Problemas de migración para los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)


### <a name="e1-no-case-in-a-native-proc"></a>E.1 Ninguna expresión CASE en un procedimiento nativo

La expresión CASE en Transact-SQL no puede usarse dentro de un procedimiento nativo. Puede crear una solución alternativa:

- [Implementación de una expresión CASE de un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md)


### <a name="e2-no-merge-in-a-native-proc"></a>E.2 Ninguna instrucción MERGE en un procedimiento nativo


La [instrucción MERGE](../../t-sql/statements/merge-transact-sql.md) de Transact-SQL tiene similitudes con lo que a menudo se denomina característica *upsert* . Un procedimiento nativo no puede usar la instrucción MERGE. En cambio, puede conseguir la misma función de MERGE al usar una combinación de instrucciones SELECT más UPDATE más INSERT. Puede encontrar un ejemplo de código en:

- [Implementación de la funcionalidad MERGE en un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/implementing-merge-functionality-in-a-natively-compiled-stored-procedure.md)



### <a name="e3-no-joins-in-update-or-delete-statements-in-a-native-proc"></a>E.3 Ninguna combinación en instrucciones UPDATE o DELETE en un procedimiento nativo

Las instrucciones de Transact-SQL en un procedimiento nativo solo pueden tener acceso a las tablas con optimización para memoria. En las instrucciones UPDATE y DELETE no puede combinar ninguna tabla. Los intentos en un procedimiento nativo producen un error con un mensaje como Msg 12319 que explica que:

- No puede usar la cláusula FROM en una instrucción UPDATE.
- No puede especificar un origen de tabla en una instrucción DELETE.

Ningún tipo de subconsulta proporciona una solución alternativa. En cambio, puede usar una variable de tabla con optimización para memoria para lograr un resultado de combinación en varias instrucciones. Aquí se muestran dos ejemplos de código:

- DELETE...JOIN... queremos ejecutar en un procedimiento nativo, pero no podemos.
- Un conjunto de soluciones alternativas de instrucciones de Transact-SQL que consigue la combinación de eliminación.


*Escenario:* la tabla TabProjectEmployee tiene una clave única de dos columnas: ProjectId y EmployeeId. Cada fila indica la asignación de un empleado a un proyecto activo. Cuando un empleado deja la empresa, el empleado debe eliminarse de la tabla TabProjectEmployee.


#### <a name="invalid-t-sql-deletejoin"></a>T-SQL no válido, DELETE...JOIN


Un procedimiento nativo no puede tener una instrucción DELETE...JOIN como se muestra a continuación.


```tsql
DELETE pe
    FROM
             TabProjectEmployee   AS pe
        JOIN TabEmployee          AS e

            ON pe.EmployeeId = e.EmployeeId
    WHERE
            e.EmployeeStatus = 'Left-the-Company'
;
```


#### <a name="valid-work-around-manual-deletejoin"></a>Solución alternativa válida, DELETE...JOIN manual

A continuación, se muestra el ejemplo de código de la solución alternativa en dos partes:

1. CREATE TYPE se ejecuta una vez, días antes de que el tipo se haya usado por primera vez por cualquier variable de tabla actual.

2. El proceso de negocio usa el tipo que se ha creado. Comienza al declarar una variable de tabla del tipo de tabla que se ha creado.


```tsql

CREATE TYPE dbo.type_TableVar_EmployeeId
    AS TABLE  
    (
        EmployeeId   bigint   NOT NULL
    );
```


Después, use el tipo de creación de tabla.


```tsql
DECLARE @MyTableVarMo  dbo.type_TableVar_EmployeeId  

INSERT INTO @MyTableVarMo (EmployeeId)
    SELECT
            e.EmployeeId
        FROM
                 TabProjectEmployee  AS pe
            JOIN TabEmployee         AS e  ON e.EmployeeId = pe.EmployeeId
        WHERE
            e.EmployeeStatus = 'Left-the-Company'
;

DECLARE @EmployeeId   bigint;

WHILE (1=1)
BEGIN
    SET @EmployeeId = NULL;

    SELECT TOP 1 @EmployeeId = v.EmployeeId
        FROM @MyTableVarMo  AS v;

    IF (NULL = @Employeed) BREAK;
    
    DELETE TabProjectEmployee
        WHERE EmployeeId = @EmployeeId;

    DELETE @MyTableVarMo
        WHERE EmployeeId = @EmployeeId;
END;
```


### <a name="e4-query-plan-limitations-for-native-procs"></a>E.4 Limitaciones del plan de consulta de los procedimientos nativos


Algunos tipos de planes de consulta no están disponibles en los procedimientos nativos. Muchos de los detalles se tratan en:

- [Guía del procesamiento de consultas para tablas con optimización para memoria](../../relational-databases/in-memory-oltp/a-guide-to-query-processing-for-memory-optimized-tables.md)


#### <a name="no-parallel-processing-in-a-native-proc"></a>No existe un procesamiento paralelo en un procedimiento nativo

El procesamiento paralelo no puede formar parte de ningún plan de consulta de un procedimiento nativo. Los procedimientos nativos siempre son de subproceso único.


#### <a name="join-types"></a>Tipos de combinación


Ni una combinación hash ni una combinación de mezcla pueden ser parte de ningún plan de consulta de un procedimiento nativo. Se usan las combinaciones de bucle anidado.


#### <a name="no-hash-aggregation"></a>Ninguna agregación hash

Cuando el plan de consulta de un procedimiento nativo requiere una fase de agregación, solo está disponible la agregación de flujo. La agregación hash no se admite en un plan de consulta de un procedimiento nativo.

- La agregación hash es mejor cuando deben agregarse los datos de un gran número de filas.



## <a name="f-application-design-transactions-and-retry-logic"></a>F. Diseño de aplicación: transacciones y lógica de reintento

Una transacción que implica una tabla con optimización para memoria puede llegar a ser dependiente de otra transacción que implique la misma tabla. Si el recuento de transacciones dependientes supera el máximo permitido se producirá un error en todas las transacciones dependientes.

En SQL Server 2016:

- El máximo permitido es de 8 transacciones dependientes. 8 es también el límite de transacciones que del que puede depender cualquier transacción determinada.
- El número de error es 41839. (En SQL Server 2014 el número de error es 41301).


Puede hacer que sus scripts de Transact-SQL sean más sólidos frente a un posible error de transacción agregando *lógica de reintento* a sus scripts. Probablemente, la lógica de reintento le ayudará cuando las llamadas a UPDATE y DELETE sean frecuentes, o si se hace referencia a la tabla con optimización para memoria mediante una clave externa de otra tabla. Para obtener detalles, consulte:

- [Transacciones con tablas con optimización para memoria](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)
- [Límites de dependencia de transacciones en tablas con optimización para memoria: error 41839](https://blogs.msdn.microsoft.com/sqlcat/2016/07/11/transaction-dependency-limits-with-memory-optimized-tables-error-41839/)



## <a name="related-links"></a>Vínculos relacionados

- [OLTP en memoria (optimización en memoria)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)



