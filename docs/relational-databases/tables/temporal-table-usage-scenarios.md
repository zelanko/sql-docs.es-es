---
title: Escenarios de uso de tablas temporales | Microsoft Docs
ms.custom: ''
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 4b8fa2dd-1790-4289-8362-f11e6d63bb09
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 621387ca62340818cbe8d5529de17bcdf7e96884
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999365"
---
# <a name="temporal-table-usage-scenarios"></a>Escenarios de uso de tablas temporales
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Las tablas temporales suelen ser útiles en escenarios que requieren historial de seguimiento de cambios de datos.    
Debido a las enormes ventajas de productividad, se recomienda tener en cuenta las tablas temporales en los siguientes casos de uso.  
  
## <a name="data-audit"></a>Auditoría de datos  
 Use el control de versiones del sistema temporal en tablas que almacenan información crítica para la que necesita realizar un seguimiento de qué ha cambiado y cuándo, y para realizar análisis forense de datos en cualquier momento.    
Las tablas temporales con versión del sistema permiten planear escenarios de auditoría de datos en las primeras fases del ciclo de desarrollo o agregar auditoría de datos a aplicaciones o soluciones existentes cuando se necesita.  
  
 El siguiente diagrama muestra a un escenario de una tabla Employee con una muestra de datos que incluye versiones de fila actuales (marcadas en color azul) e históricas (marcadas en color gris).   
La parte derecha del diagrama visualiza las versiones de fila en el eje de tiempo y cuáles son las filas seleccionadas con diferentes tipos de consulta en una tabla temporal con o sin la cláusula SYSTEM_TIME.  
  
 ![EscenarioDeUsoTemporal1](../../relational-databases/tables/media/temporalusagescenario1.png "EscenarioDeUsoTemporal1")  
  
### <a name="enabling-system-versioning-on-a-new-table-for-data-audit"></a>Habilitación del control de versiones del sistema en una nueva tabla para auditoría de datos  
 Si ha identificado información que necesita datos de auditoría, cree tablas de base de datos como temporales con versión del sistema. En este sencillo ejemplo se ilustra un escenario con información sobre empleados en una hipotética base de datos de recursos humanos:  
  
```  
CREATE TABLE Employee   
(    
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED   
  , [Name] nvarchar(100) NOT NULL  
  , [Position] varchar(100) NOT NULL   
  , [Department] varchar(100) NOT NULL  
  , [Address] nvarchar(1024) NOT NULL  
  , [AnnualSalary] decimal (10,2) NOT NULL  
  , [ValidFrom] datetime2 (2) GENERATED ALWAYS AS ROW START  
  , [ValidTo] datetime2 (2) GENERATED ALWAYS AS ROW END  
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)  
 )    
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));  
```  
  
 En [Creación de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)se describen diversas opciones para crear una tabla temporal con versión del sistema.  
  
### <a name="enabling-system-versioning-on-an-existing-table-for-data-audit"></a>Habilitación del control de versiones del sistema en una tabla existente para auditoría de datos  
 Si necesita realizar auditoría de datos en bases de datos existentes, utilice ALTER TABLE para extender las tablas no temporales para convertirlas en tablas con versión del sistema. Para evitar cambios importantes en la aplicación, agregue las columnas de período como HIDDEN, como se explica en [Alter Non-Temporal Table to be System-Versioned Temporal Table (Modificación de una tabla no temporal para convertirla en tabla temporal con versión del sistema)](https://msdn.microsoft.com/library/mt590957.aspx#Anchor_3). En el ejemplo siguiente se muestra cómo habilitar el control de versiones del sistema en una tabla de Employee existente en una hipotética base de datos de recursos humanos:  
  
```  
/*   
Turn ON system versioning in Employee table in two steps   
(1) add new period columns (HIDDEN)   
(2) create default history table   
*/   
ALTER TABLE Employee   
ADD   
    ValidFrom datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , ValidTo datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);   
  
ALTER TABLE Employee    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.Employee_History));  
```  
  
 Después de ejecutar el script anterior, todos los cambios de datos se recopilarán de forma transparente en la tabla de historial.    
En un escenario de auditoría de datos típico, consultaría todos los cambios que se aplicaron a una fila individual en un período de tiempo de interés. La tabla de historial predeterminada se crea con el árbol B de almacén de filas agrupado para tratar eficazmente este caso de uso.  
  
### <a name="performing-data-analysis"></a>Realización de análisis de datos  
 Después de habilitar el control de versiones mediante cualquier de los enfoques anteriores, basta una consulta para realizar la auditoría de datos. La siguiente consulta busca versiones de fila para el registro Employee con EmployeeID = 1000 que estaban activas al menos durante una parte del período comprendido entre el 1 de enero de 2014 y el 1 de enero de 2015 (incluido el límite superior):  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME    
        BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'   
            WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 Reemplace FOR SYSTEM_TIME BETWEEN...AND por FOR SYSTEM_TIME ALL para analizar todo el historial de cambios de datos para ese empleado concreto:  
  
```  
SELECT * FROM Employee   
    FOR SYSTEM_TIME ALL WHERE    
        EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 Para buscar versiones de fila que estaban activas solo dentro de un período (y no fuera de él), use CONTAINED IN. Esta consulta es muy eficaz porque solo consulta la tabla de historial:  
  
```  
SELECT * FROM Employee FOR SYSTEM_TIME    
    CONTAINED IN ('2014-01-01 00:00:00.0000000', '2015-01-01 00:00:00.0000000')   
        WHERE EmployeeID = 1000 ORDER BY ValidFrom;  
```  
  
 Por último, en algunos escenarios de auditoría, puede que desee ver el aspecto de toda la tabla en un momento dado en el pasado:  
  
```  
SELECT * FROM Employee FOR SYSTEM_TIME AS OF '2014-01-01 00:00:00.0000000' ;  
```  
  
 Las tablas temporales con versión del sistema almacenan valores para columnas de período en la zona horaria UTC, aunque siempre es más conveniente trabajar con la zona horaria local tanto para filtrar datos como para mostrar resultados. En el ejemplo de código siguiente se muestra cómo aplicar la condición de filtrado que se especificó originalmente en la zona horaria local y después se convirtió a UTC mediante la cláusula AT TIME ZONE introducida en SQL Server 2016:  
  
```  
/*Add offset of the local time zone to current time*/  
DECLARE @asOf DATETIMEOFFSET = GETDATE() AT TIME ZONE 'Pacific Standard Time'  
/*Convert AS OF filter to UTC*/  
SET @asOf = DATEADD (MONTH, -9, @asOf) AT TIME ZONE 'UTC';  
  
SELECT   
    EmployeeID  
    , Name  
    , Position  
    , Department  
    , [Address]  
    , [AnnualSalary]  
    , ValidFrom AT TIME ZONE 'Pacific Standard Time' AS ValidFromPT   
    , ValidTo AT TIME ZONE 'Pacific Standard Time' AS ValidToPT  
FROM Employee   
    FOR SYSTEM_TIME AS OF @asOf where EmployeeId = 1000  
  
```  
  
 El uso de AT TIME ZONE es útil para todos los demás escenarios donde se usan tablas con versión del sistema.  
  
> [!TIP]  
>  Las condiciones de filtrado especificadas en cláusulas temporales con FOR SYSTEM_TIME son SARGABLE (es decir, SQL Server puede usar un índice agrupado subyacente para llevar a cabo una búsqueda en lugar de una operación de análisis.   
> Si consulta directamente la tabla de historial, asegúrese de que la condición de filtrado también sea SARGABLE especificando los filtros en forma de \<columna de período>  {< | > | =, ...} condición_fecha AT TIME ZONE "UTC".  
> Si aplica AT TIME ZONE a columnas de período, SQL Server realizará un examen de tabla o índice, lo cual puede resultar muy caro. Evite este tipo de condición en las consultas:  
> \<columna de periodo>  AT TIME ZONE "\<su zona horaria>"  >  {< | > | =, ...} condición_fecha.  
  
 Vea también: [Consulta de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md).  
  
## <a name="point-in-time-analysis-time-travel"></a>Análisis a un momento dado (viaje en el tiempo)  
 A diferencia de la auditoría de datos, donde el foco está normalmente en los cambios que se produjeron en registros individuales, en escenarios de viaje en el tiempo los usuarios desean ver cómo cambiaron los conjuntos de datos completos a lo largo del tiempo. A veces, el viaje en el tiempo incluye varias tablas temporales relacionadas, cada una de ellas cambiando a un ritmo independiente, para las que desea analizar:  
  
-   Tendencias de los indicadores importantes en los datos históricos y actuales  
  
-   Instantánea exacta de todos los datos "a partir de" cualquier momento dado del pasado (ayer, hace un mes, etc.)  
  
-   Diferencias entre dos momentos dados de interés (hace un mes frente a hace tres meses, por ejemplo)  
  
 Hay muchos escenarios reales que requieren el análisis de viaje en el tiempo. Para ilustrar este escenario de uso, echemos un vistazo a OLTP con historial generado automáticamente.  
  
### <a name="oltp-with-auto-generated-data-history"></a>OLTP con historial de datos generado automáticamente  
 En sistemas de procesamiento de transacciones, no es inusual analizar cómo cambian las métricas importantes a lo largo del tiempo. Idealmente, analizar el historial no debería afectar al rendimiento de la aplicación OLTP donde el acceso al estado más reciente de los datos debe producirse con una latencia y bloqueo de datos mínimos.  Las tablas temporales con versión del sistema están diseñadas para permitir a los usuarios mantener de forma transparente el historial completo de cambios para su análisis posterior, independientemente de los datos actuales, con un impacto mínimo en la carga de trabajo OLTP principal.  
Para cargas de trabajo con mucho procesamiento de transacciones, se recomienda usar [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md), que permiten almacenar datos actuales en memoria y el historial completo de cambios en disco de una manera eficiente.  
  
 Para la tabla de historial, se recomienda utilizar un índice de almacén de columnas agrupado por las razones siguientes:  
  
-   El análisis de tendencias típico aprovecha el rendimiento de las consultas que proporciona un índice de almacén de columnas agrupado.  
  
-   La tarea de vaciado de datos con tablas optimizadas para memoria funciona mejor con mucha carga de trabajo OLTP cuando la tabla de historial tiene un índice de almacén de columnas agrupado.  
  
-   Un índice de almacén de columnas agrupado proporciona una compresión excelente, especialmente en escenarios donde no todas las columnas se cambian al mismo tiempo.  
  
 El uso de tablas temporales con OLTP en memoria reduce la necesidad de mantener todo el conjunto de datos en memoria y permite distinguir fácilmente entre los datos activos e inactivos.  
Ejemplos de escenarios reales que encajan bien en esta categoría son la administración de inventarios o la compraventa de divisas, entre otros.  
  
 El diagrama siguiente muestra el modelo de datos simplificado utilizado para la administración de inventarios:  
  
 ![UsoTemporalEnMemoria](../../relational-databases/tables/media/temporalusageinmemory.png "UsoTemporalEnMemoria")  
  
 En el ejemplo de código siguiente se crea ProductInventory como una tabla temporal con versión del sistema en memoria con un índice de almacén de columnas agrupado en la tabla de historial (que realmente reemplaza al índice de almacén de filas que se crea de forma predeterminada):  
  
> [!NOTE]  
>  Asegúrese de que la base de datos permite la creación de tablas optimizadas para memoria. Vea [Crear una tabla con optimización para memoria y un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
```  
USE TemporalProductInventory  
GO  
  
BEGIN  
    --If table is system-versioned, SYSTEM_VERSIONING must be set to OFF first   
    IF ((SELECT temporal_type FROM SYS.TABLES WHERE object_id = OBJECT_ID('dbo.ProductInventory', 'U')) = 2)  
    BEGIN  
        ALTER TABLE [dbo].[ProductInventory] SET (SYSTEM_VERSIONING = OFF)  
    END  
    DROP TABLE IF EXISTS [dbo].[ProductInventory]  
       DROP TABLE IF EXISTS [dbo].[ProductInventoryHistory]  
END  
GO  
  
CREATE TABLE [dbo].[ProductInventory]  
(  
    ProductId int NOT NULL,  
    LocationID INT NOT NULL,  
    Quantity int NOT NULL CHECK (Quantity >=0),  
  
    SysStartTime datetime2(0) GENERATED ALWAYS AS ROW START  NOT NULL ,  
    SysEndTime datetime2(0) GENERATED ALWAYS AS ROW END  NOT NULL ,  
    PERIOD FOR SYSTEM_TIME(SysStartTime,SysEndTime),  
  
    --Primary key definition  
    CONSTRAINT PK_ProductInventory PRIMARY KEY NONCLUSTERED (ProductId, LocationId)  
)  
WITH  
(  
    MEMORY_OPTIMIZED=ON,      
    SYSTEM_VERSIONING = ON   
    (          
        HISTORY_TABLE = [dbo].[ProductInventoryHistory],          
        DATA_CONSISTENCY_CHECK = ON  
    )  
)  
  
CREATE CLUSTERED COLUMNSTORE INDEX IX_ProductInventoryHistory ON [ProductInventoryHistory]  
WITH (DROP_EXISTING = ON);  
```  
  
 Para el modelo anterior, este podría ser el aspecto del procedimiento para mantener el inventario:  
  
```  
CREATE PROCEDURE [dbo].[spUpdateInventory]  
@productId int,  
@locationId int,  
@quantityIncrement int  
  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')  
    UPDATE dbo.ProductInventory  
        SET Quantity = Quantity + @quantityIncrement   
            WHERE ProductId = @productId AND LocationId = @locationId  
  
/*If zero rows were updated than this is insert of the new product for a given location*/  
    IF @@rowcount = 0  
        BEGIN  
            IF @quantityIncrement < 0  
                SET @quantityIncrement = 0  
            INSERT INTO [dbo].[ProductInventory]  
                (  
                    [ProductId]  
                    ,[LocationID]  
                    ,[Quantity]  
                )  
                VALUES  
                   (  
                        @productId  
                       ,@locationId  
                       ,@quantityIncrement  
        END  
END;  
```  
  
 El procedimiento almacenado spUpdateInventory inserta un nuevo producto en el inventario o actualiza la cantidad de productos para la ubicación específica. La lógica de negocios es muy sencilla y se centra en mantener la precisión del estado más reciente en todo momento incrementando o disminuyendo el campo Quantity a través de la actualización de la tabla, mientras que las tablas con versión del sistema agregan de forma transparente dimensión de historial a los datos, como se muestra en el diagrama siguiente.  
  
 ![UsoTemporalEnMemoria2b](../../relational-databases/tables/media/temporalusageinmemory2b.png "UsoTemporalEnMemoria2b")  
  
 Ahora, la consulta del estado más reciente puede realizarse eficazmente desde el módulo compilado de forma nativa:  
  
```  
CREATE PROCEDURE [dbo].[spQueryInventoryLatestState]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT, LANGUAGE=N'English')  
    SELECT ProductId, LocationID, Quantity, SysStartTime  
      FROM dbo.ProductInventory  
    ORDER BY ProductId, LocationId  
END;  
GO  
EXEC [dbo].[spQueryInventoryLatestState];  
```  
  
 El análisis de los datos a lo largo del tiempo pasa a ser una tarea muy sencilla con la cláusula FOR SYSTEM_TIME ALL, tal como se muestra en el ejemplo siguiente:  
  
```  
DROP VIEW IF EXISTS vw_GetProductInventoryHistory;  
GO  
CREATE VIEW vw_GetProductInventoryHistory  
AS  
   SELECT ProductId, LocationId, Quantity, SysStartTime, SysEndTime   
   FROM [dbo].[ProductInventory]  
   FOR SYSTEM_TIME ALL;  
GO  
SELECT * FROM vw_GetProductInventoryHistory   
    WHERE ProductId = 2;  
```  
  
 El diagrama siguiente muestra el historial de datos de un producto que se puede representar fácilmente importando la vista anterior en Power Query, Power BI o una herramienta de inteligencia empresarial similar:  
  
 ![HistorialDeProductosEnElTiempo](../../relational-databases/tables/media/producthistoryovertime.png "HistorialDeProductosEnElTiempo")  
  
 Las tablas temporales se pueden utilizar en este escenario para realizar otros tipos de análisis de viaje en el tiempo, como reconstruir el estado de AS OF del inventario a cualquier momento dado del pasado o comparar instantáneas que pertenecen a diferentes momentos en el tiempo.  
  
 Para este escenario de uso, también puede extender las tablas Product y Location para convertirlas en tablas temporales, lo que permite un análisis posterior del historial de cambios de UnitPrice y NumberOfEmployee.  
  
```  
ALTER TABLE Product   
ADD   
    SysStartTime datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DF_ValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , SysEndTime datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);   
  
ALTER TABLE Product    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.ProductHistory));  
  
ALTER TABLE [Location]  
ADD   
    SysStartTime datetime2 (2) GENERATED ALWAYS AS ROW START HIDDEN    
        constraint DFValidFrom DEFAULT DATEADD(second, -1, SYSUTCDATETIME())  
    , SysEndTime datetime2 (2)  GENERATED ALWAYS AS ROW END HIDDEN     
        constraint DFValidTo DEFAULT '9999.12.31 23:59:59.99'  
    , PERIOD FOR SYSTEM_TIME (SysStartTime, SysEndTime);  
  
ALTER TABLE [Location]    
    SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.LocationHistory));  
```  
  
 Puesto que el modelo de datos ahora implica varias tablas temporales, la práctica recomendada para el análisis AS OF es crear una vista que extraiga los datos necesarios de las tablas relacionadas y aplicar FOR SYSTEM_TIME AS OF a la vista, ya que esto simplificará considerablemente la reconstrucción del estado de todo el modelo de datos:  
  
```  
DROP VIEW IF EXISTS vw_ProductInventoryDetails;  
GO  
  
CREATE VIEW vw_ProductInventoryDetails  
AS  
    SELECT PrInv.ProductId ,PrInv.LocationId, P.ProductName, L.LocationName, PrInv.Quantity  
    , P.UnitPrice, L.NumberOfEmployees  
    , P.SysStartTime AS ProductStartTime, P.SysEndTime AS ProductEndTime  
    , L.SysStartTime AS LocationStartTime, L.SysEndTime AS LocationEndTime  
    , PrInv.SysStartTime AS InventoryStartTime, PrInv.SysEndTime AS InventoryEndTime  
FROM dbo.ProductInventory as PrInv  
JOIN dbo.Product AS P ON PrInv.ProductId = P.ProductID  
JOIN dbo.Location AS L ON PrInv.LocationId = L.LocationID;  
GO  
SELECT * FROM vw_ProductInventoryDetails  
    FOR SYSTEM_TIME AS OF '2015.01.01';   
```  
  
 En la siguiente imagen se muestra el plan de ejecución generado para la consulta SELECT. Esto ilustra que el motor de SQL Server controla completamente toda la complejidad de trabajar con las relaciones temporales:  
  
 ![PlanDeEjecuciónASOF](../../relational-databases/tables/media/asofexecutionplan.png "PlanDeEjecuciónASOF")  
  
 Utilice el código siguiente para comparar el estado del inventario de productos entre dos momentos dados (hace un día y hace un mes):  
  
```  
DECLARE @dayAgo datetime2 (0) = DATEADD (day, -1, SYSUTCDATETIME());  
DECLARE @monthAgo datetime2 (0) = DATEADD (month, -1, SYSUTCDATETIME());  
  
SELECT   
    inventoryDayAgo.ProductId  
    , inventoryDayAgo.ProductName  
    , inventoryDayAgo.LocationName  
    , inventoryDayAgo.Quantity AS QuantityDayAgo,inventoryMonthAgo.Quantity AS QuantityMonthAgo  
    , inventoryDayAgo.UnitPrice AS UnitPriceDayAgo, inventoryMonthAgo.UnitPrice AS UnitPriceMonthAgo  
FROM vw_ProductInventoryDetails  
FOR SYSTEM_TIME AS OF @dayAgo AS inventoryDayAgo  
JOIN vw_ProductInventoryDetails FOR SYSTEM_TIME AS OF @monthAgo AS inventoryMonthAgo  
    ON inventoryDayAgo.ProductId = inventoryMonthAgo.ProductId AND inventoryDayAgo.LocationId = inventoryMonthAgo.LocationID;  
```  
  
## <a name="anomaly-detection"></a>Detección de anomalías  
 La detección de anomalías (o detección de valores atípicos) es la identificación de los elementos que no cumplen un patrón esperado u otros elementos en un conjunto de datos.   
Puede utilizar tablas temporales con versión del sistema para detectar anomalías que se producen periódica o irregularmente como puede usar consultas temporales para encontrar rápidamente patrones específicos.  
De qué anomalías se trata depende del tipo de datos que se recopilan y de la lógica de negocios.  
  
 En el ejemplo siguiente se muestra una lógica simplificada para detectar "picos" en las cifras de ventas. Supongamos que trabaja con una tabla temporal que recopila el historial de los productos comprados:  
  
```  
CREATE TABLE [dbo].[Product]  
                (  
            [ProdID] [int] NOT NULL PRIMARY KEY CLUSTERED  
        , [ProductName] [varchar](100) NOT NULL  
        , [DailySales] INT NOT NULL  
        , [ValidFrom] [datetime2](7) GENERATED ALWAYS AS ROW START NOT NULL  
        , [ValidTo] [datetime2](7) GENERATED ALWAYS AS ROW END NOT NULL  
        , PERIOD FOR SYSTEM_TIME ([ValidFrom], [ValidTo])  
    )  
    WITH( SYSTEM_VERSIONING = ON (HISTORY_TABLE = [dbo].[ProductHistory]   
        , DATA_CONSISTENCY_CHECK = ON ))  
  
```  
  
 El diagrama siguiente muestra las compras a lo largo del tiempo:  
  
 ![DetecciónDeAnomalíaTemporal](../../relational-databases/tables/media/temporalanomalydetection.png "DetecciónDeAnomalíaTemporal")  
  
 Suponiendo que durante los días normales el número de productos comprados tiene una pequeña variación, la siguiente consulta identifica los valores atípicos de singleton. Se trata de ejemplos cuya diferencia en comparación con sus vecinos inmediatos es considerable (el doble), mientras que las muestras adyacentes no difieren significativamente (menos del 20 %):  
  
```  
WITH CTE (ProdId, PrevValue, CurrentValue, NextValue, ValidFrom, ValidTo)  
AS  
    (  
        SELECT   
            ProdId, LAG (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as PrevValue  
            , DailySales, LEAD (DailySales, 1, 1) over (partition by ProdId order by ValidFrom) as NextValue   
             , ValidFrom, ValidTo from Product  
        FOR SYSTEM_TIME ALL  
)  
  
SELECT   
    ProdId  
    , PrevValue  
    , CurrentValue  
    , NextValue  
    , ValidFrom  
    , ValidTo  
    , ABS (PrevValue - NextValue) / convert (float, (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END)) as PrevToNextDiff  
    , ABS (CurrentValue - PrevValue) / convert (float, (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END)) as CurrentToPrevDiff  
    , ABS (CurrentValue - NextValue) / convert (float, (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END)) as CurrentToNextDiff  
FROM CTE   
    WHERE   
        ABS (PrevValue - NextValue) / (CASE WHEN NextValue > PrevValue THEN PrevValue ELSE NextValue END) < 0.2  
            AND ABS (CurrentValue - PrevValue) / (CASE WHEN CurrentValue > PrevValue THEN PrevValue ELSE CurrentValue END) > 2  
            AND ABS (CurrentValue - NextValue) / (CASE WHEN CurrentValue > NextValue THEN NextValue ELSE CurrentValue END) > 2;  
```  
  
> [!NOTE]  
>  Este ejemplo está simplificado deliberadamente. En los escenarios de producción, probablemente utilizaría avanzados métodos estadísticos para identificar las muestras que no siguen el patrón común.  
  
## <a name="slowly-changing-dimensions"></a>Dimensiones de variación lenta  
 Las dimensiones de almacenamiento de datos normalmente contienen datos relativamente estáticos sobre entidades como ubicaciones geográficas, clientes o productos. Sin embargo, algunos escenarios también requieren realizar el seguimiento de cambios de datos en tablas de dimensiones. Dado que la modificación en las dimensiones ocurre con mucha menos frecuencia, de una forma impredecible y fuera de la programación de actualizaciones normal que se aplica a tablas de hechos, estos tipos de tablas de dimensiones se denominan dimensiones de variación lenta (DVL).  
  
 Existen varias categorías de dimensiones de variación lenta basadas en la forma de conservar el historial de cambios:  
  
-   Tipo 0:  No se conserva el historial. Los atributos de dimensión reflejan los valores originales.  
  
-   Tipo 1:  Los atributos de dimensión reflejan los valores más recientes (los valores anteriores se sobrescriben).  
  
-   Tipo 2:  Cada versión de miembro de dimensión se representa con una fila independiente en la tabla normalmente con columnas que representan el período de validez.  
  
-   Tipo 3: Mantener el historial limitado para los atributos seleccionados usando columnas adicionales en la misma fila.  
  
-   Tipo 4: Mantener el historial en la tabla independiente mientras la tabla de dimensiones original mantiene las versiones de miembro de dimensión más recientes (actual).  
  
 Cuando se elige la estrategia DVL, es responsabilidad de la capa Extraer-Transformar-Cargar (ETL, Extraer-Transformar-Cargar) mantener la precisión de las tablas de dimensiones, tarea que normalmente requiere una gran cantidad de código y un mantenimiento complejo.  
  
 Las tablas temporales con versión del sistema de SQL Server 2016 pueden utilizarse para reducir considerablemente la complejidad del código ya que el historial de los datos cuando se conserva automáticamente. Dada su implementación con dos tablas, las tablas temporales de SQL Server 2016 es los más próximo a DVL de tipo 4. Sin embargo, puesto que las consultas temporales solo permiten hacer referencia a la tabla actual, también puede plantearse el uso de tablas temporales en entornos donde piensa usar DVL de tipo 2.  
  
 Para convertir la dimensión normal en DVL, basta con crear una nueva o modificar una existente para convertirse en una tabla temporal con versión del sistema. Si la tabla de dimensiones existente contiene datos históricos, cree una tabla independiente y mueva los datos históricos allí, y mantenga las versiones de dimensión actuales (reales) en la tabla de dimensiones original. Después, utilice la sintaxis ALTER TABLE para convertir la tabla de dimensiones a una tabla temporal con versión del sistema con una tabla de historial predefinida.  
  
 En el ejemplo siguiente se ilustra el proceso y se supone que la tabla de dimensiones DimLocation ya tiene ValidFrom y ValidTo como columnas que no admiten valores NULL datetime2 y que el proceso ETL rellena:  
  
```  
/*Move "closed" row versions into newly created history table*/  
SELECT * INTO  DimLocationHistory  
    FROM DimLocation  
        WHERE ValidTo < '9999-12-31 23:59:59.99';  
GO  
/*Create clustered columnstore index which is a very good choice in DW scenarios*/  
CREATE CLUSTERED COLUMNSTORE INDEX IX_DimLocationHistory ON DimLocationHistory  
/*Delete previous versions from DimLocation which will become current table in temporal-system-versioning configuration*/  
DELETE FROM DimLocation  
    WHERE ValidTo < '9999-12-31 23:59:59.99';  
/*Add period definition*/  
ALTER TABLE DimLocation ADD PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo);  
/*Enable system-versioning and bind histiory table to the DimLocation*/  
ALTER TABLE DimLocation SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.DimLocationHistory));  
```  
  
 Tenga en cuenta que no se necesita código adicional para mantener DVL durante el proceso de carga de almacenamiento de datos una vez que se ha creado.  
  
 La siguiente ilustración muestra cómo puede utilizar las tablas temporales en un escenario sencillo que implica 2 DVL (DimLocation y DimProduct) y una tabla de hechos.  
  
 ![SCDTemporal](../../relational-databases/tables/media/temporalscd.png "SCDTemporal")  
  
 Para poder utilizar las DVL en los informes, debe ajustar eficazmente las consultas. Por ejemplo, puede que le interese calcular la cantidad total de ventas y el promedio de productos vendidos per cápita durante los últimos seis meses.  Observe que ambas métricas requieren la correlación de datos de la tabla de hechos y las dimensiones que podrían haber cambiado sus atributos importantes para el análisis (DimLocation.NumOfCustomers, DimProduct.UnitPrice).  La siguiente consulta calcula correctamente las métricas requeridas:  
  
```  
DECLARE @now datetime2 = SYSUTCDATETIME()  
DECLARE @sixMonthsAgo datetime2 SET   
    @sixMonthsAgo = DATEADD (month, -12, SYSUTCDATETIME())   
  
SELECT DimProduct_History.ProductId  
   , DimLocation_History.LocationId  
    , SUM(F.Quantity * DimProduct_History.UnitPrice) AS TotalAmount  
    , AVG (F.Quantity/DimLocation_History.NumOfCustomers) AS AverageProductsPerCapita   
FROM FactProductSales F   
/* find corresponding record in SCD history in last 6 months, based on matching fact */  
JOIN DimLocation FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimLocation_History   
    ON DimLocation_History.LocationId = F.LocationId   
        AND F.FactDate BETWEEN DimLocation_History.ValidFrom AND DimLocation_History.ValidTo   
/* find corresponding record in SCD history in last 6 months, based on matching fact */  
JOIN DimProduct FOR SYSTEM_TIME BETWEEN @sixMonthsAgo AND @now AS DimProduct_History   
    ON DimProduct_History.ProductId = F.ProductId  
        AND F.FactDate BETWEEN DimProduct_History.ValidFrom AND DimProduct_History.ValidTo   
    WHERE F.FactDate BETWEEN @sixMonthsAgo AND @now   
GROUP BY DimProduct_History.ProductId, DimLocation_History.LocationId ;  
```  
  
 **Consideraciones:**  
  
-   El uso de tablas temporales con versión del sistema para DVL es aceptable si el período de validez calculado en función del tiempo de transacción de base de datos está bien con la lógica de negocios. Si carga los datos con un retraso importante, el tiempo de la transacción puede no ser aceptable.  
  
-   De forma predeterminada, las tablas temporales con versión del sistema no permiten cambiar los datos históricos después de la carga (puede modificar el historial después de establecer SYSTEM_VERSIONING en OFF). Esto podría ser la limitación en casos donde el cambio de datos históricos ocurre con regularidad.  
  
-   Las tablas temporales con versión del sistema generan versión de fila en cualquier cambio de columna. Si desea suprimir nuevas versiones en ciertos cambios de columna debe incorporar esa limitación en la lógica ETL.  
  
-   Si espera un número significativo de filas históricas en tablas de DVL, considere el uso de un índice de almacén de columnas agrupado como la opción de almacenamiento principal para la tabla de historial. Eso reducirá la superficie de la tabla de historial y acelerará las consultas analíticas.  
  
## <a name="repairing-row-level-data-corruption"></a>Reparación de daños en los datos de fila  
 Puede basarse en los datos históricos de las tablas temporales con versión del sistema para reparar rápidamente filas individuales a cualquiera de los estados capturados anteriormente. Esta propiedad de tablas temporales es muy útil cuando es posible localizar filas afectadas y/o cuando conoce la hora del cambio de datos no deseado de forma que puede realizar la reparación de manera muy eficaz sin ocuparse de las copias de seguridad.  
  
 Este enfoque presenta una serie de ventajas:  
  
-   Es posible controlar el ámbito de la reparación de manera muy precisa. Los registros que no se ven afectados deben permanecer en el estado más reciente, que suele ser un requisito crítico.  
  
-   La operación es muy eficaz y la base de datos permanece en línea para todas las cargas de trabajo usando los datos.  
  
-   La propia operación de reparación es con versiones. Tendrá la pista de auditoría de la propia operación de reparación, por lo que puede analizar qué ocurrió posteriormente si es necesario.  
  
 La acción de reparación puede automatizarse con relativa facilidad. Este es el ejemplo de código del procedimiento almacenado que realiza la reparación de datos para la tabla Employee usada en el escenario de auditoría de datos.  
  
```  
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecord;  
GO  
  
CREATE PROCEDURE sp_RepairEmployeeRecord   
    @EmployeeID INT,  
    @versionNumber INT = 1  
AS  
  
;WITH History  
AS  
(  
        /* Order historical rows by tehir age in DESC order*/  
        SELECT ROW_NUMBER () OVER (PARTITION BY EmployeeID ORDER BY [ValidTo] DESC) AS RN, *  
        FROM Employee FOR SYSTEM_TIME ALL WHERE YEAR (ValidTo) < 9999 AND Employee.EmployeeID = @EmployeeID  
)  
  
/*Update current row by using N-th row version from history (default is 1 - i.e. last version)*/  
UPDATE Employee   
    SET [Position] = H.[Position], [Department] = H.Department, [Address] = H.[Address], AnnualSalary = H.AnnualSalary  
    FROM Employee E JOIN History H ON E.EmployeeID = H.EmployeeID AND RN = @versionNumber  
    WHERE E.EmployeeID = @EmployeeID  
  
```  
  
 Este procedimiento almacenado toma @EmployeeID y @versionNumber como parámetros de entrada. Este procedimiento restaura de forma predeterminada el estado de fila a la versión más reciente a partir del historial (@versionNumber = 1).  
  
 La siguiente imagen muestra el estado de la fila antes y después de la invocación del procedimiento. El rectángulo rojo marca la versión de fila actual que no es correcta, mientras que el rectángulo verde marca la versión correcta del historial.  
  
 ![ReparaciónDeUsoTemporal1](../../relational-databases/tables/media/temporalusagerepair1.png "ReparaciónDeUsoTemporal1")  
  
```  
EXEC sp_RepairEmployeeRecord @EmployeeID = 1, @versionNumber = 1  
```  
  
 ![ReparaciónDeUsoTemporal2](../../relational-databases/tables/media/temporalusagerepair2.png "ReparaciónDeUsoTemporal2")  
  
 Este procedimiento almacenado de reparación puede definirse para aceptar una marca de tiempo exacta en lugar de la versión de fila. Restaurará la fila a cualquier versión que estuviera activa para el momento dado proporcionado (es decir, el momento dado AS OF).  
  
```  
DROP PROCEDURE IF EXISTS sp_RepairEmployeeRecordAsOf;  
GO  
  
CREATE PROCEDURE sp_RepairEmployeeRecordAsOf   
    @EmployeeID INT,  
    @asOf datetime2  
AS  
  
/*Update current row to the state that was actual AS OF provided date*/  
UPDATE Employee   
    SET [Position] = History.[Position], [Department] = History.Department, [Address] = History.[Address], AnnualSalary = History.AnnualSalary  
    FROM Employee AS E JOIN Employee FOR SYSTEM_TIME AS OF @asOf AS History  ON E.EmployeeID = History.EmployeeID  
    WHERE E.EmployeeID = @EmployeeID  
  
```  
  
 Para el mismo ejemplo de datos la siguiente imagen ilustra el escenario de reparación con la condición de tiempo. Se resaltan el parámetro @asOf, la fila seleccionada en el historial que era real en el momento dado proporcionado y la nueva versión de fila en la tabla actual después de la operación de reparación:  
  
 ![ReparaciónDeUsoTemporal3](../../relational-databases/tables/media/temporalusagerepair3.png "ReparaciónDeUsoTemporal3")  
  
 La corrección de datos puede convertirse en parte de la carga de datos automatizada en el almacenamiento de datos y los sistemas de informes.  
Si un valor recién actualizado no es correcto entonces, en muchos escenarios, la restauración de la versión anterior del historial es una mitigación suficientemente buena. En el siguiente diagrama se muestra cómo se puede automatizar este proceso:  
  
 ![ReparaciónDeUsoTemporal4](../../relational-databases/tables/media/temporalusagerepair4.png "ReparaciónDeUsoTemporal4")  
  
## <a name="see-also"></a>Consulte también  
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)   
 [Introducción a las tablas temporales con versión del sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Comprobaciones de coherencia del sistema de la tabla temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)   
 [Creación de particiones con tablas temporales](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Limitaciones y consideraciones de las tablas temporales](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Seguridad de la tabla temporal](../../relational-databases/tables/temporal-table-security.md)   
 [Tablas temporales con control de versiones del sistema con tablas con optimización para memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Funciones y vistas de metadatos de la tabla temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
