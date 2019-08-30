---
title: Usar PowerShell para realizar una copia de seguridad de varias bases de datos en Azure Blob Storage servicio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b1be1f05ff09d85d29903e4e3be7f1f11600a7b1
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155029"
---
# <a name="use-powershell-to-backup-multiple-databases-to-azure-blob-storage-service"></a>Usar PowerShell para realizar una copia de seguridad de varias bases de datos en Azure Blob Storage servicio
  En este tema se proporcionan scripts de ejemplo que se pueden usar para automatizar las copias de seguridad en el servicio de almacenamiento de blobs de Azure mediante cmdlets de PowerShell.  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>Información general de los cmdlets de PowerShell para las copias de seguridad y restauración  
 `Backup-SqlDatabase` y `Restore-SqlDatabase` son los dos cmdlets principales disponibles para realizar operaciones de copias de seguridad y restauración. Además, hay otros cmdlets que pueden ser necesarios para automatizar las copias de seguridad en almacenamiento de blobs de Azure como el conjunto de cmdlets de **SqlCredential** que se indican a continuación es [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] una lista de los cmdlets de PowerShell disponibles en que se usan en las operaciones de copia de seguridad y restauración:  
  
 Backup-SqlDatabase  
 Este cmdlet se utiliza para crear una copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Restore-SqlDatabase  
 Se usa para restaurar una base de datos.  
  
 New-SqlCredential  
 Este cmdlet se usa para crear una credencial de SQL que se usará para la copia de seguridad de SQL Server en Azure Storage. Para obtener más información sobre las credenciales y su uso en SQL Server copias de seguridad y restauración, consulte [SQL Server Backup and restore with Azure BLOB Storage Service](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
 Get-SqlCredential  
 Este cmdlet se utiliza para recuperar el objeto Credencial y sus propiedades.  
  
 Remove-SqlCredential  
 Eliminar un objeto Credencial SQL  
  
 Set-SqlCredential  
 Este cmdlet se utiliza para cambiar o establecer las propiedades del objeto Credencial SQL.  
  
> [!TIP]  
>  Los cmdlets de credenciales se usan en escenarios de copia de seguridad y restauración en Azure BLOB Storage.  
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>PowerShell para operaciones de copia de seguridad de varias instancias y varias bases de datos  
 Las secciones siguientes contienen scripts para varias operaciones como crear una credencial SQL en varias instancias de SQL Server, hacer la copia de seguridad de todas las bases de datos de usuario en una instancia de SQL Server, etcétera. Puede utilizar estos scripts para automatizar o para programar las operaciones de copia de seguridad según los requisitos de su entorno. Los scripts que aquí se muestran son ejemplos y se pueden modificar o ampliar para su entorno.  
  
 A continuación se presentan las consideraciones para los scripts de ejemplo:  
  
1.  **Navegar por las rutas de acceso de SQL Server PowerShell:** Windows PowerShell implementa cmdlets para navegar por la estructura de ruta de acceso que representa la jerarquía de objetos compatible con un proveedor de PowerShell. Cuando ha navegado a un nodo de la ruta de acceso, puede usar otros cmdlets para realizar operaciones básicas en el objeto actual.  
  
2.  `Get-ChildItem`cmdlet La información devuelta por `Get-ChildItem` depende de la ubicación en una ruta de acceso SQL Server PowerShell. Por ejemplo, si la ubicación está en el equipo, este cmdlet devuelve todas las instancias del motor de base de datos de SQL Server instaladas en él. Como otro ejemplo, si la ubicación está en un objeto como son las bases de datos, este cmdlet devuelve una lista de objetos de base de datos.  De forma predeterminada, el cmdlet `Get-ChildItem` no devuelve los objetos del sistema.  Con el parámetro -Force, puede ver los objetos del sistema.  
  
     Para obtener más información, consulte [Navigate SQL Server PowerShell Paths](../../powershell/navigate-sql-server-powershell-paths.md).  
  
3.  Aunque cada ejemplo de código se puede probar de forma independiente cambiando los valores de las variables, crear una cuenta de Azure Storage y una credencial SQL son requisitos previos y son necesarios para todas las operaciones de copia de seguridad y restauración en el servicio Azure BLOB Storage.  
  
### <a name="create-a-sql-credential-on-all-the-instances-of-sql-server"></a>Crear una credencial SQL en todas las instancias de SQL Server  
 Hay dos ejemplos de scripts y ambos crean una credencial SQL "mybackupToURL" en todas las instancias de SQL Server de un equipo. El primer ejemplo es sencillo, crea la credencial y no intercepta las excepciones.  Por ejemplo, si hubiera ya una credencial existente con el mismo nombre en una de las instancias del equipo, el script produciría un error. El segundo ejemplo intercepta los errores y permite que el script continúe.  
  
```  
  
import-module sqlps  
  
# create variables  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
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
cd sqlserver:\sql\COMPUTERNAME  
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
  
### <a name="remove-a-sql-credential-from-all-the-instances-of-sql-server"></a>Quitar una credencial SQL de todas las instancias de SQL Server  
 Este script se puede utilizar para quitar una credencial específica de todas las instancias de SQL Server instaladas en el equipo. Si el objeto Credencial no existe en una instancia concreta, aparece un mensaje de error y el script continúa hasta que se comprueban todas las instancias.  
  
```  
  
import-module sqlps  
  
cd SQLServer:\SQL\COMPUTERNAME  
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
  
### <a name="full-database-backup-for-all-databases-including-system-databases"></a>Copia de seguridad completa de base de datos para todas las bases de datos (INCLUDING SYSTEM DATABASES)  
 El siguiente script crea copias de seguridad de todas las bases de datos del equipo. Esto incluye tanto a las bases de datos de usuario como a la base de datos del sistema **msdb** . El script filtra las bases de datos del sistema **tempdb** y **model** .  
  
```  
  
import-module sqlps  
# set the parameter values  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the  databases -filter out tempdb and model databases  
  
 foreach ($instance in $instances)  
 {  
   $path = "sqlserver:\sql\$($instance.name)\databases"  
   $alldatabases = get-childitem -Force -path $path |Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}   
  
   $alldatabases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On -script   
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases"></a>Copia de seguridad completa de base de datos de todas las bases de datos de usuario  
 El script siguiente se puede utilizar para realizar la copia de seguridad de todas las bases de datos de usuario en todas las instancias de SQL Server del equipo.  
  
```  
  
import-module sqlps   
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the user databases  
 foreach ($instance in $instances)  
 {  
    $databases = dir "sqlserver:\sql\$($instance.name)\databases"  
   $databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On   
 }  
```  
  
### <a name="full-database-backup-for-master-and-msdb-system-databases-on-all-the-instances-of-sql-server"></a>Copia de seguridad completa de la base de datos MAESTRA y MSDB (BASES DATABASE SYSTEM) en todas las instancias de SQL Server  
 El script siguiente se puede usar para crear copias de seguridad de las bases de datos **master** y **msdb** en todas las instancias de SQL Server instaladas en el equipo.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackupToUrl"  
$sysDbs = "master", "msdb"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
$instances = Get-childitem   
foreach ($instance in $instances)  
 {  
      foreach ($s in $sysdbs)  
     {  
Backup-SqlDatabase -Database $s -path "sqlserver:\sql\$($instance.name)" -BackupContainer  $backupUrlContainer -SqlCredential $credentialName -Compression On   
}    
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases-on-an-instance-of-sql-server"></a>Copia de seguridad completa de todas las bases de datos de usuario en una instancia de SQL Server  
 El siguiente script se utiliza para realizar la copia de seguridad solo de las bases de datos de usuario disponibles en una instancia con nombre de SQL Server. El mismo script se puede utilizar para la instancia predeterminada del equipo cambiando el valor del parámetro $srvPath.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\COMPUTERNAME\INSTANCENAME"  # for default instance, the $srvpath variable is "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#cd to computer level  
cd sqlserver:\sql\COMPUTERNAME  
  
#retrieves the database objects for a specific instance  
$databases = dir $srvPath\databases  
  
#backup all the user databases  
$databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
```  
  
### <a name="full-database-backup-for-only-system-databases-master-and-msdb-on-an-instance-of-sql-server"></a>Copia de seguridad completa solo de las bases de datos del sistema (MAESTRA y MSDB) en una instancia de SQL Server  
 El script completo se puede usar para crear una copia de seguridad de las bases de datos **master** y **msdb** en una instancia con nombre de SQL Server. El mismo script se puede utilizar para la instancia predeterminada del equipo cambiando el valor del parámetro $srvPath.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\COMPUTERNAME\INSTANCENAME" # for default instance, the $srvpath variable is "SQLSERVER:\SQL\COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#navigate to instance level  
cd $srvPath  
  
$sysDbs = "master", "msdb"  
foreach ($s in $sysDbs)   
{  
Backup-SqlDatabase -Database $s -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
}  
  
```  
  
## <a name="see-also"></a>Vea también  
 [SQL Server copias de seguridad y restauración con Azure Blob Storage servicio](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server](sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
