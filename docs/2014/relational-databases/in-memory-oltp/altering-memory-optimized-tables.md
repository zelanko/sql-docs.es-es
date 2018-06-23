---
title: Modificar tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: f40638174ebd432a96ce61ea27805ea77fd5a151
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114050"
---
# <a name="altering-memory-optimized-tables"></a>Modificar tablas con optimización para memoria
  No se admite la realización de operaciones ALTER en las tablas optimizadas para memoria. Esto incluye operaciones tales como cambiar el bucket_count, agregar o quitar un índice y agregar o quitar una columna. En este tema se proporcionan instrucciones sobre cómo actualizar las tablas optimizadas para memoria.  
  
## <a name="updating-the-definition-of-a-memory-optimized-table"></a>Actualizar la definición de una tabla con optimización para memoria  
 Para actualizar la definición de una tabla optimizada para memoria es necesario crear una nueva tabla con la definición de tabla actualizada, copiar los datos en la nueva tabla y comenzar a usarla. A menos que la tabla sea de solo lectura, esto requiere detener la carga de trabajo en la tabla, para asegurarse de que no se realiza ningún cambio en la tabla mientras se realiza la copia de datos.  
  
 En el procedimiento siguiente se describen los pasos necesarios para actualizar una tabla. En este ejemplo, la actualización agrega un índice. Este procedimiento conserva el nombre de la tabla y requiere dos operaciones de copia de datos: una en la tabla temporal y otra en la nueva tabla. El cambio del bucket_count de un índice, así como la adición o eliminación de una columna, se realizan de la misma manera.  
  
1.  Detenga la carga de trabajo en la tabla.  
  
2.  Genere el script para la tabla y agregue el nuevo índice al script.  
  
3.  Genere el script para los objetos enlazados al esquema (principalmente procedimientos almacenados compilados de forma nativa) que hacen referencia a T y a sus permisos.  
  
     Para encontrar los objetos enlazados al esquema que hacen referencia a la tabla, utilice la consulta siguiente:  
  
    ```tsql  
    declare @t nvarchar(255) = N'<table name>'  
  
    select r.referencing_schema_name, r.referencing_entity_name  
    from sys.dm_sql_referencing_entities (@t, 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
    where r.is_caller_dependent = 0 and m.is_schema_bound=1;  
    ```  
  
     Los permisos de un procedimiento almacenado pueden incluirse en scripts mediante el [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente:  
  
    ```tsql  
    declare @sp nvarchar(255) = N'<procedure name>'  
    declare @permissions nvarchar(max) = N''  
  
    select @permissions += dp.state_desc + N' ' + dp.permission_name + N' ON ' +   
       quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) + N' TO ' +  
       quotename(u.name) + N'; ' + char(13)  
    from sys.database_permissions as dp  
  
    join sys.database_principals as u  
       on u.principal_id = dp.grantee_principal_id  
  
    join sys.objects as o  
       on o.object_id = dp.major_id  
    where dp.class = 1 /* object */  
       and dp.minor_id = 0 and o.object_id=object_id(@sp);  
  
    select @permissions  
    ```  
  
4.  Cree una copia de la tabla y copie los datos de la tabla original en ella. La copia se puede crear usando los siguientes [!INCLUDE[tsql](../../includes/tsql-md.md)] <sup>1</sup>.  
  
    ```tsql  
    select * into dbo.T_copy from dbo.T  
    ```  
  
     Si no hay suficiente memoria disponible, `T_copy` puede ser una tabla con optimización para memoria, lo que hace que los datos más rápida de copiar.<sup> 2</sup>  
  
5.  Quite los objetos enlazados al esquema que hacen referencia a la tabla original.  
  
6.  Quite la tabla original.  
  
7.  Cree la nueva tabla (`T`) con el script que contiene el nuevo índice.  
  
8.  Copie los datos de `T_copy` en `T`.  
  
9. Vuelva a crear los objetos enlazados al esquema que hacen la referencia a la tabla y aplique los permisos.  
  
10. Inicie la carga de trabajo en `T`.  
  
 <sup>1</sup> tenga en cuenta que `T_copy` se conserva en el disco en este ejemplo. Si hay una copia de seguridad de `T` disponible, `T_copy` puede ser una tabla temporal o no perdurable.  
  
 <sup>2</sup> debe haber suficiente memoria para `T_copy`. La memoria no se libera inmediatamente en `DROP TABLE`. Si `T_copy` está con optimización para memoria, debe haber suficiente memoria para dos copias adicionales de `T`. Si `T_copy` está basada en disco, basta con que haya memoria suficiente para una copia adicional de `T`, debido a que el recolector de elementos no utilizados necesita ponerse al día después de anular la versión anterior de `T`.  
  
## <a name="changing-schema-powershell"></a>Cambiar el esquema (PowerShell)  
 Los scripts de PowerShell siguientes elaboran y generan cambios en el esquema aplicando el script a la tabla y los permisos asociados.  
  
 Uso: prepare_schema_change.ps1 *nombre_servidor ** db_name`schema_name`table_name*  
  
 Este script toma como argumento una tabla, e incluye el objeto y sus permisos, así como los objetos enlazados al esquema que hacen la referencia y sus permisos en la carpeta actual. Se generan un total de 7 scripts para actualizar el esquema de la tabla de entrada:  
  
-   Copie los datos en una tabla temporal (un montón).  
  
-   Quite los objetos enlazados al esquema que hacen referencia a la tabla.  
  
-   Quite la tabla.  
  
-   Vuelva a crear la tabla con el nuevo esquema y aplique de nuevo los permisos.  
  
-   Copie los datos de la tabla temporal en la tabla recién creada.  
  
-   Vuelva a crear los objetos enlazados al esquema que hacen referencia a la tabla y sus permisos.  
  
-   Quite la tabla temporal.  
  
 El script para el paso 4 debe actualizarse para reflejar los cambios deseados en el esquema. Si hay algún cambio en las columnas de la tabla, las secuencias de comandos para los pasos 5 (copiar los datos de tabla temporal) y 6 (volver a crear los procedimientos almacenados) deben actualizarse según sea necesario.  
  
```tsql  
# Prepare for schema changes by scripting out the table, as well as associated permissions  
# --------  
# Usage: prepare_schema_change.ps1 server_name db_name schema_name table_name  
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage prepare_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
$object_heap = "$object$(Get-Random)"  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | out-null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$scripter = New-Object ("Microsoft.SqlServer.Management.SMO.Scripter") ($server)  
  
## initialize table variable  
$tableUrn = $server.Databases[$database].Tables[$object, $schema]  
if($tableUrn.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
## initialize scripting object  
$scriptingOptions = New-Object ("Microsoft.SqlServer.Management.SMO.ScriptingOptions")   
$scriptingOptions.Permissions = $True  
$scriptingOptions.ScriptDrops = $True  
  
$scripter.Options = $scriptingOptions;  
  
write-host "(1) Scripting SELECT INTO $object_heap for table [$object] to 1_copy_to_heap_for_$schema`_$object.sql"  
Echo "SELECT * INTO $schema.$object_heap FROM $schema.$object WITH (SNAPSHOT)" | Out-File "1_copy_to_heap_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
write-host "(2) Scripting DROP for procs schema-bound to [$object] 2_drop_procs_$schema`_$object.sql"  
## query referencing schema-bound objects  
$dt = $server.Databases[$database].ExecuteWithResults("select r.referencing_schema_name, r.referencing_entity_name  
from sys.dm_sql_referencing_entities ('$schema.$object', 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
where r.is_caller_dependent = 0 and m.is_schema_bound=1;")  
  
## initialize out file  
Echo "" | Out-File "2_drop_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
Foreach ($t in $dt.Tables)  
{    
   Foreach ($r in $t.Rows)  
   {    
      ## script object   
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      $scripter.Script($so) | Out-File -Append "2_drop_procs_$schema`_$object.sql"  
   }  
}  
write-host "--done--"  
write-host ""  
  
write-host "(3) Scripting DROP table for [$object] to 3_drop_table_$schema`_$object.sql"  
$scripter.Script($tableUrn) | Out-File "3_drop_table_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
## now script creates  
$scriptingOptions.ScriptDrops = $False  
  
write-host "(4) Scripting CREATE table and permissions for [$object] to !please_edit_4_create_table_$schema`_$object.sql"  
write-host "***** rename this script to 4_create_table.sql after completing the updates to the schema"  
$scripter.Script($tableUrn) | Out-File "!please_edit_4_create_table_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
write-host "(5) Scripting INSERT INTO table from heap and UPDATE STATISTICS for [$object] to 5_copy_from_heap_$schema`_$object.sql"  
write-host "[update this script if columns are added to or removed from the table]"  
Echo "INSERT INTO [$schema].[$object] SELECT * FROM [$schema].[$object_heap]; UPDATE STATISTICS [$schema].[$object] WITH FULLSCAN, NORECOMPUTE" | Out-File "5_copy_from_heap_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
write-host "(6) Scripting CREATE PROC and permissions for procedures schema-bound to [$object] to 6_create_procs_$schema`_$object.sql"  
write-host "[update the procedure definitions if columns are renamed or removed]"  
## initialize out file  
Echo "" | Out-File "6_create_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
Foreach ($t in $dt.Tables)  
{    
   Foreach ($r in $t.Rows)  
   {    
      ## script the schema-bound object  
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      foreach($s in $scripter.Script($so))  
        {  
            Echo $s | Out-File -Append "6_create_procs_$schema`_$object.sql"  
            Echo "GO" | Out-File -Append "6_create_procs_$schema`_$object.sql"  
        }  
   }  
}  
write-host "--done--"  
write-host ""  
  
write-host "(7) Scripting DROP $object_heap to 7_drop_heap_$schema`_$object.sql"  
Echo "DROP TABLE $schema.$object_heap" | Out-File "7_drop_heap_$schema`_$object.sql";  
write-host "--done--"  
write-host ""  
  
```  
  
 El script de PowerShell siguiente ejecuta los cambios del esquema incluidos en el script del ejemplo anterior. Este script toma como argumento una tabla, y ejecuta los scripts de cambio de esquema que se generaron para dicha tabla y los procedimientos almacenados asociados.  
  
 Uso: execute_schema_change.ps1 *nombre_servidor ** db_name`schema_name`table_name*  
  
```tsql  
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage execute_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | out-null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$database = $server.Databases[$database]  
$table = $database.Tables[$object, $schema]  
if($table.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
$1 = Get-Item "1_copy_to_heap_$schema`_$object.sql"  
$2 = Get-Item "2_drop_procs_$schema`_$object.sql"  
$3 = Get-Item "3_drop_table_$schema`_$object.sql"  
$4 = Get-Item "4_create_table_$schema`_$object.sql"  
$5 = Get-Item "5_copy_from_heap_$schema`_$object.sql"  
$6 = Get-Item "6_create_procs_$schema`_$object.sql"  
$7 = Get-Item "7_drop_heap_$schema`_$object.sql"  
  
write-host "(1) Running SELECT INTO heap for table [$object] from 1_copy_to_heap_for_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $1.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(2) Running DROP for procs schema-bound from [$object] 2_drop_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $2.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(3) Running DROP table for [$object] to 4_drop_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $3.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(4) Running CREATE table and permissions for [$object] from 4_create_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $4.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(5) Running INSERT INTO table from heap for [$object] and UPDATE STATISTICS from 5_copy_from_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $5.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(6) Running CREATE PROC and permissions for procedures schema-bound to [$object] from 6_create_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $6.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
  
write-host "(7) Running DROP heap from 7_drop_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $7.OpenText().ReadToEnd())")  
write-host "--done--"  
write-host ""  
```  
  
## <a name="see-also"></a>Vea también  
 [Tablas con optimización para memoria](memory-optimized-tables.md)  
  
  