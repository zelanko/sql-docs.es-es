---
title: "Administraci&#243;n de la retenci&#243;n de datos hist&#243;ricos en las tablas temporales con versiones del sistema | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7925ebef-cdb1-4cfe-b660-a8604b9d2153
caps.latest.revision: 23
author: "CarlRabeler"
ms.author: "carlrab"
manager: "jhubbard"
caps.handback.revision: 23
---
# Administraci&#243;n de la retenci&#243;n de datos hist&#243;ricos en las tablas temporales con versiones del sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Con las tablas temporales con versiones del sistema, la tabla de historial puede aumentar el tamaño de la base de datos más que las tablas normales, especialmente en las siguientes condiciones:  
  
-   Retención de datos históricos durante un largo período  
  
-   Disponibilidad de una actualización o eliminación del modelo de modificación de gran cantidad de datos  
  
 Una tabla de historial de gran tamaño y creciente puede ser un problema debido a los costos de almacenamiento puro y a la imposición de un impuesto de rendimiento sobre las consultas temporales. Por lo tanto, al desarrollar una directiva de retención de datos para administrar datos en la tabla de historial es un aspecto importante de la planeación y la administración del ciclo de vida de cada tabla temporal.  
  
## Administración de la retención de datos para la tabla de historial  
 La administración de la retención de datos de la tabla temporal empieza por determinar el período de retención requerido para cada tabla temporal. La directiva de retención, en la mayoría de los casos, debe considerarse parte de la lógica de negocios de la aplicación mediante las tablas temporales. Por ejemplo, las aplicaciones de datos de auditoría y escenarios de viaje en el tiempo tienen requisitos firmes en términos de cuánto tiempo deben estar disponibles los datos históricos para la consulta en línea.  
  
 Una vez que determine el período de retención de datos, el siguiente paso es desarrollar un plan para administrar los datos históricos, cómo y dónde almacenar los datos históricos y cómo eliminar los datos históricos que son anteriores a los requisitos de retención. Con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], tiene los tres enfoques siguientes para administrar los datos históricos en la tabla de historial temporal:  
  
-   [Stretch Database](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_1)  
  
-   [Partición de tabla](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)  
  
-   [Script de limpieza personalizado](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)  
  
 Con cada uno de estos enfoques, la lógica para la migración o limpieza de datos del historial se basa en la columna que se corresponde con el final del período en la tabla actual. El final del valor del período para cada fila determina el momento en el que la versión de fila se "cierra", es decir, cuando llega a la tabla de historial. Por ejemplo, la condición `SysEndTime < DATEADD (DAYS, -30, SYSUTCDATETIME ())` especifica que esos datos históricos anteriores a un mes tienen quitarse o extraerse de la tabla de historial.  
  
> **NOTA:** Los ejemplos de este tema usan este [ejemplo de tabla temporal](https://msdn.microsoft.com/library/mt590957.aspx).  
  
## Uso del enfoque de Stretch Database  
  
> **NOTA:** El uso del enfoque de Stretch Database solo se aplica a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y no se aplica a [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md) en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] migra los datos históricos de forma transparente a Azure. Para obtener seguridad adicional, puede cifrar los datos en movimiento con la característica [Always Encrypted](https://msdnstage.redmond.corp.microsoft.com/library/mt163865.aspx) de SQL Server. Además, puede usar [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md) y otras características de seguridad avanzadas de SQL Server con Temporal y Stretch Database para proteger los datos.  
  
 Con el enfoque de Stretch Database, puede ajustar algunas o todas las tablas de historial temporales en Azure y SQL Server moverá de forma silenciosa los datos históricos a Azure. La habilitación del ajuste de una tabla de historial no cambia la forma en la que interactúa con la tabla temporal en términos de modificación de datos y consultas temporales.  
  
-   **Ajuste de la tabla de historial completa:** configure Stretch Database para la tabla de historial completa si el escenario principal es la auditoría de datos en un entorno con cambios frecuentes de datos y una consulta relativamente poco frecuente sobre los datos históricos.  En otras palabras, puede utilizar este enfoque si el rendimiento de las consultas temporales no es importante. En este caso, la rentabilidad proporcionada por Azure puede resultar atractiva.   
    Cuando ajuste la tabla de historial completa, puede usar el Asistente de Stretch o Transact-SQL. A continuación aparecen ejemplos de ambos.  
  
-   **Ajuste de una parte de la tabla de historial:** configure Stretch Database para una sola parte de la tabla de historial para mejorar el rendimiento si su escenario principal implica principalmente consultar datos históricos recientes, pero desea conservar la opción para consultar los datos históricos anteriores cuando sea necesario mientras se almacenan esos datos de forma remota a un menor costo. Con Transact-SQL, puede hacerlo si especifica una función de predicado para seleccionar las filas que se va a migrar de la tabla de historial en lugar de migrar todas las filas.  Cuando se trabaja con las tablas temporales, normalmente tiene sentido mover los datos en función de la condición de tiempo (es decir, según la edad de la versión de fila en la tabla de historial).    
    Utilice una función de predicado determinista para mantener una parte del historial en la misma base de datos con los datos actuales, mientras el resto se migra a Azure.    
    Para ver ejemplos y limitaciones, consulte [Selección de las filas que se van a migrar mediante una función de filtro (Stretch Database)](https://msdn.microsoft.com/library/mt613432.aspx). Puesto que las funciones no determinista no son válidas, si desea transferir datos de historial al estilo de ventana deslizante, necesitaría alterar regularmente la definición de las funciones de predicado en línea de manera que la ventana de filas que mantenga localmente sea constante en términos de edad. La ventana deslizante le permite mover constantemente datos históricos con una antigüedad superior a un mes a Azure. A continuación, aparece un ejemplo de este enfoque.  
  
> **NOTA:** Stretch Database migra los datos a Azure. Por lo tanto, necesita una cuenta de Azure y una suscripción para la facturación. Para obtener una cuenta de Azure de evaluación gratuita, haga clic en [Evaluación gratuita de un mes](https://azure.microsoft.com/pricing/free-trial/).  
  
 Puede configurar una tabla de historial temporal para Stretch con el Asistente de Stretch o Transact-SQL, y puede habilitar el ajuste para una tabla de historial temporal mientras la versión del sistema se establece en **ON**. El ajuste de la tabla actual no está permitido porque no tiene sentido aplicarlo.  
  
### Uso del Asistente de Stretch para ajustar la tabla de historial completo  
 El método más sencillo para los principiantes es usar el Asistente de Stretch para habilitar el ajuste para la base de datos completa y, después, seleccionar la tabla de historial temporal en el Asistente de Stretch (en este ejemplo se supone que ha configurado la tabla de departamento como una tabla temporal con versiones del sistema en una base de datos vacía). En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], no puede hacer clic con el botón derecho en la propia tabla de historial temporal y hacer clic en Stretch.  
  
1.  Haga clic con el botón derecho en la base de datos y seleccione **Tareas**, seleccione **Stretch** y, después, haga clic en **Habilitar** para iniciar el asistente.  
  
2.  En la ventana **Seleccionar tablas**, seleccione la casilla de la tabla de historial temporal y haga clic en Siguiente.  
  
     ![Selecting the history table on the Select tables page](../../relational-databases/tables/media/stretch-wizard-2-for-temporal.png "Selecting the history table on the Select tables page")  
  
3.  En la ventana **Configuración de Azure**, proporcione las credenciales de inicio de sesión. Inicie sesión en Microsoft Azure o regístrese para obtener una cuenta. Seleccione la suscripción que va a usar y la región de Azure. Después, cree un nuevo servidor o seleccione un servidor existente. Haga clic en **Siguiente**.  
  
     ![Create new Azure server - Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-4.png "Create new Azure server - Stretch Database wizard")  
  
4.  En la ventana **Credenciales de seguridad**, proporcione una contraseña para la clave maestra de base de datos para proteger sus credenciales de base de datos de SQL Server de origen y haga clic en Siguiente.  
  
     ![Secure credentials page of the Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-6.png "Secure credentials page of the Stretch Database wizard")  
  
5.  En la ventana **Seleccionar dirección IP**, proporcione el intervalo de direcciones IP para SQL Server para que el servidor de Azure se comunique con SQL Server (si selecciona un servidor existente para el ya existe una regla de firewall, simplemente haga clic en Siguiente aquí para usar la regla de firewall existente). Haga clic en **Siguiente** y, después, en **Finalizar** para habilitar Stretch Database y ajustar la tabla de historial temporal.  
  
     ![Select IP address page of the Stretch Database wizard](../../relational-databases/tables/media/stretch-wizard-7.png "Select IP address page of the Stretch Database wizard")  
  
6.  Cuando se complete el asistente, compruebe que se haya habilitado el ajuste correctamente para la base de datos. Vea los iconos del Explorador de objetos que indican que se ha ajustado la base de datos.  
  
> **NOTA:** Si se produce un error en Habilitar base de datos para Stretch, revise el registro de errores. Un error común consiste en configurar incorrectamente la regla de firewall.  
  
 Vea también:  
  
-   [Habilitación de Stretch Database para una base de datos](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)  
  
-   [Introducción mediante la ejecución del Asistente para Habilitar base de datos para Stretch](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)  
  
-   [Habilitar Stretch Database para una tabla](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md)  
  
### Uso de Transact-SQL para ajustar la tabla de historial completo  
 También puede usar Transact-SQL para habilitar Stretch en el servidor local y [Habilitación de Stretch Database para una base de datos](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md). Después, puede [usar Transact-SQL para habilitar Stretch Database en una tabla](https://msdn.microsoft.com/library/mt605115.aspx#Anchor_1). Con una base de datos habilitada previamente para Stretch Database, ejecute el siguiente script de Transact-SQL para ajustar una tabla de historial temporal con versiones del sistema existente:  
  
```  
ALTER TABLE <history table name>   
SET (REMOTE_DATA_ARCHIVE = ON (MIGRATION_STATE = OUTBOUND));  
```  
  
### Uso de Transact-SQL para ajustar una parte de la tabla de historial  
 Para ajustar solo una parte de la tabla de historial primero debe crear una [función de predicado en línea](https://msdn.microsoft.com/library/mt613432.aspx). En este ejemplo, supongamos que ha configurado la función de predicado en línea por primera vez el 1 de diciembre de 2015 y quiere ajustar a Azure todas las fechas de historial anteriores al 1 de noviembre de 2015. Para lograr esto, empiece por crear la siguiente función:  
  
```  
CREATE FUNCTION dbo.fn_StretchBySystemEndTime20151101(@systemEndTime datetime2)   
RETURNS TABLE   
WITH SCHEMABINDING    
AS    
RETURN SELECT 1 AS is_eligible   
  WHERE @systemEndTime < CONVERT(datetime2, '2015-11-01T00:00:00', 101) ;  
```  
  
 a continuación, use el siguiente script para agregar el predicado de filtro a la tabla de historial y establecer el estado de la migración en OUTBOUND para permitir la migración de datos basado en predicado para la tabla de historial.  
  
```  
ALTER TABLE <history table name>   
SET (   
        REMOTE_DATA_ARCHIVE = ON   
                (   
                        FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20151101 (SysEndTime)  
                                , MIGRATION_STATE = OUTBOUND   
                )  
        )   
;  
```  
  
 Para mantener una ventana deslizante, necesita que la función de predicado sea precisa cada día (es decir, cambiar la condición de fila de filtrado cada día en un día). El siguiente script es el script que necesitaría ejecutar el 2 de diciembre de 2015:  
  
```  
BEGIN TRAN  
           /*(1) Create new predicate function definition */  
        CREATE FUNCTION dbo.fn_StretchBySystemEndTime20151102(@systemEndTime datetime2)  
        RETURNS TABLE  
        WITH SCHEMABINDING   
        AS   
        RETURN SELECT 1 AS is_eligible  
               WHERE @systemEndTime < CONVERT(datetime2,'2015-11-02T00:00:00', 101)  
        GO  
  
        /*(2) Set the new function as filter predicate */  
        ALTER TABLE <history table name>  
        SET   
        (  
               REMOTE_DATA_ARCHIVE = ON  
               (  
                       FILTER_PREDICATE = dbo.fn_StretchBySystemEndTime20151102(SysEndTime),  
                       MIGRATION_STATE = OUTBOUND  
               )  
        )   
COMMIT ;  
```  
  
 utilice el Agente SQL Server o algún otro mecanismo de programación para asegurarse de que la definición de la función de predicado es válida todo el tiempo.  
  
## Uso del enfoque de la partición de tabla  
 La[partición de tabla](https://msdn.microsoft.com/library/ms188730.aspx) puede hacer que las tablas grandes sean más escalables y fáciles de administrar. Con el enfoque de partición de tabla, puede usar particiones de tabla de historial para implementar la limpieza de datos personalizada o el archivado sin conexión según una condición de tiempo. La partición de tabla también le proporcionará ventajas de rendimiento cuando se realicen consultas de tablas temporales en un subconjunto de historial de datos mediante la eliminación de una partición.  
  
 Con la partición de tabla, puede implementar un enfoque de ventana deslizante para extraer la parte más antigua de los datos históricos de la tabla de historial y mantener el tamaño de la parte retenida constante en términos de edad: manteniendo los datos en la tabla de historial igual que en el período de retención requerido. Se admite la operación de conmutación de datos fuera de la tabla de historial cuando SYSTEM_VERSIONING está activado, lo que significa que puede limpiar una parte de los datos del historial sin introducir una ventana de mantenimiento o bloquear las cargas de trabajo normales.  
  
> **NOTA:** Para realizar la conmutación de particiones, el índice agrupado en la tabla de historial debe alinearse con el esquema de partición (debe contener SysEndTime). La tabla de historial predeterminada creada por el sistema contiene un índice agrupado que incluye las columnas SysEndTime y SysStartTime, que es óptimo para la creación de particiones, la inserción de nuevos datos de historial y la típica consulta temporal. Para obtener más información, consulte [Temporal Tables](../../relational-databases/tables/temporal-tables.md).  
  
 Un enfoque de ventana deslizante tiene dos conjuntos de tareas que tiene que realizar:  
  
-   Una tarea de configuración de partición  
  
-   Tareas periódicas de mantenimiento de partición  
  
 En la ilustración, supongamos que deseamos mantener datos históricos durante 6 meses y queremos mantener todos los meses de datos en una partición independiente. Además, supongamos que hemos activado la versión del sistema en septiembre de 2015.  
  
 Una tarea de configuración de particiones crea la configuración inicial de partición de la tabla de historial. En este ejemplo, crearíamos las mismas particiones de número que el tamaño de la ventana deslizante, en meses, más una partición vacía adicional preparada previamente (se explica a continuación). Esta configuración garantiza que el sistema podrá almacenar correctamente los datos nuevos cuando iniciemos la tarea de mantenimiento periódico de la partición la primera vez y garantiza que nunca dividiremos las particiones con datos para evitar movimientos de datos valiosos. Debe realizar esta tarea mediante Transact-SQL con el siguiente script de ejemplo.  
  
 En la siguiente imagen se muestra la configuración inicial de la creación de particiones para mantener 6 meses de datos.  
  
 ![Partitioning](../../relational-databases/tables/media/partitioning.png "Partitioning")  
  
> **NOTA:** Consulte las consideraciones de rendimiento con las particiones de tabla siguientes para las implicaciones de rendimiento de uso de la opción RANGE LEFT frente a la opción RANGE RIGHT al configurar la creación de particiones.  
  
 Tenga en cuenta que la primera y última partición están "abiertas" en los límites inferior y superior respectivamente para asegurarse de que cada nueva fila tiene la partición de destino independientemente del valor de la columna de partición.   
A medida que pasa el tiempo, las nuevas filas de la tabla del historial se dirigirán a particiones superiores. Cuando se llene la partición 6ª, se habrá alcanzado el período de retención de destino. Este es el momento en el que se debe iniciar la tarea de mantenimiento periódico de la partición por primera vez (debe programarse para ejecutarse periódicamente; una vez al mes en este ejemplo).  
  
 La imagen siguiente muestra las tareas de mantenimiento periódico de la partición (vea los pasos detallados a continuación).  
  
 ![Partitioning2](../../relational-databases/tables/media/partitioning2.png "Partitioning2")  
  
 Los pasos detallados para las tareas de mantenimiento periódico de la partición son:  
  
1.  SWITCH OUT: permite crear una tabla de almacenamiento provisional y, después, cambiar una partición entre la tabla de historial y la tabla de almacenamiento provisional mediante la instrucción [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) con el argumento SWITCH PARTITION (vea el ejemplo C. "Cambio de particiones entre tablas").  
  
    ```  
    ALTER TABLE <history table> SWITCH PARTITION 1 TO <staging table>  
    ```  
  
     Después del cambio de partición, puede archivar opcionalmente los datos de la tabla de almacenamiento provisional y, a continuación, quitar o truncar la tabla de almacenamiento provisional para que estén listos para la próxima vez que necesite realizar esta tarea de mantenimiento periódico de la partición.  
  
2.  MERGE RANGE: permite combinar la partición 1 vacía con la partición 2 mediante [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md) con la opción MERGE RANGE (vea el ejemplo B). Al quitar el límite inferior con esta función, se combina eficazmente la partición vacía 1 con la partición anterior 2 para formar una nueva partición 1. Las demás particiones también cambian de forma efectiva sus ordinales.  
  
3.  SPLIT RANGE: permite crear una nueva partición 7 vacía mediante [ALTER PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-function-transact-sql.md) con la opción SPLIT RANGE (vea el ejemplo A). Al agregar un nuevo límite superior mediante esta función, crea eficazmente una partición independiente para el próximo mes.  
  
### Uso de Transact-SQL para crear particiones en la tabla de historial  
 Utilice el script de Transact-SQL en la ventana de código siguiente para crear la función de partición y el esquema de partición, y volver a crear el índice agrupado para que la partición se alinee con las particiones o el esquema de partición. En este ejemplo, crearemos un enfoque de ventana deslizante de seis meses con particiones mensuales a partir de septiembre de 2015.  
  
```  
BEGIN TRANSACTION  
  
        /*Create partition function*/  
        CREATE PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime] (datetime2(7))   
                    AS RANGE LEFT FOR VALUES   
                                (N'2015-09-30T23:59:59.999'  
                                , N'2015-10-31T23:59:59.999'  
                                , N'2015-11-30T23:59:59.999'  
                                , N'2015-12-31T23:59:59.999'  
                                , N'2016-01-31T23:59:59.999'  
                                , N'2016-02-29T23:59:59.999')  
  
        /*Create partition scheme*/  
        CREATE PARTITION SCHEME [sch_Partition_DepartmentHistory_By_SysEndTime]   
                        AS PARTITION [fn_Partition_DepartmentHistory_By_SysEndTime]   
                        TO ([PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY], [PRIMARY])  
  
        /*Re-create index to be partition-aligned with the partitioning schema*/  
        CREATE CLUSTERED INDEX [ix_DepartmentHistory] ON [dbo].[DepartmentHistory]  
        (  
                    [SysEndTime] ASC,  
                    [SysStartTime] ASC  
        )  
            WITH   
                        (PAD_INDEX = OFF  
                        , STATISTICS_NORECOMPUTE = OFF  
                        , SORT_IN_TEMPDB = OFF  
                        , DROP_EXISTING = ON  
                        , ONLINE = OFF  
                        , ALLOW_ROW_LOCKS = ON  
                        , ALLOW_PAGE_LOCKS = ON  
                        , DATA_COMPRESSION = PAGE)  
            ON [sch_Partition_DepartmentHistory_By_SysEndTime] ([SysEndTime])  
  
COMMIT TRANSACTION;  
  
```  
  
### Uso de Transact-SQL para mantener particiones en el escenario de ventana deslizante  
 Utilice el script de Transact-SQL en la siguiente ventana de código siguiente para mantener las particiones en el escenario de ventana deslizante. En este ejemplo, se conmutará la partición de septiembre de 2015 con la opción MERGE RANGE y, a continuación, se agregará una nueva partición de marzo de 2016 con la opción SPLIT RANGE.  
  
```  
BEGIN TRANSACTION  
  
         /*(1)  Create staging table */  
         CREATE TABLE [dbo].[staging_DepartmentHistory_September_2015]  
        (  
                 [DeptID] [int] NOT NULL  
                 , [DeptName] [varchar](50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL  
                 , [ManagerID] [int] NULL  
                 ,  [ParentDeptID] [int] NULL  
                 ,  [SysStartTime] [datetime2](7) NOT NULL  
                 ,  [SysEndTime] [datetime2](7) NOT NULL  
         ) ON [PRIMARY]  
         WITH  
         (  
              DATA_COMPRESSION = PAGE  
         )  
  
         /*(2) Create index on the same filegroups as the partition that will be switched out*/  
         CREATE CLUSTERED INDEX [ox_staging_DepartmentHistory_September_2015]    
         ON [dbo].[staging_DepartmentHistory_September_2015]  
         (  
                  [SysEndTime] ASC,  
                  [SysStartTime] ASC  
         )  
      WITH   
          (  
               PAD_INDEX = OFF  
               , SORT_IN_TEMPDB = OFF  
               , DROP_EXISTING = OFF  
               , ONLINE = OFF  
               , ALLOW_ROW_LOCKS = ON  
               , ALLOW_PAGE_LOCKS = ON  
          )   
         ON [PRIMARY]  
  
         /*(3) Create constraints matching the partition that will be switched out*/  
         ALTER TABLE [dbo].[staging_DepartmentHistory_September_2015]  WITH CHECK   
               ADD  CONSTRAINT [chk_staging_DepartmentHistory_September_2015_partition_1]   
                    CHECK  ([SysEndTime]<=N'2015-09-30T23:59:59.999')  
         ALTER TABLE [dbo].[staging_DepartmentHistory_September_2015]   
               CHECK CONSTRAINT [chk_staging_DepartmentHistory_September_2015_partition_1]  
  
         /*(4) Switch partition to staging table*/  
         ALTER TABLE [dbo].[DepartmentHistory]   
         SWITCH PARTITION 1 TO [dbo].[staging_DepartmentHistory_September_2015]   
         WITH (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 MINUTES, ABORT_AFTER_WAIT = NONE))  
  
         /*(5) [Commented out] Optionally archive the data and drop staging table  
         INSERT INTO [ArchiveDB].[dbo].[DepartmentHistory]   
         SELECT * FROM [dbo].[staging_DepartmentHistory_September_2015];  
         DROP TABLE [dbo].[staging_DepartmentHIstory_September_2015];  
         */  
  
         /*(6) merge range to move lower boundary one month ahead*/  
         ALTER PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime]()   
               MERGE RANGE(N'2015-09-30T23:59:59.999')  
  
         /*(7) Create new empty partition for "April and after" by creating new boundary point and specifying NEXT USED file group*/  
         ALTER PARTITION SCHEME [sch_Partition_DepartmentHistory_By_SysEndTime] NEXT USED [PRIMARY]  
         ALTER PARTITION FUNCTION [fn_Partition_DepartmentHistory_By_SysEndTime]() SPLIT RANGE(N'2016-03-31T23:59:59.999')  
  
COMMIT TRANSACTION  
  
```  
  
 Puede modificar ligeramente el script anterior y usarlo en el proceso normal de mantenimiento mensual:  
  
1.  En el paso (1), cree una nueva tabla de almacenamiento provisional para el mes que desee quitar (octubre sería el siguiente en nuestro ejemplo)  
  
2.  En el paso (3), cree la restricción y compruebe que coincide con el mes de datos que quiere quitar: `[SysEndTime]<=N'2015-10-31T23:59:59.999'` para la partición de octubre  
  
3.  En el paso (4), cambie la partición 1 a la tabla de almacenamiento provisional recién creada  
  
4.  En el paso (6), modifique la función de partición mediante la combinación del límite inferior: `MERGE RANGE(N'2015-10-31T23:59:59.999'` después de extraer los datos de octubre  
  
5.  En el paso (7), divida la función de partición mediante la creación del límite superior: `SPLIT RANGE (N'2016-04-30T23:59:59.999'` después de extraer los datos de octubre.  
  
 Sin embargo, la mejor solución sería ejecutar regularmente un script de Transact-SQL genérico que fuese capaz de llevar a cabo la acción apropiada cada mes sin modificar el script. Es posible generalizar el script anterior para que actúe sobre los parámetros proporcionados (límite inferior que debe combinarse y límite nuevo que se creará con la división de particiones). Para evitar la creación de una tabla de almacenamiento provisional cada mes, puede crear una con antelación y volver a usarla cambiando la restricción de comprobación para que coincida con la partición que se conmutará. Eche un vistazo a las páginas siguientes para obtener ideas sobre [cómo la ventana deslizante puede automatizarse al completo](https://msdn.microsoft.com/library/aa964122.aspx) mediante un script de Transact-SQL.  
  
### Consideraciones de rendimiento con las particiones de tabla  
 Es importante realizar las operaciones MERGE y SPLIT RANGE para evitar cualquier movimiento de datos, ya que este puede provocar una sobrecarga considerable del rendimiento. Para obtener más información, vea [Modificar una función de partición](../../relational-databases/partitions/modify-a-partition-function.md). Conseguirá esto usando la opción RANGE LEFT en lugar de la opción RANGE RIGHT cuando aplique [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md).  
  
 Vamos a explicar primero visualmente el significado de las opciones RANGE LEFT y RANGE RIGHT:  
  
 ![Partitioning3](../../relational-databases/tables/media/partitioning3.png "Partitioning3")  
  
 Si se define una función de partición como RANGE LEFT, los valores especificados son los límites superiores de las particiones. Cuando utilice la opción RANGE RIGHT, los valores especificados son los límites inferiores de las particiones. Cuando utilice la operación MERGE RANGE para quitar un límite de la definición de la función de partición, la implementación subyacente también quita la partición que contiene el límite. Si esa partición no está vacía, los datos se moverán a la partición que resulta de la operación MERGE RANGE.  
  
 En el escenario de ventana deslizante, siempre quitamos el límite inferior de la partición.  
  
-   Caso de RANGE LEFT: en el caso de RANGE LEFT, el límite inferior de la partición pertenece a la partición 1, que está vacía (después de conmutar la partición), por lo que MERGE RANGE no causará ningún movimiento de datos.  
  
-   Caso de RANGE RIGHT: el caso RANGE RIGHT, el límite inferior de la partición pertenece a la partición 2, que no está vacía ya que supusimos que la partición 1 se había vaciado mediante la conmutación. En este caso, la opción MERGE RANGE provocará un movimiento de datos (los datos de la partición 2 se moverán a la partición 1). Para evitar esto, la opción RANGE RIGHT del escenario de ventana deslizante debe tener la partición 1, que siempre está vacía. Esto significa que si usamos la opción RANGE RIGHT, debemos crear y mantener una partición adicional en comparación con el caso de RANGE LEFT.  
  
 Conclusión: utilizando la opción RANGE LEFT en la partición deslizante es mucho más simple para la administración de la partición y evita el movimiento de datos. Sin embargo, la definición de los límites de partición con la opción RANGE RIGHT es un poco más simple, ya que no tiene que tratar con problemas de marca de tiempo de fecha y hora.  
  
## Uso del enfoque de script de limpieza personalizado  
 En los casos en los que el enfoque de particiones de tabla y Stretch Database no sean opciones viables, el tercer enfoque consiste en eliminar los datos de la tabla de historial con el script de limpieza personalizado. La eliminación de los datos de la tabla de historial es posible solo cuando aplica **SYSTEM_VERSIONING = OFF**. Para evitar la incoherencia de datos, realice la limpieza durante la ventana de mantenimiento (cuando las cargas de trabajo que modifican datos no están activas) o dentro de una transacción (bloqueando de forma efectiva otras cargas de trabajo).  Esta operación requiere el permiso de **CONTROL** sobre tablas de historial y actuales.  
  
 Para bloquear mínimamente las aplicaciones normales y las consultas de usuario, elimine los datos en fragmentos más pequeños con un retraso al realizar el script de limpieza dentro de una transacción. Aunque no hay ningún tamaño óptimo para la eliminación de cada fragmento de datos en todos los escenarios, la eliminación de más de 10.000 filas en una sola transacción puede suponer un impacto significativo.  
  
 La lógica de limpieza es la misma para todas las tablas temporales, por lo que se puede automatizar de forma relativamente sencilla a través de un procedimiento almacenado genérico que puede programar para que se ejecute periódicamente para cada tabla temporal para la que desee limitar el historial de datos.  
  
 El siguiente diagrama muestra cómo debe organizarse la lógica de limpieza para una tabla única para reducir el impacto en las cargas de trabajo en ejecución.  
  
 ![CustomCleanUpScriptDiagram](../../relational-databases/tables/media/customcleanupscriptdiagram.png "CustomCleanUpScriptDiagram")  
  
 Estas son algunas directrices de alto nivel para implementar el proceso. Programe la lógica de limpieza para que se ejecute todos los días y realice la iteración sobre todas las tablas temporales que necesitan la limpieza de datos. Use el Agente SQL Server u otra herramienta para programar este proceso:  
  
-   Elimine los datos históricos en cada tabla temporal empezando por las filas más antiguas hasta las más recientes en varias iteraciones en pequeños fragmentos y evite la eliminación de todas las filas en una sola transacción tal como se muestra en la imagen anterior.  
  
-   Implemente cada iteración como una invocación del procedimiento almacenado genérico que quita una parte de datos de la tabla de historial (vea el ejemplo de código siguiente para este procedimiento).  
  
-   Calcule el número de filas que debe eliminar para una tabla temporal individual cada vez que se invoca el proceso. Según esto y el número de iteraciones que desee tener, determine dinámicamente los puntos de división para cada invocación del procedimiento.  
  
-   Planifique un período de retraso entre las iteraciones para una tabla única para reducir el impacto en las aplicaciones que dispongan de acceso a la tabla temporal.  
  
 Un procedimiento almacenado que permita eliminar los datos de una tabla temporal única podría ser similar al fragmento de código siguiente (revise este código con cuidado y ajústelo antes de aplicarlo a su entorno):  
  
```  
DROP PROCEDURE IF EXISTS sp_CleanupHistoryData;  
GO  
  
CREATE PROCEDURE sp_CleanupHistoryData  
         @temporalTableSchema sysname  
       , @temporalTableName sysname  
       , @cleanupOlderThanDate datetime2  
AS  
    DECLARE @disableVersioningScript nvarchar(max) = '';  
    DECLARE @deleteHistoryDataScript nvarchar(max) = '';  
    DECLARE @enableVersioningScript nvarchar(max) = '';  
  
DECLARE @historyTableName sysname    
DECLARE @historyTableSchema sysname    
DECLARE @periodColumnName sysname    
  
/*Generate script to discover history table name and end of period column for given temporal table name*/  
EXECUTE sp_executesql   
    N'SELECT @hst_tbl_nm = t2.name, @hst_sch_nm = s.name, @period_col_nm = c.name  
        FROM sys.tables t1   
           JOIN sys.tables t2 on t1.history_table_id = t2.object_id  
        JOIN sys.schemas s on t2.schema_id = s.schema_id  
            JOIN sys.periods p on p.object_id = t1.object_id  
           JOIN sys.columns c on p.end_column_id = c.column_id and c.object_id = t1.object_id  
                  WHERE   
                 t1.name = @tblName and s.name = @schName'  
                , N'@tblName sysname  
                , @schName sysname  
                , @hst_tbl_nm sysname OUTPUT  
                , @hst_sch_nm sysname OUTPUT  
                , @period_col_nm sysname OUTPUT'  
                , @tblName = @temporalTableName  
                , @schName = @temporalTableSchema  
                , @hst_tbl_nm = @historyTableName OUTPUT  
                , @hst_sch_nm = @historyTableSchema OUTPUT  
                , @period_col_nm = @periodColumnName OUTPUT   
  
IF @historyTableName IS NULL OR @historyTableSchema IS NULL OR @periodColumnName IS NULL  
    THROW 50010, 'History table cannot be found. Either specified table is not system-versioned temporal or you have provided incorrect argument values.', 1  
  
/*Generate 3 statements that will run inside a transaction: SET SYSTEM_VERSIONING = OFF, DELETE FROM history_table, SET SYSTEM_VERSIONING = ON */  
SET @disableVersioningScript =  @disableVersioningScript + 'ALTER TABLE [' + @temporalTableSchema + '].[' + @temporalTableName + '] SET (SYSTEM_VERSIONING = OFF)'  
SET @deleteHistoryDataScript =  @deleteHistoryDataScript + ' DELETE FROM  [' + @historyTableSchema + '].[' + @historyTableName + ']   
     WHERE ['+ @periodColumnName + '] < ' + '''' + convert(varchar(128), @cleanupOlderThanDate, 126) +  ''''   
SET @enableVersioningScript =  @enableVersioningScript + ' ALTER TABLE [' + @temporalTableSchema + '].[' + @temporalTableName + ']   
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = [' + @historyTableSchema + '].[' + @historyTableName + '], DATA_CONSISTENCY_CHECK = OFF )); '   
  
BEGIN TRAN  
    EXEC (@disableVersioningScript);  
    EXEC (@deleteHistoryDataScript);  
    EXEC (@enableVersioningScript);  
COMMIT;  
```  
  
## Vea también  
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)   
 [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Comprobaciones de coherencia del sistema de la tabla temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Creación de particiones con tablas temporales](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Limitaciones y consideraciones de las tablas temporales](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Seguridad de la tabla temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funciones y vistas de metadatos de la tabla temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  