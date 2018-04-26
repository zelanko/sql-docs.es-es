---
title: Configurar el cifrado de columna con PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: security
ms.reviewer: ''
ms.suite: sql
ms.technology:
- powershell
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 074c012b-cf14-4230-bf0d-55e23d24f9c8
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 106d9e6aa158bacc6938da5f97b2d2268a29b13b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="configure-column-encryption-using-powershell"></a>Configurar el cifrado de columna con PowerShell
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

En este artículo se proporcionan los pasos necesarios para establecer la configuración de destino de Always Encrypted para las columnas de base de datos mediante el cmdlet [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption) (en el módulo *SqlServer* de PowerShell). El cmdlet **Set-SqlColumnEncryption** modifica el esquema de la base de datos de destino y los datos almacenados en las columnas seleccionadas. Los datos almacenados en una columna se pueden cifrar, volver a cifrar o descifrar, en función de la configuración de cifrado de destino especificada para las columnas y la configuración de cifrado actual.
Para más información sobre la compatibilidad de Always Encrypted con el módulo SqlServer de PowerShell, consulte [Configurar Always Encrypted con PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).

## <a name="prerequisites"></a>Prerequisites

Para establecer la configuración de cifrado de destino, debe asegurarse de que:
- Hay una clave de cifrado de columna configurada en la base de datos (si está cifrando o volviendo a cifrar una columna). Para obtener más información, vea [Configure Always Encrypted Keys using PowerShell (Configurar claves de Always Encrypted con PowerShell)](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md).
- Puede tener acceso a la clave maestra de columna para cada columna que quiere cifrar, volver a cifrar o descifrar desde el equipo que ejecuta los cmdlets de PowerShell. 

## <a name="performance-and-availability-considerations"></a>Consideraciones sobre rendimiento y disponibilidad

Para aplicar los valores de cifrado de destino especificad apara la base de datos, el cmdlet **Set-SqlColumnEncryption** descarga sin problemas todos los datos de las columnas que contienen las tablas de destino, carga los datos nuevamente en un conjunto de tabla temporal (con los valores cifrados de destino) y, finalmente, reemplaza las tablas originales por las versiones nuevas de las mismas. El proveedor de datos .NET Framework para SQL Server subyacente cifra y descifra los datos en la descarga o la carga, respectivamente, dependiendo de la configuración de cifrado actual de la columna de destino y los valores de cifrado de destino especificados de las columnas de destino. La operación para mover los datos puede demorar mucho tiempo, en función del tamaño de los datos de las tablas afectadas y el ancho de banda de la red.

El cmdlet **Set-SqlColumnEncryption** admite dos enfoques para configurar el cifrado de destino: en línea y sin conexión.

Con el enfoque sin conexión, las tablas de destino (y cualquier tabla relacionada con las tablas de destino, es decir, cualquier tabla con la que una tabla de destino tenga relaciones de clave externa) no están disponibles para escribir transacciones durante todo el tiempo que demore la operación. La semántica de restricciones de clave externa (**CHECK** o **NOCHECK**) siempre se conserva cuando se utiliza el enfoque sin conexión.

Con el enfoque en línea (requiere el módulo SqlServer PowerShell de SSMS 21.x o una versión posterior), la operación de copiar y cifrar, descifrar o volver a cifrar los datos se realiza de forma incremental. Las aplicaciones pueden leer y escribir datos desde y hacia las tablas de destino a través de la operación de movimiento de datos, excepto en la última iteración, cuya duración está limitada por el parámetro **MaxDownTimeInSeconds** (que puede definir). Para detectar y procesar los cambios que las aplicaciones pueden hacer mientras se copian los datos, el cmdlet habilita el [seguimiento de cambios](../../track-changes/enable-and-disable-change-tracking-sql-server.md) en la base de datos de destino. Debido a esto, es probable que el enfoque en línea consuma más recursos en el lado servidor que el enfoque sin conexión. Es posible que la operación también demore mucho más con el enfoque en línea, especialmente si se ejecuta una carga de trabajo muy pesada en la base de datos. El enfoque en línea se puede usar para cifrar una tabla a la vez y la tabla debe tener una clave principal. De forma predeterminada, se vuelven a crear restricciones de clave externa con la opción **NOCHECK** para minimizar el impacto en las aplicaciones. Puede exigir la conservación de la semántica de restricciones de clave externa mediante la especificación de la opción **KeepCheckForeignKeyConstraints**.

A continuación, las directrices para elegir entre los enfoques sin conexión y en línea:

Use el enfoque sin conexión:
- Para minimizar la duración de la operación. 
- Para cifrar, descifrar y volver a cifrar columnas en varias tablas al mismo tiempo.
- Si la tabla de destino no tiene una clave principal.

Use el enfoque en línea:
- Para minimizar el tiempo de inactividad y la no disponibilidad de la base de datos de para las aplicaciones.

## <a name="security-considerations"></a>Consideraciones de seguridad

El cmdlet **Set-SqlColumnEncryption** , que se usa para configurar el cifrado de las columnas de la base de datos, administra las claves de Always Encrypted y los datos almacenados en las columnas de la base de datos. Por esta razón, es importante que ejecute el cmdlet en un equipo seguro. Si la base de datos está en SQL Server, ejecute el cmdlet en un equipo diferente del que hospeda la instancia de SQL Server. Dado que el objetivo principal de Always Encrypted es garantizar la seguridad de la información confidencial cifrada, incluso si el sistema de base de datos está en peligro, la ejecución de un script de PowerShell que procese las claves o la información confidencial en el equipo de SQL Server puede reducir o anular las ventajas de la característica.

Tarea  |Artículo  |Accede a claves de texto no cifrado o a almacén de claves  |Accede a base de datos   
---|---|---|---
Paso 1. Inicie un entorno de PowerShell e importe el módulo SqlServer. | [Importar el módulo SqlServer](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule) | no | no
Paso 2. Conecte con el servidor y la base de datos. | [Conectar a una base de datos](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | no | Sí
Paso 3. Autentíquese en Azure si la clave maestra de columna (que protege la clave de cifrado de columna que se va a rotar) se almacena en el Almacén de claves de Azure. | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext) | Sí | no
Paso 4. Construya una matriz de objetos SqlColumnEncryptionSettings, una para cada columna de base de datos que quiera cifrar, volver a cifrar o descifrar. SqlColumnMasterKeySettings es un objeto que existe en memoria (en PowerShell). Especifica el esquema de cifrado de destino de una columna. | [New-SqlColumnEncryptionSettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionsettings) | no | no
Paso 5. Establezca la configuración de cifrado que quiera, especificada en la matriz de objetos SqlColumnMasterKeySettings que creó en el paso anterior. Una columna se cifrará, se volverá a cifrar o se descifrará en función de la configuración de destino especificada y la configuración de cifrado actual de la columna.| [Set-SqlColumnEncryption](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/set-sqlcolumnencryption)<br><br>**Nota:** Este paso puede llevar mucho tiempo. Las aplicaciones no podrán tener acceso a las tablas durante toda la operación o parte de esta, dependiendo del enfoque (en línea o sin conexión) que seleccione. | Sí | Sí

## <a name="encrypt-columns-using-offline-approach---example"></a>Cifrar columnas con el enfoque sin conexión: ejemplo

En el ejemplo siguiente se muestra cómo establecer la configuración de cifrado de destino de un par de columnas.  Si alguna de las columnas no está cifrada, se cifrará. Si una columna ya está cifrada con una clave diferente o con un tipo de cifrado diferente, se descifrará y se volverá a cifrar con la clave o el tipo de destino especificados.


```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -LogFileDirectory .
```
 
## <a name="encrypt-columns-using-online-approach---example"></a>Cifrar columnas con el enfoque en línea: ejemplo

En el ejemplo siguiente se muestra cómo establecer la configuración de cifrado de destino de un par de columnas con el enfoque en línea. Si alguna de las columnas no está cifrada, se cifrará. Si una columna ya está cifrada con una clave diferente o con un tipo de cifrado diferente, se descifrará y se volverá a cifrar con la clave o el tipo de destino especificados.

```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Encrypt the selected columns (or re-encrypt, if they are already encrypted using keys/encrypt types, different than the specified keys/types.
$ces = @()
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.SSN" -EncryptionType "Deterministic" -EncryptionKey "CEK1"
$ces += New-SqlColumnEncryptionSettings -ColumnName "dbo.Patients.BirthDate" -EncryptionType "Randomized" -EncryptionKey "CEK1"
Set-SqlColumnEncryption -InputObject $database -ColumnEncryptionSettings $ces -UseOnlineApproach -MaxDowntimeInSeconds 180 -LogFileDirectory .
```
## <a name="decrypt-columns---example"></a>Descifrar columnas: ejemplo

En el ejemplo siguiente se muestra cómo descifrar todas las columnas que actualmente están cifradas en una base de datos.


```
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Find all encrypted columns, and create a SqlColumnEncryptionSetting object for each column.
$ces = @()
$tables = $database.Tables
for($i=0; $i -lt $tables.Count; $i++){
    $columns = $tables[$i].Columns
    for($j=0; $j -lt $columns.Count; $j++) {
        if($columns[$j].isEncrypted) {
            $threeColPartName = $tables[$i].Schema + "." + $tables[$i].Name + "." + $columns[$j].Name 
            $ces += New-SqlColumnEncryptionSettings -ColumnName $threeColPartName -EncryptionType "Plaintext" 
        }
    }
}

# Decrypt all columns.
Set-SqlColumnEncryption -ColumnEncryptionSettings $ces -InputObject $database -LogFileDirectory .
```
 

## <a name="additional-resources"></a>Recursos adicionales
- [Configurar Always Encrypted con PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [Always Encrypted (motor de base de datos)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)



