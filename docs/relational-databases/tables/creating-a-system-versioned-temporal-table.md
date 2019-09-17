---
title: Creación de una tabla temporal con control de versiones del sistema | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 21e6d74f-711f-40e6-a8b7-85f832c5d4b3
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 679260f7c8a7f50eb9a3f638f3547c82ac488cef
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238748"
---
# <a name="creating-a-system-versioned-temporal-table"></a>Creación de una tabla temporal con control de versiones del sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Existen tres maneras de crear una tabla temporal con control de versiones del sistema, según la forma en la que se especifica la tabla de historial:  
  
-   Tabla temporal con una tabla de historial anónima: especifique el esquema de la tabla actual y deje que el sistema cree una tabla de historial correspondiente con el nombre generado automáticamente.  
  
-   Tabla temporal con una tabla de historial predeterminada: especifique el nombre del esquema de tabla de historial y el nombre de tabla, y deje que el sistema cree una tabla de historial en ese esquema.  
  
-   Tabla temporal con una tabla de historial definida por el usuario y creada con antelación: cree una tabla de historial que se mejor adapte a sus necesidades y, después, haga referencia a ella durante la creación de la tabla temporal.  
  
## <a name="creating-a-temporal-table-with-an-anonymous-history-table"></a>Creación de una tabla temporal con una tabla de historial anónima  
 Esta opción resulta práctica para la generación rápida de objetos, especialmente en entornos de prueba y prototipos. También constituye la manera más sencilla de crear una tabla temporal, ya que no requiere ningún parámetro en la cláusula **SYSTEM_VERSIONING**. En el ejemplo siguiente, se crea una nueva tabla con el control de versiones del sistema habilitado sin definir el nombre de la tabla de historial.  
  
```  
CREATE TABLE Department   
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED  
  , DeptName VARCHAR(50) NOT NULL  
  , ManagerID INT NULL  
  , ParentDeptID INT NULL  
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL  
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL  
  , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)     
)    
WITH (SYSTEM_VERSIONING = ON);
```
  
### <a name="important-remarks"></a>Notas importantes  
  
-   Una tabla temporal con versiones del sistema debe tener definida una clave principal y tener especificado exactamente un parámetro **PERIOD FOR SYSTEM_TIME** con dos columnas datetime2, declaradas como **GENERATED ALWAYS AS ROW START / END**.  
  
-   Siempre se supone que las columnas **PERIOD** no aceptan valores NULL, aunque no se especifique la nulabilidad. Si se define explícitamente que las columnas  **PERIOD** aceptan valores NULL, la instrucción **CREATE TABLE** generará un error.  
  
-   La tabla de historial siempre debe tener el mismo esquema que la tabla temporal o actual, en lo concerniente a número y nombres de columnas, orden, y tipos de datos.  
  
-   Se crea automáticamente una tabla de historial anónima en el mismo esquema que la tabla temporal o actual.  
  
-   El nombre de la tabla de historial anónima tiene el formato siguiente: *MSSQL_TemporalHistoryFor_<id._objeto_tabla_temporal_actual>_[sufijo]* . El sufijo es opcional y se agregará únicamente si la primera parte del nombre de la tabla no es único.  
  
-   La tabla de historial se crea como una tabla de almacén de filas. Si es posible, se aplicará la compresión de página; en caso lo contrario, la tabla de historial estará descomprimida. Por ejemplo, algunas configuraciones de tabla, como las columnas dispersas, no permiten la compresión.  
  
-   Se crea un índice agrupado predeterminado para la tabla de historial con un nombre generado automáticamente en formato *IX_<nombre_de_tabla_de_historial>* . El índice agrupado contiene las columnas **PERIOD** (finalización, inicio).  
  
-   Para crear la tabla actual como una tabla optimizada para memoria, vea [Tablas temporales con control de versiones del sistema con tablas optimizadas para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md).  
  
## <a name="creating-a-temporal-table-with-a-default-history-table"></a>Creación de una tabla temporal con una tabla de historial predeterminada  
 Esta opción es práctica en casos en los que quiera controlar la nomenclatura y, aun así, delegar en el sistema la generación de la tabla de historial con la configuración predeterminada. En el ejemplo siguiente, se crea una nueva tabla con el control de versiones del sistema habilitado y el nombre de la tabla de historial definido explícitamente.  
  
```
CREATE TABLE Department   
(
    DeptID INT NOT NULL PRIMARY KEY CLUSTERED
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL
  , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime)
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```  
  
### <a name="important-remarks"></a>Notas importantes  
 La tabla de historial se crea con las mismas reglas que se aplican a la generación de una tabla de historial "anónima", pero con las siguientes variaciones específicas de esta modalidad.  
  
-   El nombre de esquema es obligatorio para el parámetro **HISTORY_TABLE** .  
  
-   Si el esquema especificado no existe, la instrucción **CREATE TABLE** generará un error.  
  
-   Si la tabla que especifica el parámetro **HISTORY_TABLE** ya existe, se validará con la tabla temporal recién creada en lo que respecta a la [coherencia del esquema y de los datos temporales](https://msdn.microsoft.com/library/dn935015.aspx). Si especifica una tabla de historial no válida, la instrucción **CREATE TABLE** generará un error.  
  
## <a name="creating-a-temporal-table-with-a-user-defined-history-table"></a>Creación de una tabla temporal con una tabla de historial definida por el usuario  
 Esta modalidad resulta práctica en casos en los que el usuario quiere especificar una tabla de historial con opciones de almacenamiento específicas e índices adicionales. En el ejemplo siguiente, se crea una tabla de historial definida por el usuario con un esquema acorde con el de la tabla temporal que va a generar. Para esta tabla de historial definida por el usuario, se crea un índice de almacén de columnas agrupado y un índice de almacén de filas (árbol B) no agrupado adicional orientados a las búsquedas puntuales. Después de crear esta tabla de historial definida por el usuario, se genera la tabla temporal con control de versiones del sistema, en la que se especifica la tabla de historial definida por el usuario como la predeterminada.  
  
```  
CREATE TABLE DepartmentHistory
(
    DeptID INT NOT NULL
  , DeptName VARCHAR(50) NOT NULL
  , ManagerID INT NULL
  , ParentDeptID INT NULL
  , SysStartTime DATETIME2 NOT NULL
  , SysEndTime DATETIME2 NOT NULL
);
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_DepartmentHistory
    ON DepartmentHistory;
CREATE NONCLUSTERED INDEX IX_DepartmentHistory_ID_PERIOD_COLUMNS
    ON DepartmentHistory (SysEndTime, SysStartTime, DeptID);
GO

CREATE TABLE Department   
(
    DeptID int NOT NULL PRIMARY KEY CLUSTERED  
  , DeptName VARCHAR(50) NOT NULL  
  , ManagerID INT NULL  
  , ParentDeptID INT NULL  
  , SysStartTime DATETIME2 GENERATED ALWAYS AS ROW START NOT NULL  
  , SysEndTime DATETIME2 GENERATED ALWAYS AS ROW END NOT NULL     
  , PERIOD FOR SYSTEM_TIME (SysStartTime,SysEndTime)      
)
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DepartmentHistory));
```
  
### <a name="important-remarks"></a>Notas importantes  
  
-   Si planea ejecutar consultas analíticas en datos históricos que emplean agregados o funciones basadas en ventanas, se recomienda encarecidamente crear un almacén de columnas agrupado como índice principal para la compresión y el rendimiento de las consultas.  
  
-   Si el caso de uso principal es la auditoría de datos (es decir, buscar cambios históricos de una única fila de la tabla actual), se aconseja crear una tabla de historial del almacén de filas con un índice agrupado.  
  
-   La tabla de historial no puede tener una clave principal, claves externas, índices únicos, restricciones de tabla ni desencadenadores. No puede configurarse para la captura de datos de cambios, el seguimiento de cambios, transaccional, el seguimiento de cambios ni la replicación transaccional o de mezcla.  
  
## <a name="alter-non-temporal-table-to-be-system-versioned-temporal-table"></a>Modificación de una tabla no temporal para convertirla en la tabla temporal con control de versiones del sistema  
 Si tiene que habilitar el control de versiones del sistema con una tabla existente, como cuando quiera migrar una solución temporal personalizada a la compatibilidad integrada.   
Por ejemplo, es posible que cuente con un conjunto de tablas en las que el control de versiones está implementado con desencadenadores. El uso del control de versiones del sistema temporal es más simple y ofrece ventajas adicionales, como las siguientes:  
  
-   Historial invariable  
  
-   Nueva sintaxis para las consultas a versiones anteriores  
  
-   Mejor rendimiento de DML  
  
-   Costos de mantenimiento mínimos  
  
 A la hora de convertir una tabla existente, plantéese usar la cláusula **HIDDEN** para ocultar las nuevas columnas **PERIOD** (las columnas datetime2 **SysStartTime** y **SysEndTime**) y, así, evitar repercutir en las aplicaciones existentes que no estén diseñadas para procesarlas.  

### <a name="adding-versioning-to-non-temporal-tables"></a>Adición del control de versiones a tablas no temporales  
 Si quiere iniciar el seguimiento de cambios de una tabla no temporal que contenga datos, debe agregar la definición **PERIOD** y, opcionalmente, especificar un nombre para la tabla de historial vacía que SQL Server creará automáticamente:  
  
```  
CREATE SCHEMA History;   
GO

ALTER TABLE InsurancePolicy
    ADD   
        SysStartTime DATETIME2(0) GENERATED ALWAYS AS ROW START HIDDEN
            CONSTRAINT DF_SysStart DEFAULT SYSUTCDATETIME()
      , SysEndTime DATETIME2(0) GENERATED ALWAYS AS ROW END HIDDEN
            CONSTRAINT DF_SysEnd DEFAULT CONVERT(DATETIME2 (0), '9999-12-31 23:59:59'),
        PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);
GO

ALTER TABLE InsurancePolicy   
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = History.InsurancePolicy));
```  
  
#### <a name="important-remarks"></a>Notas importantes  
  
-   La acción de agregar columnas que no admiten valores NULL con valores predeterminados en una tabla existente con datos es una operación de tamaño de datos en todas las ediciones, excepto SQL Server Enterprise Edition (donde constituye una operación de metadatos). Si cuenta con una gran tabla de historial existente con datos en SQL Server Standard Edition, la adición de una columna que no acepte valores NULL puede constituir una operación costosa.  
  
-   Las restricciones de las columnas de inicio y finalización del periodo se deben elegir con cautela:  
  
    -   El valor predeterminado de la columna de inicio especifica desde qué momento concreto considera que las filas existentes son válidas. No se puede especificar como un punto datetime en el futuro.  
  
    -   La hora de finalización se debe especificar como el valor máximo para una precisión de datetime2 determinada.  
  
-   Si se agrega un período, se realizará una comprobación de coherencia de datos en la tabla actual para garantizar la validez de los valores predeterminados de las columnas de período.  
  
-   Cuando se especifica una tabla de historial existente al habilitar **SYSTEM_VERSIONING**, se realizará una comprobación de coherencia de datos en la tabla actual y en la de historial. Puede omitirse si se especifica **DATA_CONSISTENCY_CHECK = OFF** como parámetro adicional.  
  
### <a name="migrate-existing-tables-to-built-in-support"></a>Migración de tablas existentes a la compatibilidad integrada  
 En este ejemplo se muestra cómo migrar una solución existente basada en desencadenadores a una compatibilidad temporal integrada. En este ejemplo, se supone que la solución personalizada actual divide los datos actuales e históricos en dos tablas de usuario independientes (**ProjectTaskCurrent** y **ProjectTaskHistory**). Si su solución existente usa una sola tabla para almacenar las filas reales e históricas, debe dividir los datos en dos tablas antes de realizar los pasos de migración descritos en este ejemplo:  
  
```  
/*Drop trigger on future temporal table*/   
DROP TRIGGER ProjectCurrent_OnUpdateDelete;   
/*Make sure that future period columns are non-nullable*/   
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidFrom] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskCurrent ALTER COLUMN [ValidTo] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidFrom] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskHistory ALTER COLUMN [ValidTo] datetime2 NOT NULL;   
ALTER TABLE ProjectTaskCurrent   
    ADD PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])   
ALTER TABLE ProjectTaskCurrent   
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProjectTaskHistory, DATA_CONSISTENCY_CHECK = ON));
```  
  
#### <a name="important-remarks"></a>Notas importantes  
  
-   Si se hace referencia a columnas existentes en la definición **PERIOD** , se cambiará de forma implícita generated_always_type a **AS_ROW_START** y **AS_ROW_END** para dichas columnas.  
  
-   Al agregar **PERIOD** , se efectuará una comprobación de coherencia de datos en la tabla actual para garantizar la validez de los valores existentes en las columnas de período.  
  
-   Se recomienda encarecidamente establecer **SYSTEM_VERSIONING** con **DATA_CONSISTENCY_CHECK = ON** para aplicar comprobaciones de coherencia de datos en los datos existentes.  

-   Si se prefieren las columnas ocultas, use el comando `ALTER TABLE [tableName] ALTER COLUMN [columnName] ADD HIDDEN;`.
  
 
## <a name="see-also"></a>Consulte también  
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)   
 [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Administración de la retención de datos históricos en las tablas temporales con versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [Modificación de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [Consulta de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Cambiar el esquema de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Detención del control de versiones en una tabla temporal con control de versiones](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
