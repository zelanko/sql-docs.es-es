---
title: ALTER DATABASE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 04/20/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_TSQL
- ALTER DATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- databases [SQL Server], modifying
- ALTER DATABASE statement
- databases [SQL Server], renaming
- renaming databases
- database modifications [SQL Server]
- ALTER DATABASE statement, syntax described
- database names [SQL Server], ALTER DATABASE
- modifying databases
- collations [SQL Server], modifying
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 15f8affd-8f39-4021-b092-0379fc6983da
caps.latest.revision: 282
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 6c498acedd2821127137ec6be1bd2e04e6b3da09
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="alter-database-transact-sql"></a>ALTER DATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica una base de datos o los archivos y grupos de archivos asociados a la base de datos. Agrega o quita archivos y grupos de archivos en una base de datos, cambia los atributos de una base de datos o de sus archivos y grupos de archivos, cambia la intercalación de base de datos y establece las opciones de base de datos. Las instantáneas de base de datos no se pueden modificar. Para modificar opciones de base de datos asociados con la replicación, utilice [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md).  
   
 Debido a su longitud, la sintaxis de ALTER DATABASE se divide en los temas siguientes:  
  
 ALTER DATABASE  
 El tema actual proporciona la sintaxis para cambiar el nombre y la intercalación de una base de datos.  
  
 [MODIFICAR el archivo de base de datos y las opciones de grupo de archivos](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)  
 Proporciona la sintaxis para agregar y eliminar archivos y grupos de archivos de una base de datos y para cambiar los atributos de archivos y grupos de archivos.  
  
 [Opciones de ALTER DATABASE SET](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
 Proporcionan la sintaxis para cambiar los atributos de una base de datos usando las opciones SET de ALTER DATABASE.  
  
 [Base de datos de base de datos de ALTER de creación de reflejo](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)  
 Proporciona la sintaxis de las opciones SET de ALTER DATABASE relacionadas con la creación de reflejo de la base de datos.  
  
 [MODIFICAR BASE DE DATOS SET HADR](../../t-sql/statements/alter-database-transact-sql-set-hadr.md)  
 Proporciona la sintaxis de la [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] opciones de ALTER DATABASE para configurar una base de datos secundaria en una réplica secundaria de un grupo de disponibilidad Always On.  
  
 [Nivel de compatibilidad de ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)  
 Proporciona la sintaxis de las opciones SET de ALTER DATABASE relacionadas con los niveles de compatibilidad de la base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
Base de datos de SQL Azure, consulte [ALTER DATABASE &#40; Base de datos SQL Azure &#41;](../../t-sql/statements/alter-database-azure-sql-database.md)  
Para almacenamiento de datos de SQL Azure, consulte [ALTER DATABASE &#40; Almacenamiento de datos SQL de Azure &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
Para almacenamiento de datos paralelos, vea [ALTER DATABASE &#40; Almacenamiento de datos en paralelo &#41; ](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- SQL Server Syntax  
ALTER DATABASE { database_name  | CURRENT }  
{  
    MODIFY NAME = new_database_name   
  | COLLATE collation_name  
  | <file_and_filegroup_options>  
  | <set_database_options>  
}  
[;]  
  
<file_and_filegroup_options >::=  
  <add_or_modify_files>::=  
  <filespec>::=   
  <add_or_modify_filegroups>::=  
  <filegroup_updatability_option>::=  
  
<set_database_options>::=  
  <optionspec>::=   
  <auto_option> ::=   
  <change_tracking_option> ::=  
  <cursor_option> ::=   
  <database_mirroring_option> ::=   
  <date_correlation_optimization_option> ::=  
  <db_encryption_option> ::=  
  <db_state_option> ::=  
  <db_update_option> ::=  
  <db_user_access_option> ::=  <delayed_durability_option> ::=  <external_access_option> ::=  
  <FILESTREAM_options> ::=  
  <HADR_options> ::=    
  <parameterization_option> ::=  
  <query_store_options> ::=  
  <recovery_option> ::=   
  <service_broker_option> ::=  
  <snapshot_option> ::=  
  <sql_option> ::=   
  <termination> ::=  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Es el nombre de la base de datos que se va a modificar.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 CURRENT  
 **Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Designa que la base de datos actual en uso se debe modificar.  
  
 MODIFY NAME  **=**  *new_database_name*  
 Cambia el nombre de la base de datos con el nombre especificado como *new_database_name*.  
  
 COLLATE *collation_name*  
 Especifica la intercalación de la base de datos. *collation_name* puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Si no se especifica, se asigna a la base de datos la intercalación de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Al crear bases de datos con una intercalación diferente de la predeterminada, los datos de la base de datos siempre respetan la intercalación especificada. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], al crear una base de datos independiente, la información de catálogo interno se mantiene mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predeterminado de intercalación, **Latin1_General_100_CI_AS_WS_KS_SC**.  
  
 Para obtener más información acerca de los nombres de intercalación de Windows y SQL, consulte [COLLATE &#40; Transact-SQL &#41; ](~/t-sql/statements/collations.md).  
  
 **\<delayed_durability_option >:: =**  
 **Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para obtener más información consulte [ALTER DATABASE SET Options &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md) y [controlar la durabilidad](../../relational-databases/logs/control-transaction-durability.md).  
  
 **\<file_and_filegroup_options >:: =**  
 Para obtener más información, vea [modificar el archivo de base de datos y opciones de grupo de archivos &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).  
  
## <a name="remarks"></a>Comentarios  
 Para quitar una base de datos, use [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md).  
  
 Para reducir el tamaño de una base de datos, utilice [DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md).  
  
 La instrucción ALTER DATABASE se debe ejecutar en el modo de confirmación automática (modo de administración de transacciones predeterminado) y no se permite en una transacción explícita o implícita.  
  
 El estado de un archivo de base de datos (por ejemplo, en línea o sin conexión) se mantiene con independencia del estado de la base de datos. Para obtener más información, consulte [Estados de los archivos](../../relational-databases/databases/file-states.md). El estado de los archivos de un grupo de archivos determina la disponibilidad de todo el grupo de archivos. Para que un grupo de archivos esté disponible, todos los archivos del grupo de archivos deben estar en línea. Si un grupo de archivos se encuentra en modo sin conexión, todos los intentos de acceso al grupo de archivos por parte de una instrucción SQL generan un error. Al generar un plan de consulta para las instrucciones SELECT, el optimizador de consultas evita los índices no clúster y las vistas indizadas que residen en los grupos de archivos sin conexión. Esto permite que las instrucciones se ejecuten correctamente. No obstante, si el grupo de archivos sin conexión contiene el montón o el índice clúster de la tabla de destino, las instrucciones SELECT no funcionarán. Adicionalmente, cualquier instrucción INSERT, UPDATE o DELETE que modifique una tabla con cualquier índice en un grupo de archivos sin conexión no funcionará.  
  
 Si una base de datos se encuentra en estado RESTORING, se producirán errores en la mayoría de las instrucciones ALTER DATABASE. La excepción es el establecimiento de opciones de creación de reflejo de la base de datos. Es posible que una base de datos se encuentre en estado RESTORING durante una operación de restauración activa o cuando se produce un error en una operación de restauración de una base de datos o de un archivo de registro, debido a un archivo de copia de seguridad dañado.  
  
 La memoria caché de planes para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se borra si se establece alguna de las opciones siguientes.  
  
|||  
|-|-|  
|OFFLINE|READ_WRITE|  
|ONLINE|MODIFY FILEGROUP DEFAULT|  
|MODIFY_NAME|MODIFY FILEGROUP READ_WRITE|  
|COLLATE|MODIFY FILEGROUP READ_ONLY|  
|READ_ONLY|PAGE_VERIFY|  
  
 Al borrar la memoria caché de planes, se provoca una nueva compilación de todos los planes de ejecución posteriores y puede ocasionar una disminución repentina y temporal del rendimiento de las consultas. Para cada almacén de caché borrado de la memoria caché de planes, el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contendrá el siguiente mensaje informativo: "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha detectado %d instancias de vaciado del almacén de caché '%s' (parte de la memoria caché de planes) debido a determinadas operaciones de mantenimiento de base de datos o reconfiguración". Este mensaje se registra cada cinco minutos siempre que se vacíe la memoria caché dentro de ese intervalo de tiempo.  
  
 La memoria caché de procedimientos también se vacía en los escenarios siguientes:  
  
-   Una base de datos tiene la opción de base de datos AUTO_CLOSE establecida en ON. Cuando ninguna conexión de usuario hace referencia a la base de datos ni la usa, la tarea de segundo plano intenta cerrar la base de datos y apagarla de modo automático.  
  
-   Ejecuta varias consultas con una base de datos que tiene opciones predeterminadas. Después, la base de datos se quita.  
  
-   Se quita una instantánea de base de datos para una base de datos de origen.  
  
-   Volvió a generar correctamente el registro de transacciones para una base de datos.  
  
-   Restaura una copia de seguridad de una base de datos  
  
-   Separa una base de datos.  
  
## <a name="changing-the-database-collation"></a>Cambiar la intercalación de la base de datos  
 Antes de aplicar otra intercalación a una base de datos, asegúrese de que se cumplen las siguientes condiciones:  
  
-   Es el único usuario que utiliza actualmente la base de datos.  
  
-   Ningún objeto enlazado a un esquema depende de la intercalación de la base de datos.  
  
     Si los objetos siguientes, que dependen de la intercalación de base de datos, existen en la base de datos, la instrucción ALTER DATABASE*database_name*instrucción COLLATE producirá un error. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolverá un mensaje de error para cada objeto que bloquee la acción de ALTER:  
  
    -   Vistas y funciones definidas por el usuario creadas con SCHEMABINDING  
  
    -   Columnas calculadas  
  
    -   Restricciones CHECK  
  
    -   Funciones con valores de tabla que devuelven tablas con columnas de caracteres con intercalaciones heredadas de la intercalación predeterminada de la base de datos  
  
     La información de dependencia de las entidades no vinculadas a esquemas se actualiza automáticamente si se cambia la intercalación de la base de datos.  
  
 Cambiar la intercalación de la base de datos no crea duplicados entre los nombres del sistema para los objetos de base de datos. Si se producen nombres duplicados en la intercalación cambiada, los siguientes espacios de nombres pueden provocar errores en el cambio de la intercalación de la base de datos:  
  
-   Nombres de objetos, como un procedimiento, una tabla, un desencadenador o una vista  
  
-   Nombres de esquemas.  
  
-   Entidades de seguridad, como un grupo, rol o usuario  
  
-   Nombres de tipo escalar, como los tipos definidos por el usuario y por el sistema  
  
-   Nombres de catálogos de texto completo  
  
-   Nombres de columnas o parámetros en un objeto  
  
-   Nombres de índices en una tabla  
  
Los nombres duplicados resultantes de la nueva intercalación provocarán que la acción de cambio no se ejecute correctamente y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolverá un mensaje de error que especifica el espacio de nombres donde se ha encontrado el duplicado.  
  
## <a name="viewing-database-information"></a>Ver la información de la base de datos  
 Se pueden utilizar vistas de catálogo, funciones del sistema y procedimientos almacenados del sistema para devolver información sobre bases de datos, archivos y grupos de archivos.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER en la base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-name-of-a-database"></a>A. Cambiar el nombre de una base de datos  
 En el ejemplo siguiente se cambia el nombre de la base de datos `AdventureWorks2012` a `Northwind`.  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
### <a name="b-changing-the-collation-of-a-database"></a>B. Cambiar la intercalación de una base de datos  
 En el siguiente ejemplo se crea una base de datos denominada `testdb` con la intercalación `SQL_Latin1_General_CP1_CI_A`S, y luego se cambia la intercalación de la base de datos `testdb` a `COLLATE French_CI_AI`.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE master;  
GO  
  
CREATE DATABASE testdb  
COLLATE SQL_Latin1_General_CP1_CI_AS ;  
GO  
  
ALTER DATABASE testDB  
COLLATE French_CI_AI ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
- [ALTER DATABASE &#40; Base de datos SQL Azure &#41;](alter-database-azure-sql-database.md)  
- [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
- [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
- [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
- [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
- [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
- [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
- [sp_spaceused &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
- [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
- [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
- [Sys.database_mirroring_witnesses &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
- [Sys.data_spaces &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
- [Sys.FileGroups &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
- [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)   
- [Bases de datos del sistema](../../relational-databases/databases/system-databases.md)  
  

