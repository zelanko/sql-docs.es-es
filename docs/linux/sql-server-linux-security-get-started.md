---
title: "Introducción a la seguridad de SQL Server en Linux | Documentos de Microsoft"
description: "En este tema se describe las acciones de seguridad típica."
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 254df7047188570cbf766efb29b486d77d095a98
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>Tutorial sobre las características de seguridad de SQL Server en Linux

Si es un usuario de Linux que es una novedad de SQL Server, las tareas siguientes le guiarán por algunas de las tareas de seguridad. Estos no son únicas o específicas de Linux, pero es conveniente tener una idea de las áreas para investigar en profundidad. En cada ejemplo se proporciona un vínculo a la documentación detallada para dicha área.

>  [!NOTE]
>  Los ejemplos siguientes usan el **AdventureWorks2014** base de datos de ejemplo. Para obtener instrucciones sobre cómo obtener e instalar esta base de datos de ejemplo, vea [restaurar una base de datos de SQL Server de Windows en Linux](sql-server-linux-migrate-restore-database.md).


## <a name="create-a-login-and-a-database-user"></a>Crear un inicio de sesión y un usuario de base de datos 

Conceder a otros usuarios acceso a SQL Server mediante la creación de un inicio de sesión en la base de datos maestra utilizando la [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) instrucción. Por ejemplo:

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

>  [!NOTE]
>  Utilice siempre una contraseña segura en lugar de los asteriscos anteriores.

Los inicios de sesión pueden conectarse a SQL Server y tener acceso (con permisos limitados) a la base de datos maestra. Para conectarse a una base de datos de usuario, un inicio de sesión necesita una identidad correspondiente en el nivel de base de datos, llama a un usuario de base de datos. Los usuarios son específicos de cada base de datos y se deben crear por separado en cada base de datos para concederles acceso. El siguiente ejemplo se desplaza a la base de datos AdventureWorks2014 y, a continuación, usa el [CREATE USER](../t-sql/statements/create-user-transact-sql.md) instrucción para crear un usuario denominado Larry que está asociado con el inicio de sesión denominado Larry. Aunque el inicio de sesión y el usuario están relacionadas (asignados entre sí), son objetos diferentes. El inicio de sesión es una entidad de seguridad de nivel de servidor. El usuario es una entidad de seguridad de nivel de base de datos.

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- Una cuenta de administrador de SQL Server puede conectarse a cualquier base de datos y puede crear más inicios de sesión y usuarios en cualquier base de datos.  
- Cuando un usuario crea una base de datos se convierten en el propietario de la base de datos, que puede conectarse a esa base de datos. Los propietarios de base de datos pueden crear más usuarios.

Más adelante puede autorizar a otros inicios de sesión para crear una más inicios de sesión y les concede el `ALTER ANY LOGIN` permiso. Dentro de una base de datos, se pueden autorizar a otros usuarios para crear más usuarios concediéndoles el `ALTER ANY USER` permiso. Por ejemplo:   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

Ahora el inicio de sesión Juan puede crear más inicios de sesión y el usuario Juan puede crear más usuarios.


## <a name="granting-access-with-least-privileges"></a>Conceder acceso con privilegios mínimos

Las primeras personas para conectarse a una base de datos de usuario será el administrador y las cuentas de propietario de base de datos. Sin embargo, estos usuarios tienen todos los los permisos disponibles en la base de datos. Se trata de más permisos que debe tener la mayoría de los usuarios. 

Cuando acaba de empezar, puede asignar algunos categorías generales de permisos mediante la integrada *funciones fijas de base de datos*. Por ejemplo, el `db_datareader` rol fijo de base de datos puede leer todas las tablas de la base de datos, pero no realizar ningún cambio. Conceder la pertenencia a un rol fijo de base de datos mediante el uso de la [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md) instrucción. En el ejemplo siguiente se agrega el usuario `Jerry` a la `db_datareader` rol fijo de base de datos.   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

Para obtener una lista de los roles fijos de base de datos, vea [Roles de nivel de base de datos](../relational-databases/security/authentication-access/database-level-roles.md).

Más adelante, cuando esté listo para configurar el acceso más preciso a los datos (altamente recomendados), crear sus propios roles de base de datos definido por el usuario mediante [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md) instrucción. A continuación, asignarle permisos granulares específicos para roles personalizados.

Por ejemplo, las siguientes instrucciones crean un rol de base de datos denominado `Sales`, concede el `Sales` grupo la capacidad de ver, actualizar y eliminar filas de la `Orders` de tabla y, a continuación, agrega el usuario `Jerry` a la `Sales` rol.   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

Para obtener más información sobre el sistema de permisos, consulte [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## <a name="configure-row-level-security"></a>Configurar la seguridad de nivel de fila  

[Seguridad de nivel de fila](../relational-databases/security/row-level-security.md) le permite restringir el acceso a las filas de una base de datos en función de usuario que ejecuta una consulta. Esta característica es útil para escenarios como asegurarse de que los clientes solo pueden tener acceso a sus propios datos o que los trabajadores solo puedan acceder a datos que son pertinentes para su departamento.   

Los pasos siguientes tutorial configurar dos usuarios con diferentes acceso a nivel de fila el `Sales.SalesOrderHeader` tabla. 

Cree dos cuentas de usuario para probar la seguridad de nivel de fila:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Conceder acceso de lectura en el `Sales.SalesOrderHeader` tabla para ambos usuarios:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Crear un nuevo esquema y funciones en línea con valores de tabla. La función devuelve 1 cuando una fila en la `SalesPersonID` columna coincide con el identificador de un `SalesPerson` inicio de sesión o si el usuario que ejecuta la consulta es el usuario administrador.   
   
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

Crear una directiva de seguridad agregando la función como un filtro y un predicado de bloqueo en la tabla:  

```
CREATE SECURITY POLICY SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader,   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  ON Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Ejecute lo siguiente para consultar el `SalesOrderHeader` como cada usuario de la tabla. Compruebe que `SalesPerson280` ve únicamente las 95 filas desde sus propias ventas y que la `Manager` puede ver todas las filas de la tabla.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
REVERT; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
REVERT;   
```
 
Modifique la directiva de seguridad para deshabilitar la directiva.  Ahora ambos usuarios pueden acceder a todas las filas. 

```
ALTER SECURITY POLICY SalesFilter   
WITH (STATE = OFF);    
``` 


## <a name="enable-dynamic-data-masking"></a>Habilitar el enmascaramiento dinámico de datos

[Enmascaramiento de datos dinámicos](../relational-databases/security/dynamic-data-masking.md) le permite limitar la exposición de datos confidenciales a los usuarios de una aplicación total o parcialmente enmascarando determinadas columnas. 

Use un `ALTER TABLE` instrucción que se va a agregar a la función de enmascaramiento del `EmailAddress` columna en el `Person.EmailAddress` tabla: 
 
```
USE AdventureWorks2014;
GO
ALTER TABLE Person.EmailAddress    
ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Crear un nuevo usuario `TestUser` con `SELECT` permiso en la tabla, a continuación, ejecute una consulta como `TestUser` para ver los datos enmascarados:   

```  
CREATE USER TestUser WITHOUT LOGIN;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
REVERT;    
```
 
Compruebe que la función de enmascaramiento cambia la dirección de correo electrónico en el primer registro de:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## <a name="enable-transparent-data-encryption"></a>Habilitar el cifrado de datos transparente

Una amenaza para la base de datos es el riesgo de que alguien robar los archivos de base de datos en el disco duro. Esto podría suceder con una intrusión que obtiene acceso con privilegios elevados en el sistema, a través de las acciones de un empleado de problema o robo del equipo que contiene los archivos (por ejemplo, un equipo portátil).

Cifrado de datos transparente (TDE) cifra los archivos de datos a medida que se almacenan en el disco duro. La base de datos maestra del motor de base de datos de SQL Server tiene la clave de cifrado, por lo que el motor de base de datos puede tratar los datos. No se puede leer los archivos de base de datos sin acceso a la clave. Los administradores de alto nivel pueden administrar, copia de seguridad y vuelva a crear la clave, por lo que se puede mover la base de datos, sino solo a los usuarios seleccionados. Cuando se configura TDE, la `tempdb` base de datos se cifra también automáticamente. 

Puesto que el motor de base de datos puede leer los datos, el cifrado de datos transparente no protege frente a accesos no autorizados por los administradores del equipo que se puede leer la memoria, o directamente acceso a SQL Server a través de una cuenta de administrador.

### <a name="configure-tde"></a>Configurar TDE

- Cree una clave maestra
- Cree u obtenga un certificado protegido por la clave maestra
- Cree una clave de cifrado de base de datos y protéjala con el certificado
- Configure la base de datos para que utilice el cifrado

Configurar TDE requiere `CONTROL` permiso en la base de datos maestra y `CONTROL` permiso en la base de datos de usuario. Normalmente, un administrador configura TDE. 

En el ejemplo siguiente se muestra cómo cifrar y descifrar la base de datos `AdventureWorks2014` mediante un certificado instalado en el servidor denominado `MyServerCert`.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;  
GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
SET ENCRYPTION ON;   
```

Para quitar TDE, ejecute`ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

El programa de las operaciones de cifrado y descifrado se ejecutan en subprocesos en segundo plano, con SQL Server. Puede ver el estado de estas operaciones mediante las vistas de catálogo y las vistas de administración dinámica de la lista que se muestra más adelante en este tema.   

>  [!WARNING]
>  Los archivos de copia de seguridad de las bases de datos que tienen habilitado TDE también se cifran mediante la clave de cifrado de la base de datos. Como consecuencia, al restaurar estas copias de seguridad debe estar disponible el certificado que protege la clave de cifrado de la base de datos. Esto significa que, además de hacer copias de seguridad de la base de datos, tiene que asegurarse de que mantiene copias de seguridad de los certificados del servidor para evitar la pérdida de datos. Si el certificado deja de estar disponible, perderá los datos. Para obtener más información, consulte [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

Para obtener más información acerca de TDE, vea [cifrado de datos transparente (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## <a name="configure-backup-encryption"></a>Configurar el cifrado de copia de seguridad
SQL Server tiene la capacidad de cifrar los datos mientras crea una copia de seguridad. Al especificar el algoritmo de cifrado y el sistema de cifrado (un certificado o clave asimétrica) al crear una copia de seguridad, puede crear un archivo de copia de seguridad cifrado.    
  
> [!WARNING]  
>  Es muy importante realizar una copia de seguridad del certificado o la clave asimétrica, y preferiblemente en una ubicación diferente de la que se usó para cifrar el archivo de copia de seguridad. Sin el certificado o la clave asimétrica, no puede restaurar la copia de seguridad, lo que deja inutilizable el archivo de copia de seguridad. 
 
 
En el ejemplo siguiente se crea un certificado y, a continuación, crea una copia de seguridad protegida por el certificado.
```
USE master;  
GO  
CREATE CERTIFICATE BackupEncryptCert   
   WITH SUBJECT = 'Database backups';  
GO 
BACKUP DATABASE [AdventureWorks2014]  
TO DISK = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
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

Para obtener más información, consulte [cifrado de copia de seguridad](../relational-databases/backup-restore/backup-encryption.md).


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de las características de seguridad de SQL Server, vea [centro de seguridad para el motor de base de datos de SQL Server y base de datos de SQL Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

