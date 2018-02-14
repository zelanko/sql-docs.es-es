---
title: "Compilación nativa de tablas y procedimientos almacenados | Microsoft Docs"
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f9cbe1802a5a4a353ad4af72abcb092187aa8e0a
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>Compilación nativa de tablas y procedimientos almacenados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
OLTP en memoria introduce el concepto de compilación nativa. 
            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede compilar de forma nativa procedimientos almacenados que acceden a tablas optimizadas para memoria. 
            [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también puede compilar de forma nativa las tablas optimizadas para memoria. La compilación nativa permite un acceso más rápido a los datos y una ejecución de consultas más eficiente que el lenguaje [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado (tradicional). La compilación nativa de tablas y procedimientos almacenados produce los archivos DLL.

Se admite también la compilación nativa de los tipos de tabla con optimización para memoria. Para obtener más información, vea [Faster temp table and table variable by using memory optimization (Tabla temporal y variable de tabla más rápidas con optimización de memoria)](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md).

La compilación nativa se refiere al proceso de convertir construcciones de programación a código nativo, que consta de instrucciones de procesador sin necesidad de compilación o interpretación adicional.

OLTP en memoria compila las tablas optimizadas para memoria cuando se crean, y los procedimientos almacenados compilados de forma nativa cuando se cargan en archivos DLL nativos. Además, los archivos DLL se recompilan tras reiniciar una base de datos o un servidor. La información necesaria para volver a crear los archivos DLL se almacena en los metadatos de la base de datos. Los archivos DLL no forman parte de la base de datos, aunque están asociados a la base de datos. Por ejemplo, los archivos DLL no se incluyen en las copias de seguridad de bases de datos.

> [!NOTE]
> Las tablas con optimización para memoria se vuelven a compilar durante un reinicio del servidor. Para acelerar la recuperación de bases de datos, los procedimientos almacenados compilados de forma nativa no se vuelven a compilar durante un reinicio del servidor, sino que se compilan en el momento de la primera ejecución. Como consecuencia de esta compilación diferida, los procedimientos almacenados compilados de forma nativa solo aparecen al llamar a [sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql.md) tras la primera ejecución.

## <a name="maintenance-of-in-memory-oltp-dlls"></a>Mantenimiento de los archivos DLL de OLTP en memoria

La consulta siguiente muestra todos los archivos DLL de tablas y procedimientos almacenados cargados actualmente en la memoria del servidor:

```sql
SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.description = 'XTP Native DLL';
```

Los administradores de bases de datos no necesitan mantener los archivos generados por una compilación nativa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quita automáticamente los archivos generados que ya no son necesarios. Por ejemplo, los archivos generados se eliminarán cuando se elimine una tabla o un procedimiento almacenado, o si se quita una base de datos.

> [!NOTE]
> Si la compilación produce un error o se interrumpe, algunos archivos generados no se eliminan. Estos archivos se dejan intencionadamente por motivos de compatibilidad y se quitan cuando se quita la base de datos.

> [!NOTE]
> SQL Server compila los archivos DLL para todas las tablas necesarias para la recuperación de la base de datos. Si se quita una tabla justo antes de un reinicio de la base de datos, puede haber residuos de la tabla en los archivos de punto de control o en el registro de transacciones, de modo que puede volver a compilar el archivo DLL de la tabla durante el inicio de la base de datos. Después de reiniciar, el archivo DLL se descargará y se quitarán los archivos con el proceso de limpieza normal.

## <a name="native-compilation-of-tables"></a>Compilación nativa de tablas

Al crear una tabla optimizada para memoria mediante la instrucción **CREATE TABLE** , la información de la tabla se escribe en los metadatos de la base de datos y se crean las estructuras de tabla y de índice en la memoria. Además, la tabla se compila en un archivo DLL.

Considere el script de ejemplo siguiente, que crea una base de datos y una tabla optimizada para memoria:

```sql
USE master;
GO

CREATE DATABASE DbMemopt3;
GO

ALTER DATABASE DbMemopt3
    add filegroup DbMemopt3_mod_memopt_1_fg
        contains memory_optimized_data
;
GO

-- You must edit the front portion of filename= path, to where your DATA\ subdirectory is,
-- keeping only the trailing portion '\DATA\DbMemopt3_mod_memopt_1_fn'!

ALTER DATABASE DbMemopt3
    add file
    (
        name     = 'DbMemopt3_mod_memopt_1_name',
        filename = 'C:\DATA\DbMemopt3_mod_memopt_1_fn'

        --filename = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\DbMemopt3_mod_memopt_1_fn'
    )
        to filegroup DbMemopt3_mod_memopt_1_fg
;
GO

USE DbMemopt3;
GO

CREATE TABLE dbo.t1
(
    c1 int not null primary key nonclustered,
    c2 int
)
    with (memory_optimized = on)
;
GO



-- You can safely rerun from here to the end.

-- Retrieve the path of the DLL for table t1.


DECLARE @moduleName  nvarchar(256);

SET @moduleName =
    (
        '%xtp_t_' +
        cast(db_id() as nvarchar(16)) +
        '_' +
        cast(object_id('dbo.t1') as nvarchar(16)) +
        '%.dll'
    )
;


-- SEARCHED FOR NAME EXAMPLE:  mod1.name LIKE '%xtp_t_8_565577053%.dll'
PRINT @moduleName;


SELECT
        mod1.name,
        mod1.description
    from
        sys.dm_os_loaded_modules  as mod1
    where
        mod1.name LIKE @moduleName
    order by
        mod1.name
;
-- ACTUAL NAME EXAMPLE:  mod1.name = 'C:\Program Files\Microsoft SQL Server\MSSQL13.SQLSVR2016ID\MSSQL\DATA\xtp\8\xtp_t_8_565577053_184009305855461.dll'
GO

--   DROP DATABASE DbMemopt3;  -- Clean up.
GO
```

Al crear la tabla, también se crea el archivo DLL de la tabla y se carga en memoria. La consulta DMV que aparece inmediatamente después de la instrucción CREATE TABLE recupera la ruta de acceso del archivo DLL de la tabla.

El archivo DLL de la tabla entiende las estructuras de índice y el formato de fila de la tabla. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el archivo DLL para recorrer índices, recuperar filas y almacenar el contenido de estas.

## <a name="native-compilation-of-stored-procedures"></a>Compilación nativa de procedimientos almacenados

Los procedimientos almacenados marcados con NATIVE_COMPILATION se compilan de forma nativa. Esto significa que todas las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] del procedimiento se compilan en código nativo para lograr una ejecución eficaz de la lógica de negocios de rendimiento crítico.

Para obtener más información acerca de los procedimientos almacenados compilados de forma nativa, vea [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).

Considere el procedimiento almacenado de ejemplo siguiente, que inserta filas en la tabla t1 del ejemplo anterior:

```sql
CREATE PROCEDURE dbo.native_sp
    with native_compilation,
         schemabinding,
         execute as owner
as
begin atomic
    with (transaction isolation level = snapshot,
          language = N'us_english')

    DECLARE @i int = 1000000;

    WHILE @i > 0
    begin
        INSERT dbo.t1 values (@i, @i+1);
        SET @i -= 1;
    end
end;
GO

EXECUTE dbo.native_sp;
GO

-- Reset.

DELETE from dbo.t1;
GO
```

El archivo DLL de native_sp puede interactuar directamente con el archivo DLL de t1, así como con el motor de almacenamiento de OLTP en memoria, para insertar las filas a la mayor velocidad posible.

El compilador de OLTP en memoria utiliza el optimizador de consultas para crear un plan de ejecución eficaz para cada una de las consultas del procedimiento almacenado. Tenga en cuenta que los procedimientos almacenados compilados de forma nativa no se recompilan automáticamente si cambian los datos de la tabla. Para obtener más información sobre el mantenimiento de estadísticas y procedimientos almacenados con OLTP en memoria, vea [Estadísticas para las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/statistics-for-memory-optimized-tables.md).

## <a name="security-considerations-for-native-compilation"></a>Consideraciones de seguridad para la compilación nativa

La compilación nativa de tablas y procedimientos almacenados utiliza el compilador de OLTP en memoria. Este compilador genera archivos que se escriben en el disco y se cargan en la memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza los siguientes mecanismos para restringir el acceso a estos archivos.

### <a name="native-compiler"></a>Compilador nativo

El archivo ejecutable del compilador, así como los archivos binarios y de encabezado necesarios para la compilación nativa, se instalan como parte de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la carpeta MSSQL\Binn\Xtp. Así, si la instancia predeterminada se instala en C:\Archivos de programa, los archivos del compilador se instalan en C:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\Binn\Xtp.

Para limitar el acceso al compilador, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza listas de control de acceso (ACL) para restringir el acceso a los archivos binarios. Todos los archivos binarios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están protegidos frente a su modificación o alteración mediante ACL. Las ACL del compilador nativo también limitan el uso del compilador; solo la cuenta de servicio y los administradores del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tienen permisos de ejecución y de lectura para los archivos del compilador nativo.

### <a name="files-generated-by-a-native-compilation"></a>Archivos generados por una compilación nativa

Entre los archivos que se generan cuando se compila una tabla o un procedimiento almacenado se incluyen los archivos intermedios y DLL, incluidos aquellos que tienen las extensiones siguientes: .c, .obj, .xml y .pdb. Los archivos generados se guardan en una subcarpeta de la carpeta de datos predeterminada. La subcarpeta se denomina Xtp. Al instalar la instancia predeterminada con la carpeta de datos predeterminada, los archivos generados se colocan en C:\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL13.MSSQLSERVER\MSSQL\DATA\Xtp.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] evita la alteración con las DLL generadas de tres maneras:

- Cuando una tabla o un procedimiento almacenado se compila en un archivo DLL, este archivo se carga en memoria y se vincula al proceso sqlserver.exe inmediatamente. Un archivo DLL no se puede modificar mientras esté vinculado a un proceso.

- Cuando se reinicia una base de datos, se recompilan todas las tablas y los procedimientos almacenados (se quitan y se vuelven a crear) según los metadatos de la base de datos. De este modo, se quitará cualquier cambio realizado en un archivo generado por un agente malintencionado.

- Los archivos generados se consideran parte de los datos de usuario y tienen las mismas restricciones de seguridad, mediante ACL, que los archivos de base de datos: solo los administradores del sistema y la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden tener acceso a estos archivos.

No se necesita ninguna interacción del usuario para administrar estos archivos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creará y quitará los archivos según sea necesario.

## <a name="see-also"></a>Ver también

[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)

[Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)
