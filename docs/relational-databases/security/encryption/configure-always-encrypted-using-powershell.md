---
title: "Configure Always Encrypted using PowerShell (Configurar Always Encrypted con PowerShell) | Microsoft Docs"
ms.custom: ""
ms.date: "09/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-security"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 12f2bde5-e100-41fa-b474-2d2332fc7650
caps.latest.revision: 15
author: "stevestein"
ms.author: "sstein"
manager: "jhubbard"
caps.handback.revision: 13
---
# Configure Always Encrypted using PowerShell (Configurar Always Encrypted con PowerShell)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

En el módulo SqlServer PowerShell se proporcionan cmdlets para configurar [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) en Azure SQL Database y SQL Server 2016.

La mayoría de los cmdlets para Always Encrypted del módulo SqlServer funcionan con claves de Always Encrypted o información confidencial almacenadas en columnas cifradas, por lo que es importante que ejecute los cmdlets en un equipo seguro. Cuando administre Always Encrypted, ejecute los cmdlets en un equipo diferente del que hospeda la instancia de SQL Server. 

Dado que el objetivo principal de Always Encrypted es garantizar la seguridad de la información confidencial cifrada, incluso si el sistema de base de datos está en peligro, la ejecución de un script de PowerShell que procese las claves o la información confidencial en el equipo de SQL Server puede reducir o anular las ventajas de la característica. Para obtener más recomendaciones relacionadas con la seguridad, vea [Security Considerations for Key Management](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement) (Consideraciones de seguridad para la administración de claves).

Los vínculos a los artículos de cmdlet están al [final de esta página](#aecmdletreference).

## Requisitos previos

Instale el [módulo SqlServer](https://msdn.microsoft.com/library/mt740629.aspx) en un equipo seguro distinto del equipo que hospeda la instancia de SQL Server. 

Instale el módulo SqlServer mediante la instalación de la versión más reciente de [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
Tenga en cuenta que el módulo *SqlServer* es diferente del módulo *sqlps*, que no admite Always Encrypted. Para obtener más información, vea la entrada de blog del equipo sobre la [actualización de julio de 2016 de SQL PowerShell](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update).

## <a name="importsqlservermodule"></a> Importar el módulo SqlServer 

Para cargar el módulo SqlServer:

1.  Use el cmdlet **Set-ExecutionPolicy** para establecer la directiva de ejecución de script apropiada.
2.  Use el cmdlet **Import-Module** para importar el módulo SqlServer.

En este ejemplo se carga el módulo SqlServer.

```
# Import the SQL Server Module.  
Import-Module "SqlServer" 
```

## <a name="connectingtodatabase"></a> Conectar a una base de datos

Algunos de los cmdlets de Always Encrypted funcionan con datos o metadatos de la base de datos y requieren que se conecte primero a la base de datos. Hay dos métodos recomendados para conectarse a una base de datos al configurar Always Encrypted con el módulo SqlServer: 
1. Conectarse mediante SQL Server PowerShell.
2. Conectarse mediante Objetos de administración de SQL Server (SMO).

### Usar SQL Server PowerShell

Este método solo funciona para SQL Server (no se admite en Base de datos SQL de Azure).

Con SQL Server PowerShell, puede navegar por las rutas de acceso mediante alias de Windows PowerShell similares a los comandos que se usan normalmente para navegar por las rutas de acceso al sistema de archivos. Una vez que se haya desplazado a la instancia de destino y la base de datos, los cmdlets posteriores tendrán como destino dicha base de datos, como se muestra en el ejemplo siguiente:

```
# Import the SqlServer module.
Import-Module "SqlServer"
# Navigate to the database in the remote instance.
cd SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
# List column master keys in the above database.
Get-SqlColumnMasterKey
```

 
También puede especificar una ruta de acceso a la base de datos mediante el parámetro genérico **Path**, en lugar de desplazarse a la base de datos.


```
# Import the SqlServer module.
Import-Module "SqlServer" 
# List column master keys for the specified database.
Get-SqlColumnMasterKey -Path SQLSERVER:\SQL\servercomputer\DEFAULT\Databases\yourdatabase
```
 
### Mediante SMO

Este método funciona para Base de datos SQL de Azure y SQL Server.
Con SMO, puede crear un objeto de la [clase Database](https://msdn.microsoft.com/library/microsoft.sqlserver.management.smo.database.aspx) y pasar dicho objeto mediante el parámetro **InputObject** de un cmdlet que se conecte a la base de datos.


```
# Import the SqlServer module
Import-Module "SqlServer"  

# Connect to your database (Azure SQL database).
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName] 

# List column master keys for the specified database.
Get-SqlColumnMasterKey -InputObject $database
```


También puede usar la canalización:


```
$database | Get-SqlColumnMasterKey
```

## Tareas de Always Encrypted mediante PowerShell

- [Configure Always Encrypted Keys using PowerShell (Configurar claves de Always Encrypted con PowerShell)](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md) 
- [Rotate Always Encrypted Keys using PowerShell (Rotar claves Always Encrypted con PowerShell)](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [Configurar el cifrado de columna con PowerShell](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md)


##  <a name="aecmdletreference"></a> Referencia de cmdlets de Always Encrypted

Los siguientes cmdlets de PowerShell están disponibles para Always Encrypted:

|CMDLET |Descripción
|:---|:---
|**[Add-SqlAzureAuthenticationContext](https://msdn.microsoft.com/library/mt759815.aspx)**  |Realiza la autenticación en Azure y adquiere un token de autenticación.
|**[Add-SqlColumnEncryptionKeyValue](https://msdn.microsoft.com/library/mt759817.aspx)**    |Agrega un nuevo valor cifrado para un objeto de clave de cifrado de columnas existente en la base de datos.
|**[Complete-SqlColumnMasterKeyRotation](https://msdn.microsoft.com/library/mt759791.aspx)**    |Completa la rotación de una clave maestra de columna.
|**[Get-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759814.aspx)** |Devuelve todos los objetos de clave de cifrado de columnas definidos en la base de datos, o devuelve un objeto de clave de cifrado de columnas con el nombre especificado.
|**[Get-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759782.aspx)** |Devuelve los objetos de clave maestra de columna definidos en la base de datos, o devuelve un objeto de clave maestra de columna con el nombre especificado.
|**[Invoke-SqlColumnMasterKeyRotation](https://msdn.microsoft.com/library/mt759810.aspx)**  |Inicia la rotación de una clave maestra de columna.
|**[New-SqlAzureKeyVaultColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759795.aspx)**    |Crea un objeto SqlColumnMasterKeySettings que describe una clave asimétrica almacenada en el Almacén de claves de Azure.
|**[New-SqlCngColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759818.aspx)**  |Crea un objeto SqlColumnMasterKeySettings que describe una clave asimétrica almacenada en un almacén de claves compatible con la API Cryptography Next Generation (CNG).
|**[New-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759808.aspx)** |Crea un objeto de clave de cifrado de columnas en la base de datos.
|**[New-SqlColumnEncryptionKeyEncryptedValue](https://msdn.microsoft.com/library/mt759794.aspx)**   |Produce un valor cifrado de una clave de cifrado de columnas.
|**[New-SqlColumnEncryptionSettings](https://msdn.microsoft.com/library/mt759825.aspx)**    |Crea un objeto SqlColumnEncryptionSettings que encapsula la información sobre el cifrado de una sola columna, incluida la CEK y el tipo de cifrado.
|**[New-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759813.aspx)** |Crea un objeto de clave maestra de columna en la base de datos.
|**New-SqlColumnMasterKeySettings**|Crea un objeto SqlColumnMasterKeySettings para una clave maestra de columna con el proveedor y la ruta de acceso de la clave especificados.
|**[New-SqlCspColumnMasterKeySettings](https://msdn.microsoft.com/library/mt759784.aspx)**  |Crea un objeto SqlColumnMasterKeySettings que describe una clave asimétrica almacenada en un almacén de claves con un proveedor de servicios criptográficos (CSP) compatible con Cryptography API (CAPI).
|**[Remove-SqlColumnEncryptionKey](https://msdn.microsoft.com/library/mt759786.aspx)**  |Quita de la base de datos el objeto de clave de cifrado de columnas.
|**[Remove-SqlColumnEncryptionKeyValue](https://msdn.microsoft.com/library/mt759783.aspx)** |Quita un valor cifrado de un objeto de clave de cifrado de columnas existente en la base de datos.
|**[Remove-SqlColumnMasterKey](https://msdn.microsoft.com/library/mt759800.aspx)**  |Quita de la base de datos el objeto de clave maestra de columna.
|**[Set-SqlColumnEncryption](https://msdn.microsoft.com/library/mt759790.aspx)**    |Cifra, descifra o vuelve a cifrar las columnas especificadas de la base de datos.



## Recursos adicionales

- [Always Encrypted (motor de base de datos)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Uso de Always Encrypted con el proveedor de datos .NET Framework para SQL Server](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [Configure Always Encrypted using SQL Server Management Studio (Configurar Always Encrypted con SQL Server Management Studio)](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

