---
title: "Usar PowerShell para crear copias de seguridad de varias bases de datos en el servicio de Almacenamiento de blobs de Microsoft Azure | Microsoft Docs"
ms.custom: ""
ms.date: "05/20/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-backup-restore"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# Usar PowerShell para crear copias de seguridad de varias bases de datos en el servicio de Almacenamiento de blobs de Microsoft Azure
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tema proporciona ejemplos de scripts que se pueden utilizar para automatizar las copias de seguridad del servicio de almacenamiento Blob de Windows Azure con los cmdlets de PowerShell.  
  
## Información general de los cmdlets de PowerShell para las copias de seguridad y restauración  
 El **Backup-SqlDatabase** y **Restore-SqlDatabase** son dos cmdlets principales disponibles para realizar operaciones de copia de seguridad y restauración. Además, hay otros cmdlets que pueden requerir automatizar las copias de seguridad para el almacenamiento Blob de Windows Azure como el conjunto de cmdlets de **SqlCredential** . La siguiente es una lista de los cmdlets de PowerShell disponibles en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que se utilizan en las operaciones de copia de seguridad y restauración:  
  
 Backup-SqlDatabase  
 Este cmdlet se utiliza para crear una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Restore-SqlDatabase  
 Se usa para restaurar una base de datos.  
  
 New-SqlCredential  
 Este cmdlet se utiliza para crear una credencial SQL para la copia de seguridad de SQL Server en el Almacenamiento de Windows Azure. Para obtener más información sobre las credenciales y su uso en las copias de seguridad y restauración de SQL Server, vea [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 Get-SqlCredential  
 Este cmdlet se utiliza para recuperar el objeto Credencial y sus propiedades.  
  
 Remove-SqlCredential  
 Eliminar un objeto Credencial SQL  
  
 Set-SqlCredential  
 Este cmdlet se utiliza para cambiar o establecer las propiedades del objeto Credencial SQL.  
  
> [!TIP]  
>  Los cmdlets de credenciales se utilizan en las copias de seguridad y en la restauración en los escenarios de almacenamiento Blob de Windows Azure.  
  
### PowerShell para operaciones de copia de seguridad de varias instancias y varias bases de datos  
 Las secciones siguientes contienen scripts para varias operaciones como crear una credencial SQL en varias instancias de SQL Server, hacer la copia de seguridad de todas las bases de datos de usuario en una instancia de SQL Server, etcétera. Puede utilizar estos scripts para automatizar o para programar las operaciones de copia de seguridad según los requisitos de su entorno. Los scripts que aquí se muestran son ejemplos y se pueden modificar o ampliar para su entorno.  
  
 A continuación se presentan las consideraciones para los scripts de ejemplo:  
  
1.  **Navegar por las rutas de acceso de SQL Server PowerShell:** Windows PowerShell implementa cmdlets para navegar por la estructura de ruta de acceso que representa la jerarquía de objetos compatible con un proveedor de PowerShell. Cuando ha navegado a un nodo de la ruta de acceso, puede usar otros cmdlets para realizar operaciones básicas en el objeto actual.  
  
2.  Cmdlet **Get-ChildItem**: la información devuelta por **Get-ChildItem** depende de la ubicación de una ruta de acceso de PowerShell de SQL Server. Por ejemplo, si la ubicación está en el equipo, este cmdlet devuelve todas las instancias del motor de base de datos de SQL Server instaladas en él. Como otro ejemplo, si la ubicación está en un objeto como son las bases de datos, este cmdlet devuelve una lista de objetos de base de datos.  De forma predeterminada, el cmdlet **Get-ChildItem** no devuelve los objetos del sistema.  Mediante el parámetro –Force, puede ver los objetos del sistema.  
  
     Para obtener más información, consulte [Navigate SQL Server PowerShell Paths](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md).  
  
3.  Aunque cada ejemplo de código se pueda probar de forma independiente cambiando los valores de las variables, crear una cuenta de Almacenamiento de Windows Azure y una credencial SQL son requisitos previos y es imprescindible para todas las operaciones de copia de seguridad y de restauración en el servicio de almacenamiento Blob de Windows Azure.  
  
### Crear una credencial SQL en todas las instancias de SQL Server  
 Hay dos ejemplos de scripts y ambos crean una credencial SQL “mybackupToURL“ en todas las instancias de SQL Server de un equipo. El primer ejemplo es sencillo, crea la credencial y no intercepta las excepciones.  Por ejemplo, si hubiera ya una credencial existente con el mismo nombre en una de las instancias del equipo, el script produciría un error. El segundo ejemplo intercepta los errores y permite que el script continúe.  
  
```  
  
import-module sqlps  
  
# create variables  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#pipe the instances to new-sqlcredentail cmdlet to create SQL credential  
$instances | new-sqlcredential -Name $credentialName  -Identity $storageAccount -Secret $secureString  
```  
  
```  
  
import-module sqlps  
  
# set the parameter values  
  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#loop through instances and create a SQL credential, output any errors  
foreach ($instance in $instances)  
{  
    Try  
{  
     new-sqlcredential -Name $credentialName -path "SQLServer:\SQL\$($instance.name)" -Identity $storageAccount -Secret $secureString -ea Stop   
}  
Catch [Exception]  
    {  
  
            write-host "instance - $($instance.name): "$_.Exception.Message  
  
    }  
  
 }  
  
```  
  
### Quitar una credencial SQL de todas las instancias de SQL Server  
 Este script se puede utilizar para quitar una credencial específica de todas las instancias de SQL Server instaladas en el equipo. Si el objeto Credencial no existe en una instancia concreta, aparece un mensaje de error y el script continúa hasta que se comprueban todas las instancias.  
  
```  
  
import-module sqlps  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$credentialName = "mybackuptoURL"  
  
$instances = Get-childitem  
  
foreach ($instance in $instances)  
   {   
    try  
        {  
            $path = "SQLServer:\SQL\$($instance.name)\credentials\$credentialName"   
            Remove-sqlCredential -path $path -ea stop   
         }  
         catch [Exception]  
         {  
            write-host $_.Exception.Message  
  
        }  
  
    }  
```  
  
### Copia de seguridad completa de base de datos para todas las bases de datos (INCLUDING SYSTEM DATABASES)  
 El siguiente script crea copias de seguridad de todas las bases de datos del equipo. Esto incluye tanto a las bases de datos de usuario como a la base de datos del sistema **msdb** . El script filtra las bases de datos del sistema **tempdb** y **model** .  
  
```  
  
import-module sqlps  
# set the parameter values  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the  databases -filter out tempdb and model databases  
  
 foreach ($instance in $instances)  
 {  
   $path = "sqlserver:\sql\$($instance.name)\databases"  
   $alldatabases = get-childitem -Force -path $path |Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}   
  
   $alldatabases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On -script   
 }  
  
```  
  
### Copia de seguridad completa de base de datos de todas las bases de datos de usuario  
 El script siguiente se puede utilizar para realizar la copia de seguridad de todas las bases de datos de usuario en todas las instancias de SQL Server del equipo.  
  
```  
  
import-module sqlps   
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the user databases  
 foreach ($instance in $instances)  
 {  
    $databases = dir "sqlserver:\sql\$($instance.name)\databases"  
   $databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On   
 }  
```  
  
### Copia de seguridad completa de la base de datos MAESTRA y MSDB (BASES DATABASE SYSTEM) en todas las instancias de SQL Server  
 El script siguiente se puede usar para crear copias de seguridad de las bases de datos **master** y **msdb** en todas las instancias de SQL Server instaladas en el equipo.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackupToUrl"  
$sysDbs = "master", "msdb"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
foreach ($instance in $instances)  
 {  
      foreach ($s in $sysdbs)  
     {  
Backup-SqlDatabase -Database $s -path "sqlserver:\sql\$($instance.name)" -BackupContainer  $backupUrlContainer -SqlCredential $credentialName -Compression On   
}    
 }  
  
```  
  
### Copia de seguridad completa de todas las bases de datos de usuario en una instancia de SQL Server  
 El siguiente script se utiliza para realizar la copia de seguridad solo de las bases de datos de usuario disponibles en una instancia con nombre de SQL Server. El mismo script se puede utilizar para la instancia predeterminada del equipo cambiando el valor del parámetro $srvPath.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME"  # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
  
#retrieves the database objects for a specific instance  
$databases = dir $srvPath\databases  
  
#backup all the user databases  
$databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
```  
  
### Copia de seguridad completa solo de las bases de datos del sistema (MAESTRA y MSDB) en una instancia de SQL Server  
 El script completo se puede usar para crear una copia de seguridad de las bases de datos **master** y **msdb** en una instancia con nombre de SQL Server. El mismo script se puede utilizar para la instancia predeterminada del equipo cambiando el valor del parámetro $srvpath.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME" # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#navigate to instance level  
cd $srvPath  
  
$sysDbs = "master", "msdb"  
foreach ($s in $sysDbs)   
{  
Backup-SqlDatabase -Database $s -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
}  
  
```  
  
## Vea también  
 [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  