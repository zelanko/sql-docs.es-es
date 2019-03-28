---
title: Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup compression [SQL Server], Resource Governor
- backup compression [SQL Server], CPU usage
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- Resource Governor, backup compression
ms.assetid: 01796551-578d-4425-9b9e-d87210f7ba72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5fcd3d72ef3e716cd640d35505b82df459eb37b7
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531457"
---
# <a name="use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql"></a>Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad (Transact-SQL)
  De forma predeterminada, la copia de seguridad con compresión aumenta significativamente el uso de CPU, y la CPU adicional consumida por el proceso de compresión puede afectar adversamente a las operaciones simultáneas. Por consiguiente, podría querer crear una copia de seguridad comprimida de prioridad baja en una sesión en la que el uso de CPU esté limitado por el[regulador de recursos](../resource-governor/resource-governor.md) cuando se produce la contención por la CPU. En este tema se presenta un escenario en el que se clasifican las sesiones de un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determinado asignándolas a un grupo de cargas de trabajo del regulador de recursos que limita el uso de CPU en tales casos.  
  
> [!IMPORTANT]  
>  En un escenario determinado en el que se use el regulador de recursos, la clasificación de la sesión podría basarse en un nombre de usuario, un nombre de aplicación u otra característica que pueda diferenciar una conexión. Para obtener más información, consulte [Resource Governor Classifier Function](../resource-governor/resource-governor-classifier-function.md) y [Resource Governor Workload Group](../resource-governor/resource-governor-workload-group.md).  
  
##  <a name="Top"></a> Este tema contiene el conjunto siguiente de escenarios, que se presentan en secuencia:  
  
1.  [Configurar un inicio de sesión y un usuario para operaciones de prioridad baja](#setup_login_and_user)  
  
2.  [Configurar el regulador de recursos para limitar el uso de CPU](#configure_RG)  
  
3.  [Comprobar la clasificación de la sesión actual (Transact-SQL)](#verifying)  
  
4.  [Comprimir las copias de seguridad utilizando una sesión con CPU limitada](#creating_compressed_backup)  
  
##  <a name="setup_login_and_user"></a> Configurar un inicio de sesión y un usuario para operaciones de prioridad baja  
 El escenario de este tema requiere un usuario y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de prioridad baja. El nombre de usuario se utilizará para clasificar las sesiones que se ejecutan en el inicio de sesión y enrutarlas a un grupo de cargas de trabajo del regulador de recursos que limita el uso de CPU.  
  
 En el procedimiento siguiente se describen los pasos para configurar un inicio de sesión y un usuario con este propósito, además de un ejemplo de [!INCLUDE[tsql](../../includes/tsql-md.md)], "Ejemplo A: Configurar un inicio de sesión y un usuario (Transact-SQL)".  
  
### <a name="to-set-up-a-login-and-database-user-for-classifying-sessions"></a>Para configurar un inicio de sesión y un usuario de la base de datos para clasificar las sesiones  
  
1.  Cree un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para crear copias de seguridad comprimidas de prioridad baja.  
  
     **Para crear un inicio de sesión**  
  
    -   [Crear un inicio de sesión](../security/authentication-access/create-a-login.md)  
  
    -   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
2.  Si lo desea, puede conceder el permiso VIEW SERVER STATE a este inicio de sesión.  
  
    -   [Permisos de objeto de sistema GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-system-object-permissions-transact-sql)  
  
     Para obtener más información, vea [Permisos de entidad de seguridad de base de datos GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-principal-permissions-transact-sql).  
  
3.  Cree un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para este inicio de sesión.  
  
     **Para crear un usuario**  
  
    -   [Crear un usuario de base de datos](../security/authentication-access/create-a-database-user.md)  
  
    -   [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
4.  Para que las sesiones de este inicio de sesión y este usuario puedan realizar una copia de seguridad de una base de datos determinada, agregue el usuario al rol de base de datos db_backupoperator de esa base de datos. Haga esto con cada base de datos de la que este usuario vaya a hacer una copia de seguridad. Si lo desea, puede agregar el usuario a los demás roles fijos de base de datos.  
  
     **Para agregar un usuario a un rol fijo de base de datos**  
  
    -   [sp_addrolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql)  
  
     Para obtener más información, vea [Permisos de entidad de seguridad de base de datos GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-principal-permissions-transact-sql).  
  
### <a name="example-a-setting-up-a-login-and-user-transact-sql"></a>Ejemplo A: Configurar un inicio de sesión y un usuario (Transact-SQL)  
 El ejemplo siguiente solo es pertinente si decide crear un usuario y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nuevos para las copias de seguridad de prioridad baja. Por otro lado, puede usar un inicio de sesión y un usuario existentes, si hay alguno adecuado.  
  
> [!IMPORTANT]  
>  En el ejemplo siguiente se usa un inicio de sesión y un nombre de usuario de ejemplo, *nombre_de_dominio*`\MAX_CPU`. Reemplácelos por los nombres del usuario y el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que piensa usar al crear las copias de seguridad comprimidas de prioridad baja.  
  
 En este ejemplo se crea un inicio de sesión para la cuenta de Windows *nombre_de_dominio*`\MAX_CPU` y, después, se concede el permiso VIEW SERVER STATE al inicio de sesión. Este permiso permite comprobar la clasificación que hace el regulador de recursos de las sesiones del inicio de sesión. Después, en el ejemplo se crea un usuario para *nombre_de_dominio*`\MAX_CPU` y se agrega al rol fijo de base de datos db_backupoperator para la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . La función clasificadora del regulador de recursos usará este nombre de usuario.  
  
```sql  
-- Create a SQL Server login for low-priority operations  
USE master;  
CREATE LOGIN [domain_name\MAX_CPU] FROM WINDOWS;  
GRANT VIEW SERVER STATE TO [domain_name\MAX_CPU];  
GO  
-- Create a SQL Server user in AdventureWorks2012 for this login  
USE AdventureWorks2012;  
CREATE USER [domain_name\MAX_CPU] FOR LOGIN [domain_name\MAX_CPU];  
EXEC sp_addrolemember 'db_backupoperator', 'domain_name\MAX_CPU';  
GO  
  
```  
  
 [&#91;Principio&#93;](#Top)  
  
##  <a name="configure_RG"></a> Configurar el regulador de recursos para limitar el uso de CPU  
  
> [!NOTE]  
>  Asegúrese de que el regulador de recursos está habilitado. Para obtener más información, vea [Habilitar el regulador de recursos](../resource-governor/enable-resource-governor.md).  
  
 En este escenario en el que se usa el regulador de recursos, la configuración comprende los pasos básicos siguientes:  
  
1.  Cree y configure un grupo de recursos de servidor del regulador de recursos que limite el ancho de banda máximo medio de CPU que se concederá a las solicitudes en el grupo de recursos de servidor cuando se produzca la contención por la CPU.  
  
2.  Cree y configure un grupo de cargas de trabajo del regulador de recursos que utiliza este grupo.  
  
3.  Cree una *función clasificadora*; se trata de una función definida por el usuario (UDF) que devuelve unos valores que el regulador de recursos usa para clasificar las sesiones de modo que se enruten al grupo de cargas de trabajo adecuado.  
  
4.  Registre la función clasificadora con el regulador de recursos.  
  
5.  Aplique los cambios a la configuración en memoria del regulador de recursos.  
  
> [!NOTE]  
>  Para obtener información sobre los grupos de recursos de servidor del regulador de recursos, los grupos de cargas de trabajo y la clasificación, vea [Regulador de recursos](../resource-governor/resource-governor.md).  
  
 Las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] para estos pasos se describen en el procedimiento "Para configurar el regulador de recursos de modo que se limite el uso de CPU”. Después, se muestra un ejemplo de [!INCLUDE[tsql](../../includes/tsql-md.md)] del procedimiento.  
  
 **Para configurar el regulador de recursos (SQL Server Management Studio)**  
  
-   [Configurar el regulador de recursos utilizando una plantilla](../resource-governor/configure-resource-governor-using-a-template.md)  
  
-   [Crear un grupo de recursos de servidor](../resource-governor/create-a-resource-pool.md)  
  
-   [Crear un grupo de cargas de trabajo](../resource-governor/create-a-workload-group.md)  
  
### <a name="to-configure-resource-governor-for-limiting-cpu-usage-transact-sql"></a>Para configurar el regulador de recursos de modo que se limite el uso de CPU (Transact-SQL)  
  
1.  Emita una instrucción [CREATE RESOURCE POOL](/sql/t-sql/statements/create-resource-pool-transact-sql) para crear un grupo de recursos de servidor. En el ejemplo de este procedimiento se utiliza la sintaxis siguiente:  
  
     *CREATE RESOURCE POOL pool_name* WITH ( MAX_CPU_PERCENT = *value* );  
  
     *Value* es un número entero comprendido entre 1 y 100 que indica el porcentaje máximo medio de ancho banda de CPU. El valor adecuado depende del entorno. A efectos de ilustración, en el ejemplo de este tema se utiliza un porcentaje del 20% (MAX_CPU_PERCENT = 20.)  
  
2.  Emita una instrucción [CREATE WORKLOAD GROUP](/sql/t-sql/statements/create-workload-group-transact-sql) para crear un grupo de cargas de trabajo para las operaciones de prioridad baja cuyo uso de CPU quiera regular. En el ejemplo de este procedimiento se utiliza la sintaxis siguiente:  
  
     CREATE WORKLOAD GROUP *group_name* USING *pool_name*;  
  
3.  Emita una instrucción [CREATE FUNCTION](/sql/t-sql/statements/create-function-transact-sql) para crear una función clasificadora que asigne el grupo de cargas de trabajo creado en el paso anterior al usuario del inicio de sesión de prioridad baja. En el ejemplo de este procedimiento se utiliza la sintaxis siguiente:  
  
     CREATE FUNCTION [*schema_name*.]*function_name*() RETURNS sysname  
  
     WITH SCHEMABINDING  
  
     AS  
  
     BEGIN  
  
     DECLARE @workload_group_name AS *sysname*  
  
     IF (SUSER_NAME() = '*user_of_low_priority_login*')  
  
     SET @workload_group_name = '*workload_group_name*'  
  
     RETURN @workload_group_name  
  
     END  
  
     Para obtener información sobre los componentes de esta instrucción CREATE FUNCTION, vea:  
  
    -   [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)  
  
    -   [SUSER_SNAME &#40;Transact-SQL&#41;](/sql/t-sql/functions/suser-sname-transact-sql)  
  
        > [!IMPORTANT]  
        >  SUSER_NAME es solo una de las diversas funciones del sistema que se pueden utilizar en una función clasificadora. Para obtener más información, vea [Crear y probar una función clasificadora definida por el usuario](../resource-governor/create-and-test-a-classifier-user-defined-function.md).  
  
    -   [SET @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/set-local-variable-transact-sql).  
  
4.  Emita una instrucción [ALTER RESOURCE GOVERNOR](/sql/t-sql/statements/alter-resource-governor-transact-sql) para registrar la función clasificadora con el regulador de recursos. En el ejemplo de este procedimiento se utiliza la sintaxis siguiente:  
  
     ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = *schema_name*.*function_name*);  
  
5.  Emita una segunda instrucción ALTER RESOURCE GOVERNOR para aplicar los cambios a la configuración en memoria del regulador de recursos de la siguiente manera:  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    ```  
  
### <a name="example-b-configuring-resource-governor-transact-sql"></a>Ejemplo B: Configurar Resource Governor (Transact-SQL)  
 En el ejemplo siguiente se realizan los pasos dentro de una única transacción:  
  
1.  Crea el grupo de recursos de servidor `pMAX_CPU_PERCENT_20` .  
  
2.  Crea el grupo de cargas de trabajo `gMAX_CPU_PERCENT_20` .  
  
3.  Crea la función clasificadora `rgclassifier_MAX_CPU()` , que utiliza el nombre de usuario creado en el ejemplo anterior.  
  
4.  Registra la función clasificadora con el regulador de recursos.  
  
 Después de confirmar la transacción, el ejemplo aplica los cambios de configuración solicitados en las instrucciones ALTER WORKLOAD GROUP o ALTER RESOURCE POOL.  
  
> [!IMPORTANT]  
>  En el ejemplo siguiente se usa el nombre de usuario del usuario de ejemplo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creado en "Ejemplo A: Configurar un inicio de sesión y un usuario (Transact-SQL)", *nombre_de_dominio*`\MAX_CPU`. Reemplace esto por el nombre del usuario del inicio de sesión que piensa usar para crear copias de seguridad comprimidas de prioridad baja.  
  
```sql  
-- Configure Resource Governor.  
BEGIN TRAN  
USE master;  
-- Create a resource pool that sets the MAX_CPU_PERCENT to 20%.   
CREATE RESOURCE POOL pMAX_CPU_PERCENT_20  
   WITH  
      (MAX_CPU_PERCENT = 20);  
GO  
-- Create a workload group to use this pool.   
CREATE WORKLOAD GROUP gMAX_CPU_PERCENT_20  
USING pMAX_CPU_PERCENT_20;  
GO  
-- Create a classification function.  
-- Note that any request that does not get classified goes into   
-- the 'Default' group.  
CREATE FUNCTION dbo.rgclassifier_MAX_CPU() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
    DECLARE @workload_group_name AS sysname  
      IF (SUSER_NAME() = 'domain_name\MAX_CPU')  
          SET @workload_group_name = 'gMAX_CPU_PERCENT_20'  
    RETURN @workload_group_name  
END;  
GO  
  
-- Register the classifier function with Resource Governor.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION= dbo.rgclassifier_MAX_CPU);  
COMMIT TRAN;  
GO  
-- Start Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
 [&#91;Principio&#93;](#Top)  
  
##  <a name="verifying"></a> Comprobar la clasificación de la sesión actual (Transact-SQL)  
 Si lo desea, inicie sesión como el usuario que especificó en la función clasificadora y compruebe la clasificación de la sesión emitiendo la instrucción [SELECT](/sql/t-sql/queries/select-transact-sql) siguiente en el Explorador de objetos:  
  
```sql  
USE master;  
SELECT sess.session_id, sess.login_name, sess.group_id, grps.name   
FROM sys.dm_exec_sessions AS sess   
JOIN sys.dm_resource_governor_workload_groups AS grps   
    ON sess.group_id = grps.group_id  
WHERE session_id > 50;  
GO  
```  
  
 En el panel de resultados, la columna **name** debe enumerar una o varias sesiones para el nombre del grupo de cargas de trabajo que especificó en la función clasificadora.  
  
> [!NOTE]  
>  Para obtener información sobre las vistas de administración dinámica invocadas por esta instrucción SELECT, vea [sys.dm_exec_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql) y [sys.dm_resource_governor_workload_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql).  
  
 [&#91;Principio&#93;](#Top)  
  
##  <a name="creating_compressed_backup"></a> Comprimir las copias de seguridad utilizando una sesión con CPU limitada  
 Para crear una copia de seguridad comprimida en una sesión con el uso máximo de CPU limitado, inicie sesión como el usuario especificado en la función clasificadora. En el comando de copia de seguridad, especifique WITH COMPRESSION ([!INCLUDE[tsql](../../includes/tsql-md.md)]) o seleccione **Comprimir copia de seguridad** ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]). Para crear una copia de seguridad comprimida de la base de datos, vea [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md).  
  
### <a name="example-c-creating-a-compressed-backup-transact-sql"></a>Ejemplo C: Crear una copia de seguridad comprimida (Transact-SQL)  
 En el ejemplo [BACKUP](/sql/t-sql/statements/backup-transact-sql) siguiente se crea una copia de seguridad completa comprimida de la base de datos [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] en un archivo de copia de seguridad al que se ha dado formato recientemente, `Z:\SQLServerBackups\AdvWorksData.bak`.  
  
```sql  
--Run backup statement in the gBackup session.  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   MEDIADESCRIPTION='AdventureWorks2012 Compressed Data Backups'  
   DESCRIPTION='First database backup on AdventureWorks2012 Compressed Data Backups media set'  
   COMPRESSION;  
GO  
```  
  
 [&#91;Principio&#93;](#Top)  
  
## <a name="see-also"></a>Vea también  
 [Crear y probar una función clasificadora definida por el usuario](../resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [regulador de recursos](../resource-governor/resource-governor.md)  
  
  
