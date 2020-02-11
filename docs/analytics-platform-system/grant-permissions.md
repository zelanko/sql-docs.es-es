---
title: Conceder permisos de T-SQL
description: Conceda permisos de T-SQL para operaciones de base de datos en almacenamiento de datos paralelos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401149"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>Conceder permisos de T-SQL para almacenamiento de datos paralelos
Conceda permisos de T-SQL para operaciones de base de datos en almacenamiento de datos paralelos.

## <a name="grant-permissions-to-submit-database-queries"></a>Conceder permisos para enviar consultas de base de datos
En esta sección se describe cómo conceder permisos a los roles de base de datos y a los usuarios para consultar datos en el dispositivo PDW de SQL Server.  
  
Las instrucciones usadas para conceder permisos a los datos de consulta dependen del ámbito de acceso deseado. Las siguientes instrucciones SQL crean un inicio de sesión denominado KimAbercrombie que puede tener acceso al dispositivo, crear un usuario de base de datos denominado KimAbercrombie en la base de datos **AdventureWorksPDW2012** , crear un rol de base de datos denominado PDWQueryData, agregar el uso KimAbercrombie al rol PDWQueryData y, después, Mostrar opciones para conceder el acceso a las consultas, en función de si el acceso se concede en el objeto o en el  
  
```sql  
USE master;  
GO  
  
CREATE LOGIN KimAbercrombie WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
USE AdventureWorksPDW2012;  
GO  
  
CREATE USER KimAbercrombie;  
GO  
  
CREATE ROLE PDWQueryData;  
GO  
  
EXEC sp_addrolemember 'PDWQueryData', 'KimAbercrombie'  
GO  
  
-- If the permission is granted against a table or view only, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO PDWQueryData;  
GO  
  
-- If the permission is granted for the database, use this syntax:  
GRANT SELECT ON DATABASE::AdventureWorksPDW2012 TO PDWQueryData;  
GO  
  
-- If KimAbercrombie is the only user that needs to access a table, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO KimAbercrombie;  
GO  
```  
  
## <a name="grant-permissions-to-use-the-admin-console"></a>Conceder permisos para usar la consola de administración
En esta sección se describe cómo conceder permisos a los inicios de sesión de para usar la consola de administración de.  
  
**Usar la consola de administración**  
  
Para usar la consola de administración, un inicio de sesión requiere el permiso servidor **View Server State** . La siguiente instrucción SQL concede el permiso **View Server State** al inicio de `KimAbercrombie` sesión para que Kim pueda usar la consola de administración para supervisar el dispositivo PDW de SQL Server.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**Kill Sessions**  
  
Para conceder a un inicio de sesión el permiso para eliminar sesiones, conceda el permiso **ALTER any Connection** como se indica a continuación:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>Conceder permisos para cargar datos
En esta sección se describe cómo conceder permisos a los roles de base de datos y a los usuarios de base de datos para cargar datos en el SQL Server PDWappliance.  
  
En el siguiente script se muestran los permisos necesarios para cada opción de carga. Puede modificarlo para satisfacer sus necesidades específicas.  
  
```sql  
-- Create server login for the examples that follow.  
USE master;  
CREATE LOGIN BI_ETLUser WITH PASSWORD = '******';  
  
--Grant BULK Load permissions   
GRANT ADMINISTER BULK OPERATIONS TO BI_ETLUser;  
  
--Grant Staging database permissions  
USE stagedb;  
CREATE USER BI_ETLUser for login BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
EXEC sp_addrolemember 'db_ddladmin','BI_ETLUser';  
  
-- The CREATE TABLE permission is required for the database hosting the temporary table.  
-- This may be the staging database (if specified) or destination database.   
-- The CREATE permission is not required if loading in fastappend mode.  
GRANT CREATE TABLE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in append or fastappend mode, the INSERT permission is required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
  
-- If loading in reload mode, the INSERT and DELETE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT DELETE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in upsert mode, the INSERT and UPDATE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT UPDATE ON database::stagedb TO BI_ETLUser;  
  
-- Destination DB  
USE tpch_1gb;  
CREATE USER BI_ETLUser FOR LOGIN BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
```  
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>Conceder permisos para Copiar datos fuera del dispositivo
En esta sección se describe cómo conceder permisos a un usuario o a un rol de base de datos para copiar datos fuera de la aplicación PDW de SQL Server.  
  
Para trasladar los datos a otra ubicación, se requiere el permiso **Select** en la tabla que contiene los datos que se van a trasladar.  
  
Si el destino de los datos es otro PDW de SQL Server, el usuario debe tener **CREATE TABLE** permiso en el destino y el permiso **ALTER Schema** en el esquema que contendrá la tabla.  
  
## <a name="grant-permissions-to-manage-databases"></a>Conceder permisos para administrar bases de datos
En esta sección se describe cómo conceder permisos a un usuario de base de datos para administrar una base de datos en el dispositivo PDW de SQL Server.  
  
En algunas situaciones, una compañía asigna un administrador a una base de datos. El administrador controla el acceso que tienen otros inicios de sesión a la base de datos, así como los datos y los objetos de la base de datos. Para administrar todos los objetos, roles y usuarios de una base de datos, conceda al usuario el permiso **control** en la base de datos. La instrucción siguiente concede al usuario `KimAbercrombie`el permiso de **control** en la base de datos **AdventureWorksPDW2012** .  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
Para conceder a un usuario el permiso para controlar todas las bases de datos en el dispositivo, conceda el permiso **ALTER any Database** en la base de datos maestra.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>Conceder permisos para administrar inicios de sesión, usuarios y roles de base de datos
En esta sección se describe cómo conceder permisos para administrar inicios de sesión, usuarios de base de datos y roles de base de datos.  
  
### <a name="PermsAdminConsole"></a>Conceder permisos para administrar inicios de sesión  
**Agregar o administrar inicios de sesión**  
  
Las siguientes instrucciones SQL crean un inicio de sesión denominado KimAbercrombie que puede crear nuevos inicios de sesión mediante la instrucción [Create login](../t-sql/statements/create-login-transact-sql.md) y modificar los inicios de sesión existentes mediante la instrucción [ALTER login](../t-sql/statements/alter-login-transact-sql.md) .  
  
El permiso **ALTER any login** permite crear nuevos inicios de sesión y quitarlos. Una vez que existe un inicio de sesión, el inicio de sesión se puede administrar mediante inicios de sesión con el permiso **ALTER any login** o el permiso **ALTER** en ese inicio de sesión. Un inicio de sesión puede cambiar la contraseña y la base de datos predeterminada para su propio inicio de sesión.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>Conceder permisos para administrar sesiones de inicio de sesión  
Para poder ver todas las sesiones en el servidor, se necesita el permiso **View Server State** . La capacidad de finalizar las sesiones de otros inicios de sesión requiere el permiso **ALTER any Connection** . En el ejemplo siguiente se `KimAbercrombie` usa el inicio de sesión creado anteriormente.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>Conceder permiso para administrar usuarios de base de datos  
La creación y eliminación de usuarios de base de datos requiere el permiso **ALTER any User** . La administración de los usuarios existentes requiere el permiso **ALTER any User** o el permiso **ALTER** en dicho usuario. En el ejemplo siguiente se `KimAbercrombie` usa el inicio de sesión creado anteriormente.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>Conceder el permiso para administrar roles de base de datos  
Crear y quitar roles de base de datos definidos por el usuario requiere el permiso **ALTER any role** . En el ejemplo siguiente se `KimAbercrombie` usa el inicio de sesión y el uso creados anteriormente.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>Gráficos de permisos de inicio de sesión, usuario y rol  
Los gráficos siguientes pueden ser confusos, pero muestran cómo los permisos de palanca más altos (como el CONTROL) incluyen permisos más granulares que se pueden conceder por separado (por ejemplo, ALTER). Se recomienda conceder siempre la menor cantidad de permisos para que alguien complete las tareas necesarias. Para ello, conceda permisos más específicos, en lugar de los permisos de nivel superior.  
  
**Permisos de inicio de sesión:**  
  
![Permisos de inicio de sesión de seguridad de APS](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**Permisos de usuario:**  
  
![Permisos de usuario de seguridad de APS](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**Permisos de rol:**  
  
![Permisos de rol de seguridad de APS](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>Conceder permisos para supervisar el dispositivo
El dispositivo PDW de SQL Server se puede supervisar mediante la consola de administración de o las vistas del sistema de PDW de SQL Server. Los inicios de sesión requieren el permiso **View Server State** en el nivel de servidor para supervisar el dispositivo. Los inicios de sesión requieren el permiso **ALTER any Connection** para finalizar las conexiones mediante la consola de administración de o el comando **Kill** . Para obtener información sobre los permisos necesarios para usar la consola de administración, consulte [conceder permisos para usar la consola de administración &#40;PDW de SQL Server&#41;](#grant-permissions-to-use-the-admin-console).  
  
### <a name="PermsAdminConsole"></a>Conceder permiso para supervisar el dispositivo mediante las vistas del sistema  
Las siguientes instrucciones SQL crean un inicio de `monitor_login` sesión denominado y concede el permiso **View Server State** al `monitor_login` inicio de sesión.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>Conceder permiso para supervisar el dispositivo mediante las vistas del sistema y para finalizar las conexiones  
Las siguientes instrucciones SQL crean un inicio de `monitor_and_terminate_login` sesión denominado y conceden los permisos **View Server State** y **ALTER any Connection** al `monitor_and_terminate_login` inicio de sesión.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
Para crear inicios de sesión de administrador, consulte [roles fijos de servidor](pdw-permissions.md#fixed-server-roles).  
  
## <a name="see-also"></a>Consulte también
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[CREAR USUARIO](../t-sql/statements/create-user-transact-sql.md)  
[CREAR ROL](../t-sql/statements/create-role-transact-sql.md)  
[Cargar](load-overview.md)  
