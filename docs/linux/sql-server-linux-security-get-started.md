---
title: Introducción a la seguridad de SQL Server en Linux
description: En este artículo se describen las acciones de seguridad habituales.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 1e64ce76ef2528c96ecc0206b7a56b31d4c95ef7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68019502"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Tutorial sobre las características de seguridad de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Si es usuario de Linux y no está familiarizado con SQL Server, las secciones siguientes le guiarán por algunas tareas de seguridad. No son exclusivas ni específicas de Linux, pero le ayudarán a hacerse una idea de las áreas en las que puede profundizar. En los ejemplos se proporciona un vínculo a documentación detallada de cada área.

> [!NOTE]
>  En los siguientes ejemplos, se usa la base de datos de ejemplo **AdventureWorks2014**. Para consultar las instrucciones sobre cómo obtener e instalar esta base de datos de ejemplo, vea [Restaurar una base de datos de SQL Server de Windows a Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Creación de un inicio de sesión y un usuario de base de datos 

Conceda acceso a SQL Server a otros usuarios mediante la creación de un inicio de sesión en la base de datos maestra con la instrucción [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md). Por ejemplo:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  Use siempre una contraseña segura en lugar de los asteriscos del comando anterior.

Los inicios de sesión pueden conectarse a SQL Server y tener acceso (con permisos limitados) a la base de datos maestra. Para conectarse a una base de datos de usuario, un inicio de sesión necesita una identidad correspondiente en el nivel de base de datos, denominado usuario de base de datos. Los usuarios son específicos de cada base de datos y se deben crear por separado en cada base de datos para concederles acceso. En el ejemplo siguiente se usa la base de datos AdventureWorks2014 y, luego, se aplica la instrucción [CREATE USER](../t-sql/statements/create-user-transact-sql.md) para crear un usuario denominado Larry que está asociado con el inicio de sesión "Larry". Aunque el inicio de sesión y el usuario están relacionados (asignados entre sí), son objetos diferentes. El inicio de sesión es una entidad de seguridad de nivel de servidor. El usuario es una entidad de seguridad de nivel de base de datos.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- Una cuenta de administrador de SQL Server puede conectarse a cualquier base de datos y crear más inicios de sesión y usuarios.  
- Cuando alguien crea una base de datos, se convierte en su propietario, por lo que puede conectarse a esa base de datos. Los propietarios de bases de datos pueden crear más usuarios.

Posteriormente, se puede autorizar a otros inicios de sesión para que creen más inicios de sesión mediante la concesión del permiso `ALTER ANY LOGIN`. En una base de datos, se puede autorizar a otros usuarios para que creen más usuarios mediante la concesión del permiso `ALTER ANY USER`. Por ejemplo:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

Ahora, el inicio de sesión "Larry" puede crear más inicios de sesión y el usuario "Jerry" puede crear más usuarios.


## <a name="granting-access-with-least-privileges"></a>Concesión de acceso con privilegios mínimos

Las primeras personas que se conecten a una base de datos de usuario serán las cuentas de administrador y de propietario de la base de datos. Estos usuarios tienen todos los permisos disponibles en la base de datos, que son más de los que debería tener la mayoría de los usuarios. 

Si acaba de empezar, puede asignar algunas categorías generales de permisos mediante los *roles fijos de base de datos* integrados. Por ejemplo, el rol fijo de base de datos `db_datareader` puede leer todas las tablas de la base de datos, pero no realizar cambios. Para conceder la pertenencia a un rol fijo de base de datos, use la instrucción [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md). En el ejemplo siguiente se agrega el usuario `Jerry` al rol fijo de base de datos `db_datareader`.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

Para obtener una lista con los roles fijos de base de datos, vea [Roles de nivel de base de datos](../relational-databases/security/authentication-access/database-level-roles.md).

Más adelante, cuando esté listo para configurar un acceso más preciso a los datos (lo que se recomienda encarecidamente), puede crear sus propios roles de base de datos definidos por el usuario mediante la instrucción [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md). Después, asigne permisos pormenorizados específicos a los roles personalizados.

Por ejemplo, las siguientes instrucciones crean un rol de base de datos denominado `Sales`, conceden al grupo `Sales` la capacidad de ver, actualizar y eliminar filas de la tabla `Orders` y, después, agregan el usuario `Jerry` al rol `Sales`.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

For more information about the permission system, see [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## Configure row-level security  

[Row-Level Security](../relational-databases/security/row-level-security.md) enables you to restrict access to rows in a database based on the user executing a query. This feature is useful for scenarios like ensuring that customers can only access their own data or that workers can only access data that is pertinent to their department.   

The following steps walk through setting up two Users with different row-level access to the `Sales.SalesOrderHeader` table. 

Create two user accounts to test the row level security:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Grant read access on the `Sales.SalesOrderHeader` table to both users:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Create a new schema and inline table-valued function. The function returns 1 when a row in the `SalesPersonID` column matches the ID of a `SalesPerson` login or if the user executing the query is the Manager user.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```   

Create a security policy adding the function as both a filter and a block predicate on the table:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
USE AdventureWorks2014; GO ALTER TABLE Person.EmailAddress     ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Verify that the masking function changes the email address in the first record from:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## Enable Transparent Data Encryption

One threat to your database is the risk that someone will steal the database files off of your hard-drive. This could happen with an intrusion that gets elevated access to your system, through the actions of a problem employee, or by theft of the computer containing the files (such as a laptop).

Transparent Data Encryption (TDE) encrypts the data files as they are stored on the hard drive. The master database of the SQL Server database engine has the encryption key, so that the database engine can manipulate the data. The database files cannot be read without access to the key. High-level administrators can manage, backup, and recreate the key, so the database can be moved, but only by selected people. When TDE is configured, the `tempdb` database is also automatically encrypted. 

Since the Database Engine can read the data, Transparent Data Encryption does not protect against unauthorized access by administrators of the computer who can directly read memory, or access SQL Server through an administrator account.

### Configure TDE

- Create a master key
- Create or obtain a certificate protected by the master key
- Create a database encryption key and protect it by the certificate
- Set the database to use encryption

Configuring TDE requires `CONTROL` permission on the master database and `CONTROL` permission on the user database. Typically an administrator configures TDE. 

The following example illustrates encrypting and decrypting the `AdventureWorks2014` database using a certificate installed on the server named `MyServerCert`.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;   GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

To remove TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

The encryption and decryption operations are scheduled on background threads by SQL Server. You can view the status of these operations using the catalog views and dynamic management views in the list that appears later in this topic.   

> [!WARNING]
>  Backup files of databases that have TDE enabled are also encrypted by using the database encryption key. As a result, when you restore these backups, the certificate protecting the database encryption key must be available. This means that in addition to backing up the database, you have to make sure that you maintain backups of the server certificates to prevent data loss. Data loss will result if the certificate is no longer available. For more information, see [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

For more information about TDE, see [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## Configure backup encryption
SQL Server has the ability to encrypt the data while creating a backup. By specifying the encryption algorithm and the encryptor (a certificate or asymmetric key) when creating a backup, you can create an encrypted backup file.    
  
> [!WARNING]  
>  It is very important to back up the certificate or asymmetric key, and preferably to a different location than the backup file it was used to encrypt. Without the certificate or asymmetric key, you cannot restore the backup, rendering the backup file unusable. 
 
 
The following example creates a certificate, and then creates a backup protected by the certificate.
```
USE master;   GO   CREATE CERTIFICATE BackupEncryptCert   WITH SUBJECT = 'Database backups';   GO BACKUP DATABASE [AdventureWorks2014]   TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
WITH  
  COMPRESSION,  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
