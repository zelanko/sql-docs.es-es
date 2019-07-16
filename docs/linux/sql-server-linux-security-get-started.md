---
title: Introducción a la seguridad de SQL Server en Linux
description: En este artículo describe las acciones de seguridad típica.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 1e64ce76ef2528c96ecc0206b7a56b31d4c95ef7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019502"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Tutorial para conocer las características de seguridad de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Si es un usuario de Linux que está familiarizado con SQL Server, las tareas siguientes le guiarán a través de algunas de las tareas de seguridad. Estos no son únicos o específica de Linux, pero resulta útil para darle una idea de las áreas para investigar en profundidad. En cada ejemplo, se proporciona un vínculo a la documentación detallada para dicha área.

> [!NOTE]
>  Los ejemplos siguientes usan la **AdventureWorks2014** base de datos de ejemplo. Para obtener instrucciones sobre cómo obtener e instalar esta base de datos de ejemplo, vea [restaurar una base de datos de SQL Server de Windows a Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Crear un inicio de sesión y un usuario de base de datos 

Conceder a otros usuarios acceso a SQL Server mediante la creación de un inicio de sesión en la base de datos maestra mediante el [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) instrucción. Por ejemplo:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  Utilice siempre una contraseña segura en lugar de los asteriscos en el comando anterior.

Los inicios de sesión pueden conectarse a SQL Server y tener acceso (con permisos limitados) a la base de datos maestra. Para conectarse a una base de datos de usuario, un inicio de sesión necesita una identidad correspondiente en el nivel de base de datos, llama a un usuario de base de datos. Los usuarios son específicos de cada base de datos y deben crearse por separado en cada base de datos para concederles acceso. El siguiente ejemplo se desplaza a la base de datos AdventureWorks2014 y, a continuación, usa el [CREATE USER](../t-sql/statements/create-user-transact-sql.md) instrucción para crear un usuario denominado Larry que está asociado con el inicio de sesión denominado Larry. Aunque el inicio de sesión y el usuario están relacionados (asignados entre sí), son objetos diferentes. El inicio de sesión es una entidad de seguridad de nivel de servidor. El usuario es una entidad de seguridad de nivel de base de datos.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- Una cuenta de administrador de SQL Server puede conectarse a cualquier base de datos y puede crear más inicios de sesión y usuarios en cualquier base de datos.  
- Cuando alguien crea una base de datos se convierten en el propietario de la base de datos, que puede conectarse a esa base de datos. Los propietarios de base de datos pueden crear más usuarios.

Más adelante puede autorizar a otros inicios de sesión para crear una más inicios de sesión y les concede la `ALTER ANY LOGIN` permiso. Dentro de una base de datos, puede autorizar a otros usuarios para crear más usuarios y les concede la `ALTER ANY USER` permiso. Por ejemplo:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

Ahora el inicio de sesión Larry puede crear más inicios de sesión y el usuario de Jerry puede crear más usuarios.


## <a name="granting-access-with-least-privileges"></a>Concesión de acceso con privilegios mínimos

Las primeras personas para conectarse a una base de datos de usuario será el administrador y cuentas de propietario de la base de datos. Sin embargo, estos usuarios tienen los permisos disponibles en la base de datos. Se trata de más permisos que debe tener la mayoría de los usuarios. 

Cuando acaba de empezar, puede asignar algunas categorías generales de permisos mediante el uso de los integrados *funciones fijas de base de datos*. Por ejemplo, el `db_datareader` rol fijo de base de datos puede leer todas las tablas de la base de datos, pero no realiza ningún cambio. Conceder la pertenencia a un rol fijo de base de datos mediante el uso de la [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) instrucción. El ejemplo siguiente se agrega el usuario `Jerry` a la `db_datareader` rol fijo de base de datos.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

Para obtener una lista de los roles fijos de base de datos, vea [Roles de nivel de base de datos](../relational-databases/security/authentication-access/database-level-roles.md).

Posteriormente, cuando esté listo para configurar el acceso más preciso a los datos (altamente recomendados), crear sus propios roles de base de datos definido por el usuario mediante [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) instrucción. A continuación, asignarle permisos granulares específicos para roles personalizados.

Por ejemplo, las siguientes instrucciones crean un rol de base de datos denominado `Sales`, concede el `Sales` grupo la capacidad de ver, actualizar y eliminar las filas de la `Orders` de tabla y, a continuación, agrega el usuario `Jerry` a la `Sales` rol.   
   
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
CREAR SalesFilter de directiva de seguridad   
Agregar Security.fn_securitypredicate(SalesPersonID) de predicado de filtro    
  EN Sales.SalesOrderHeader,   
Agregar bloque predicado Security.fn_securitypredicate(SalesPersonID)    
  EN Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
Ejecutar como usuario = 'SalesPerson280';   
Seleccionar * desde Sales.SalesOrderHeader;    
REVERTIR; 
 
Ejecutar como usuario = 'Administrador';   
Seleccionar * desde Sales.SalesOrderHeader;   
REVERTIR;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
ALTER SalesFilter de directiva de seguridad   
CON (ESTADO = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
USAR AdventureWorks2014; Vaya de ALTER TABLE Person.EmailAddress     ALTER columna EmailAddress    
Agregar ENMASCARADO con (función = ' email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
Crear usuario de prueba de usuario sin inicio de sesión;   
GRANT SELECT ON Person.EmailAddress a TestUser;    
 
Ejecutar como usuario = "TestUser";   
Seleccione EmailAddressID, dirección de correo electrónico de Person.EmailAddress;       
REVERTIR;    
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

CREAR CLAVE MAESTRA DE CIFRADO POR CONTRASEÑA = ' ***';  
GO  

Crear certificado MyServerCert con el asunto = 'Mi base de datos clave certificado de cifrado';  
GO  

USAR AdventureWorks2014;   Ir
  
CREATE DATABASE ENCRYPTION KEY  
CON ALGORITMO = AES_256  
CIFRADO de MyServerCert de certificado de servidor;  
GO
  
Modificar base de datos AdventureWorks2014  
ESTABLECER CIFRADO   
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
Patrón de uso;   Vaya   crear certificado BackupEncryptCert   con el asunto = 'Database copias de seguridad';   Ir de la base de datos de copia de seguridad [AdventureWorks2014]   a disco = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
por  
  COMPRESIÓN,  
  ENCRYPTION   
   (  
   ALGORITMO = AES_256,  
   CERTIFICADO de servidor = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
