---
title: Modificación de los datos de una tabla temporal con control de versiones del sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5f398470-c531-47b5-84d5-7c67c27df6e5
caps.latest.revision: 8
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3df5a6e48c644c43082508805d28eb38624e6f0e
ms.sourcegitcommit: 67d5f2a654b36da7fcc7c39d38b8bcf45791acc3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/14/2018
ms.locfileid: "39038112"
---
# <a name="modifying-data-in-a-system-versioned-temporal-table"></a>Modificación de los datos de una tabla temporal con control de versiones del sistema
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Se modifican los datos de una tabla temporal con control de versiones del sistema mediante instrucciones DML regulares con una diferencia importante: no es posible modificar directamente los datos de las columnas PERIOD. Al actualizar algún dato, se crea una nueva versión y la instancia antigua de cada fila actualizada se inserta en la tabla de historial. Al eliminar algún dato, la eliminación es lógica; es decir, la fila se mueve a la tabla de historial desde la actual, no se elimina directamente.  
  
## <a name="inserting-data"></a>Inserción de datos  
 Al insertar nuevos datos, debe tener en cuenta las columnas **PERIOD** si no presentan la condición **HIDDEN**. También puede utilizar la modificación de la partición con las tablas temporales con control de versiones del sistema.  
  
### <a name="insert-new-data-with-visible-period-columns"></a>Inserción de nuevos datos con columnas PERIOD visibles  
 Puede escribir su instrucción **INSERT** cuando tenga columnas **PERIOD** visibles como se muestra a continuación para tener en cuenta las nuevas columnas **PERIOD** :  
  
-   Si especifica la lista de columnas en su instrucción **INSERT** , puede omitir las columnas **PERIOD** porque el sistema generará automáticamente valores para ellas.  
  
    ```  
    --Insert with column list and without period columns   
    INSERT INTO [dbo].[Department] ([DeptID] ,[DeptName] ,[ManagerID] ,[ParentDeptID])   
    VALUES(10, 'Marketing', 101, 1);  
  
    ```  
  
-   Si especifica las columnas**PERIOD** en la lista de columnas en su instrucción **INSERT** , tendrá que indicar **DEFAULT** como su valor.  
  
    ```  
    INSERT INTO [dbo].[Department] ([DeptID] ,[DeptName] ,[ManagerID] ,[ParentDeptID], SysStartTime, SysEndTime)   
    VALUES(11, 'Sales', 101, 1, default, default);  
  
    ```  
  
-   Si no se especifica la lista de columnas en su instrucción **INSERT** , indique **DEFAULT** para las columnas **PERIOD** .  
  
    ```  
    --Insert without  column list and DEFAULT values for period columns   
    INSERT INTO [dbo].[Department]    
    VALUES(12, 'Production', 101, 1, default, default);  
  
    ```  
  
### <a name="insert-data-into-a-table-with-hidden-period-columns"></a>Inserción de datos en una tabla con columnas PERIOD HIDDEN  
 Si las columnas **PERIOD** se especifican como HIDDEN, solo tendrá que indicar los valores para las columnas visibles cuando utilice INSERT sin especificar la lista de columnas. No hace falta tener en cuenta las nuevas columnas **PERIOD** en su instrucción **INSERT** . Este comportamiento garantiza que las aplicaciones heredadas seguirán funcionando aunque habilite el control de versiones del sistema en las tablas en las que resultará provechoso.  
  
```  
CREATE TABLE [dbo].[CompanyLocation]  
(   
     [LocID] [int] IDENTITY(1,1) NOT NULL PRIMARY KEY  
   , [LocName] [varchar](50) NOT NULL  
   , [City] [varchar](50) NOT NULL  
   , [SysStartTime] [datetime2](0) GENERATED ALWAYS AS ROW START HIDDEN NOT NULL   
   , [SysEndTime] [datetime2](0) GENERATED ALWAYS AS ROW END HIDDEN NOT NULL   
   , PERIOD FOR SYSTEM_TIME ([SysStartTime], [SysEndTime])   
)    
WITH ( SYSTEM_VERSIONING = ON );   
GO   
INSERT INTO [dbo].[CompanyLocation]   
VALUES  ('Headquarters', 'New York');  
  
```  
  
### <a name="inserting-data-using-partition-switch"></a>Inserción de datos mediante PARTITION SWITCH  
 Si la tabla actual tiene particiones, puede utilizar la modificación de particiones como un mecanismo eficaz para cargar datos en una partición vacía o en varias particiones en paralelo.   
La tabla de almacenamiento provisional usada en la instrucción **PARTITION SWITCH IN** con una tabla temporal con control de versiones del sistema debe tener definido **SYSTEM_TIME PERIOD** , pero no tiene que tratarse de una tabla temporal con control de versiones del sistema.    
Así se garantiza la realización de comprobaciones de coherencia durante la inserción de datos en una tabla de almacenamiento provisional o cuando se agregue PERIOD de SYSTEM_TIME a una tabla de este tipo rellenada previamente.  
  
```  
/*Create staging table with period definition for SWITCH IN temporal table*/   
CREATE TABLE [dbo].[Staging_Department_Partition2]  
(   
     [DeptID] [int] NOT NULL  
   , [DeptName] [varchar](50)  NOT NULL  
   , [ManagerID] [int] NULL  
   , [ParentDeptID] [int] NULL  
   , [SysStartTime] [datetime2](7) GENERATED ALWAYS AS ROW START NOT NULL  
   , [SysEndTime] [datetime2](7) GENERATED ALWAYS AS ROW END NOT NULL  
   , PERIOD FOR SYSTEM_TIME ( [SysStartTime], [SysEndTime] )   
) ON [PRIMARY]   
  
/*Create aligned primary key*/   
ALTER TABLE [dbo].[Staging_Department_Partition2]    
ADD CONSTRAINT [Staging_Department_Partition2_PK]  
   PRIMARY KEY CLUSTERED  
   (  [DeptID] ASC )     
   ON [PRIMARY]   
  
/*   
Create and enforce constraints for partition boundaries.   
Partition 2 contains rows with DeptID > 100 and DeptID <=200   
*/   
ALTER TABLE [dbo].[Staging_Department_Partition2]      
   WITH CHECK ADD  CONSTRAINT [chk_staging_Department_partition_2]     
   CHECK  ([DeptID]>N'100' AND [DeptID]<=N'200')   
ALTER TABLE [dbo].[Staging_Department_Partition2]    
   CHECK CONSTRAINT [chk_staging_Department_partition_2]   
  
/*Load data into staging table*/   
INSERT INTO [dbo].[staging_Department] ([DeptID],[DeptName],[ManagerID],[ParentDeptID])   
VALUES (101,'D101',1,NULL)  
  
/*Use PARTITION SWITCH IN to efficiently add data to current table */    
ALTER TABLE [Staging_Department]    
SWITCH TO [dbo].[Department] PARTITION 2;  
  
```  
  
 Si trata de aplicar la instrucción PARTITION SWITCH desde una tabla sin una definición de periodo, se le mostrará un mensaje de error: `Msg 13577, Level 16, State 1, Line 25    ALTER TABLE SWITCH statement failed on table 'MyDB.dbo.Staging_Department_2015_09_26' because target table has SYSTEM_TIME PERIOD while source table does not have it.`  
  
## <a name="updating-data"></a>Actualización de datos  
 Puede actualizar datos de la tabla actual con una instrucción **UPDATE** habitual. Puede actualizar los datos de la tabla actual desde la de historial para un escenario de error. Pero no puede actualizar columnas **PERIOD** ni datos directamente en la tabla de historial en el caso de que **SYSTEM_VERSIONING = ON**.   
Establezca **SYSTEM_VERSIONING = OFF** y actualice las filas de la tabla actual y de historial, pero tenga en cuenta que así el sistema no conservará un historial de cambios.  
  
### <a name="updating-the-current-table"></a>Actualización de la tabla actual  
 En este ejemplo, se actualiza la columna ManagerID para cada fila donde DeptID tenga el valor 10. No se hace referencia a columnas **PERIOD** de ninguna manera.  
  
```  
UPDATE [dbo].[Department] SET [ManagerID] = 501 WHERE [DeptID] = 10  
```  
  
 Sin embargo, no puede actualizar una columna **PERIOD** ni la tabla de historial.  En este ejemplo, un intento de actualizar una columna **PERIOD** genera un error.  
  
```  
UPDATE [dbo].[Department]    
SET SysStartTime = '2015-09-23 23:48:31.2990175'    
WHERE DeptID = 10 ;  
  
Msg 13537, Level 16, State 1, Line 3   
Cannot update GENERATED ALWAYS columns in table 'TmpDev.dbo.Department'.  
  
```  
  
### <a name="updating-the-current-table-from-the-history-table"></a>Actualización de la tabla actual desde la de historial  
 Puede usar **UPDATE** en la tabla actual para revertir el estado real de la fila a uno válido en un momento dado en el pasado (es decir, a la “última versión válida de la fila conocida”). En el siguiente ejemplo se muestra la reversión a los valores de la tabla de historial a partir de 2015-04-25, donde DeptID tiene valor 10.  
  
```  
UPDATE Department   
SET DeptName = History.DeptName   
FROM Department    
FOR SYSTEM_TIME AS OF '2015-04-25' AS History   
WHERE History.DeptID  = 10   
AND Department.DeptID = 10 ;  
  
```  
  
## <a name="deleting-data"></a>Eliminación de datos  
 Puede eliminar datos en la tabla actual con una instrucción **DELETE** habitual. La columna PERIOD final de las filas eliminadas se rellenará con la hora de inicio de la transacción subyacente.   
No puede eliminar filas directamente de la tabla de historial en el caso de que **SYSTEM_VERSIONING = ON**.   
Establezca **SYSTEM_VERSIONING = OFF** y elimine las filas de la tabla actual y de historial, pero tenga en cuenta que así el sistema no conservará el historial de cambios.   
Las instrucciones**TRUNCATE**, **SWITCH PARTITION OUT** para la tabla actual y la instrucción **SWITCH PARTITION IN** para la tabla del historial no se admiten si **SYSTEM_VERSIONING = ON**.  
  
## <a name="using-merge-to-modify-data-in-temporal-table"></a>Uso de MERGE para modificar los datos de la tabla temporal  
 La operación**MERGE** se admite con las mismas limitaciones que tienen las instrucciones **INSERT** y **UPDATE** en lo relativo a las columnas **PERIOD** .  
  
```  
CREATE TABLE DepartmentStaging (DeptId INT, DeptName varchar(50));   
GO   
INSERT INTO DepartmentStaging VALUES (1, 'Company Management');   
INSERT INTO DepartmentStaging VALUES (10, 'Science & Research');   
INSERT INTO DepartmentStaging VALUES (15, 'Process Management');   
  
MERGE dbo.Department AS target   
USING (SELECT DeptId, DeptName FROM DepartmentStaging) AS source (DeptId, DeptName)   
ON (target.DeptId = source.DeptId)   
WHEN MATCHED THEN    
    UPDATE   
   SET DeptName = source.DeptName   
WHEN NOT MATCHED THEN   
   INSERT (DeptName)   
   VALUES (source.DeptName);  
  
```  
  
## <a name="see-also"></a>Ver también  
 [Tablas temporales](../../relational-databases/tables/temporal-tables.md)   
 [Creación de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [Consulta de los datos de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)   
 [Cambiar el esquema de una tabla temporal con control de versiones del sistema](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [Detención del control de versiones en una tabla temporal con control de versiones](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  
