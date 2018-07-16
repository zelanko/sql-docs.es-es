---
title: Habilitar y deshabilitar la captura de datos modificados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- change data capture [SQL Server], enabling databases
- change data capture [SQL Server], disabling databases
- change data capture [SQL Server], disabling tables
ms.assetid: b741894f-d267-4b10-adfe-cbc14aa6caeb
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e96cb5bb777544b8a3a390eee59a16e0213c857f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37309515"
---
# <a name="enable-and-disable-change-data-capture-sql-server"></a>Habilitar y deshabilitar la captura de datos modificados (SQL Server)
  Este tema describe cómo habilitar y deshabilitar la captura de datos modificados para una tabla y una base de datos.  
  
## <a name="enable-change-data-capture-for-a-database"></a>Habilitar la captura de datos modificados en una base de datos  
 Para que pueda crearse una instancia de captura para tablas individuales, es preciso que un miembro del rol fijo de servidor `sysadmin` habilite previamente la base de datos para la captura de datos modificados. Esto se hace ejecutando el procedimiento almacenado [sys.sp_cdc_enable_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql) en el contexto de la base de datos. Para determinar si una base de datos ya está habilitada, consulte la columna `is_cdc_enabled` en la vista de catálogo `sys.databases`.  
  
 Cuando una base de datos está habilitada para la captura de datos modificados, la `cdc` esquema, `cdc` usuario, las tablas de metadatos y otros objetos del sistema se crean para la base de datos. El `cdc` esquema contiene las tablas de metadatos de captura de datos de cambio y, después de las tablas de origen están habilitadas para la captura de datos modificados, las tablas de cambios individuales que sirven como repositorio para los datos modificados. El `cdc` esquema también contiene las funciones de sistema asociadas que se usan para consultar los datos modificados.  
  
 La captura de datos modificados requiere el uso exclusivo del esquema `cdc` y del usuario `cdc`. Si en una base de datos existe un esquema o un usuario de base de datos denominado *cdc* , dicha base de datos no se puede habilitar para la captura de datos modificados hasta que el esquema y/o el usuario se quiten o se cambie su nombre.  
  
 Vea la plantilla Habilitar una base de datos para la captura de datos modificados si desea obtener un ejemplo de cómo habilitar una base de datos.  
  
> [!IMPORTANT]  
>  Para buscar las plantillas en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vaya a **Ver**, haga clic en **Explorador de plantillas**y, a continuación, seleccione **Plantillas de SQL Server**. **Captura de datos modificados** es una subcarpeta. Bajo esta carpeta, encontrará todas las plantillas a las que se hace referencia en este tema. También existe un icono **Explorador de plantillas** en la barra de herramientas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
```tsql  
-- ====  
-- Enable Database for CDC template   
-- ====  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_db  
GO  
```  
  
## <a name="disable-change-data-capture-for-a-database"></a>Deshabilitar la captura de datos modificados para una base de datos  
 Un miembro de la `sysadmin` rol fijo de servidor puede ejecutar el procedimiento almacenado [sys.sp_cdc_disable_db &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql) en el contexto de base de datos para deshabilitar la captura de datos modificados para una base de datos. No es necesario deshabilitar tablas individuales antes de deshabilitar la base de datos. Cuando se deshabilita la base de datos quitan todos los metadatos de captura de datos modificados asociados, incluidos el `cdc` trabajos de captura de usuario y esquema y los datos modificados. Sin embargo, los roles de acceso creados por la captura de datos modificados no se quitarán automáticamente y se deben eliminar explícitamente. Para determinar si una base de datos está habilitada, consulte la columna `is_cdc_enabled` en la vista de catálogo sys.databases.  
  
 Si se quita una base de datos habilitada para la captura de datos modificados, se quitarán automáticamente los trabajos de captura de datos modificados.  
  
 Vea la plantilla Deshabilitar una base de datos para la captura de datos modificados si desea obtener un ejemplo de deshabilitación de una base de datos.  
  
> [!IMPORTANT]  
>  Para buscar las plantillas en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vaya a **Ver**, haga clic en **Explorador de plantillas**y, a continuación, haga clic en **Plantillas de SQL Server**. **Captura de datos modificados** es una subcarpeta donde se pueden buscar todas las plantillas a las que se hace referencia en este tema. También existe un icono **Explorador de plantillas** en la barra de herramientas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
```tsql  
-- =======  
-- Disable Database for Change Data Capture template   
-- =======  
USE MyDB  
GO  
EXEC sys.sp_cdc_disable_db  
GO  
```  
  
## <a name="enable-change-data-capture-for-a-table"></a>Habilitar la captura de datos modificados para una tabla  
 Después de una base de datos se habilitó para la captura de datos modificados, los miembros de la `db_owner` rol fijo de base de datos puede crear una instancia de captura para tablas de origen individuales mediante el procedimiento almacenado `sys.sp_cdc_enable_table`. Para determinar si una tabla de origen se ha habilitado ya para la captura de datos modificados, examine la columna is_tracked_by_cdc en la vista de catálogo `sys.tables`.  
  
 Se pueden especificar las opciones siguientes al crear una instancia de captura:  
  
 `Columns in the source table to be captured`.  
  
 De forma predeterminada, todas las columnas de la tabla de origen se identifican como columnas capturadas. Si solo es necesario realizar el seguimiento de un subconjunto de las columnas, por ejemplo, por motivos de privacidad o de rendimiento, use el parámetro *@captured_column_list* para especificar el subconjunto de columnas.  
  
 `A filegroup to contain the change table.`  
  
 De forma predeterminada, la tabla de cambios se encuentra en el grupo de archivos predeterminado de la base de datos. Los propietarios de base de datos que quieran controlar la ubicación de las tablas de cambios individuales pueden usar el parámetro *@filegroup_name* para especificar un grupo de archivos determinado para la tabla de cambios asociada a la instancia de captura. El grupo de archivos con nombre debe existir previamente. Generalmente, se recomienda que las tablas de cambios se coloquen en un grupo de archivos independiente de las tablas de origen. Consulte la `Enable a Table Specifying Filegroup Option` plantilla para obtener un ejemplo que muestra el uso de la *@filegroup_name* parámetro.  
  
```tsql  
-- =========  
-- Enable a Table Specifying Filegroup Option Template  
-- =========  
USE MyDB  
GO  
  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = N'MyRole',  
@filegroup_name = N'MyDB_CT',  
@supports_net_changes = 1  
GO  
```  
  
 `A role for controlling access to a change table.`  
  
 La finalidad del rol con nombre es controlar el acceso a los datos de cambios. El rol especificado puede ser un rol fijo de servidor existente o un rol de base de datos. Si el rol especificado aún no existe, se crea automáticamente un rol de base de datos con ese nombre. Los miembros del rol `sysadmin` o `db_owner` tienen acceso total a los datos de las tablas de cambios. Los demás usuarios deben tener el permiso SELECT en todas las columnas capturadas de la tabla de origen. Además, cuando se especifica un rol, los usuarios que no sean miembros del `sysadmin` o `db_owner` rol también debe ser miembros del rol especificado.  
  
 Si prefiere no usar un rol de acceso, debe establecer explícitamente el valor NULL en el parámetro *@role_name* . Vea la plantilla `Enable a Table Without Using a Gating Role` para obtener un ejemplo de cómo habilitar una tabla sin un rol de acceso.  
  
```tsql  
-- =========  
-- Enable a Table Without Using a Gating Role template   
-- =========  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = NULL,  
@supports_net_changes = 1  
GO  
  
```  
  
 `A function to query for net changes.`  
  
 Una instancia de captura siempre incluirá una función con valores de tabla para devolver todas las entradas de la tabla de cambios que se produjeron dentro de un intervalo definido. Esta función se denomina anexando el nombre de la instancia de captura a "cdc.fn_cdc_get_all_changes_". Para obtener más información, vea [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql).  
  
 Si el parámetro *@supports_net_changes* está establecido en 1, también se genera una función net changes para la instancia de captura. Esta función devuelve solo un cambio por cada fila distinta que haya cambiado en el intervalo especificado en la llamada. Para obtener más información, vea [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql).  
  
 Para poder usar las consultas net changes, la tabla de origen debe tener una clave principal o un índice único que identifique las filas de forma única. Si se usa un índice único, el nombre del índice se debe especificar con el parámetro *@index_name* . Las columnas definidas en la clave principal o índice único deben estar incluidas en la lista de columnas de origen que se van a capturar.  
  
 Vea la plantilla `Enable a Table for All and Net Changes Queries` para obtener un ejemplo que muestre la creación de una instancia de captura con ambas funciones de consulta.  
  
```tsql  
-- =============  
-- Enable a Table for All and Net Changes Queries template   
-- =============  
USE MyDB  
GO  
EXEC sys.sp_cdc_enable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@role_name     = N'MyRole',  
@supports_net_changes = 1  
GO  
```  
  
> [!NOTE]  
>  Si la captura de datos modificados está habilitada en una tabla con una clave principal existente y el parámetro *@index_name* no se usa para identificar un índice único alternativo, la característica de captura de datos modificados usará la clave principal. Los cambios subsiguientes en la clave principal no se permitirán sin deshabilitar primero la captura de datos modificados para la tabla. Esto es así independientemente de si se solicitó compatibilidad con las consultas net changes cuando se configuró la captura de datos modificados. Si no hay ninguna clave principal en una tabla en el momento en que se habilita para la captura de datos modificados, la captura de datos modificados omite la incorporación posterior de una clave principal. Dado que la captura de datos modificados no utilizará ninguna clave principal que se cree una vez habilitada la tabla, las columnas de clave y la clave se pueden quitar sin restricciones.  
  
## <a name="disable-change-data-capture-for-a-table"></a>Deshabilitar la captura de datos modificados para una tabla  
 Los miembros de la `db_owner` rol fijo de base de datos puede quitar una instancia de captura para tablas de origen individuales mediante el procedimiento almacenado `sys.sp_cdc_disable_table`. Para determinar si una tabla de origen está habilitada actualmente para la captura de datos modificados, examine la columna `is_tracked_by_cdc` en la vista de catálogo `sys.tables`. Si no hay ninguna tabla habilitada para la base de datos después de que tenga lugar la deshabilitación, también se quitarán los trabajos de captura de datos modificados.  
  
 Si quita una tabla habilitada para la captura de datos modificados, se quitarán automáticamente los metadatos de la captura de datos modificados que están asociados a la tabla.  
  
 Vea la plantilla Deshabilitar una instancia de captura para una tabla si desea obtener un ejemplo de deshabilitación de una tabla.  
  
```tsql  
-- =====  
-- Disable a Capture Instance for a Table template   
-- =====  
USE MyDB  
GO  
EXEC sys.sp_cdc_disable_table  
@source_schema = N'dbo',  
@source_name   = N'MyTable',  
@capture_instance = N'dbo_MyTable'  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](track-data-changes-sql-server.md)   
 [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../track-changes/about-change-data-capture-sql-server.md)   
 [Trabajar con datos modificados &#40;SQL Server&#41;](work-with-change-data-sql-server.md)   
 [Administrar y supervisar la captura de datos modificados &#40;SQL Server&#41;](../track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
