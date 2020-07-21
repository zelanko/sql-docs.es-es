---
title: Eliminación de archivos de blob de copia de seguridad con concesiones activas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8301c1f88eb8cf928066a3c12b14452ddbd98cda
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958515"
---
# <a name="deleting-backup-blob-files-with-active-leases"></a>Eliminar archivos de blob de copia de seguridad con concesiones activas
  Cuando se realiza una copia de seguridad o se restaura desde Azure Storage, SQL Server adquiere una concesión infinita para bloquear el acceso exclusivo al BLOB. Cuando el proceso de copia de seguridad o de restauración se ha completado correctamente, se libera la concesión. Si una copia de seguridad o una restauración dan error, el proceso de copia de seguridad intenta limpiar los blobs no válidos. Sin embargo, si el error de la copia de seguridad se debe a un error de conectividad en la red mantenido o prolongado, es posible que el proceso de copia de seguridad no pueda obtener acceso al blob y este podría quedar huérfano. Esto significa que no se puede escribir en el blob o que el blob no se puede eliminar hasta que no se libera la concesión. En este tema se describe cómo liberar la concesión y eliminar el blob.  
  
 Para obtener más información sobre los tipos de concesiones, lea este [artículo](https://go.microsoft.com/fwlink/?LinkId=275664).  
  
 Si se produce un error en la operación de copia de seguridad, se puede obtener un archivo de copia de seguridad que no es válido.  El archivo blob de copia de seguridad también podría tener una concesión activa, impidiendo su eliminación o sobrescritura.  Con el fin de eliminar o sobrescribir estos blobs, primero se debe interrumpir la concesión. Si hay errores de copia de seguridad, se recomienda limpiar las concesiones y eliminar los blobs. También puede elegir periódicamente una limpieza como parte de las tareas de administración de almacenamiento.  
  
 Si se produce un error de restauración, las restauraciones posteriores no se bloquean y, por tanto, la concesión activa puede no suponer ningún problema. Solo es necesario interrumpir la concesión cuando se tiene que sobrescribir o eliminar el blob.  
  
## <a name="managing-orphaned-blobs"></a>Administrar blobs huérfanos  
 En los pasos siguientes se describe cómo realizar la limpieza después de una actividad de copia de seguridad o restauración con errores. Todos los pasos se pueden realizar mediante scripts de PowerShell. En la sección siguiente se proporciona un ejemplo de código:  
  
1.  **Identificar blobs que tienen concesiones** : si tiene un script o un proceso que ejecuta los procesos de copia de seguridad, es posible que pueda capturar el error dentro del script o del proceso y usarlo para limpiar los blobs.   También puede usar las propiedades LeaseStats y LeastState para identificar los blobs que tienen concesiones. Una vez identificados los blobs, se recomienda que revise la lista y compruebe la validez del archivo de copia de seguridad antes de eliminar el blob.  
  
2.  **Interrumpir la concesión** : una solicitud autorizada puede interrumpir la concesión sin proporcionar un identificador de concesión. Vea [aquí](https://go.microsoft.com/fwlink/?LinkID=275664) para obtener más información.  
  
    > [!TIP]  
    >  SQL Server emite un identificador de concesión para establecer acceso exclusivo durante la operación de restauración. El identificador de concesión de restauración es BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2.  
  
3.  **Eliminar el blob** : para eliminar un blob que tiene una concesión activa, debe interrumpir primero la concesión.  
  
###  <a name="powershell-script-example"></a><a name="Code_Example"></a>Ejemplo de script de PowerShell  
 Importante: Si está ejecutando PowerShell 2,0, puede que tenga problemas al cargar el ensamblado de Microsoft WindowsAzure.Storage.dll. ** \* \* \* \* ** Recomendamos que se actualice a Powershell 3.0 para resolver el problema. También puede usar la siguiente solución alternativa para PowerShell 2.0:  
  
-   Cree o modifique el archivo powershell.exe.config para cargar los ensamblados de .NET 2.0 y .NET 4.0 en tiempo de ejecución con lo siguiente:  
  
    ```xml
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0.30319"/>
            <supportedRuntime version="v2.0.50727"/>
        </startup>
    </configuration>
    ```  
  
 En el ejemplo siguiente se ilustra cómo identificar los blobs que tienen concesiones activas y cómo interrumpirlas. En el ejemplo también se muestra cómo filtrar los identificadores de concesión de versión.  
  
 Sugerencias para ejecutar este script  
  
> [!WARNING]  
>  Si una copia de seguridad en el servicio de almacenamiento de blobs de Azure se está ejecutando al mismo tiempo que este script, se puede producir un error en la copia de seguridad, ya que este script interrumpirá la concesión que la copia de seguridad está intentando adquirir al mismo tiempo. Se recomienda ejecutar este script durante una ventana de mantenimiento o cuando no esté previsto que se ejecute ninguna copia de seguridad.  
  
1.  Al ejecutar este script, se le pedirá que proporcione valores para la cuenta de almacenamiento, la clave de almacenamiento, el contenedor y los parámetros de ruta de acceso y nombre del ensamblado de Azure Storage. La ruta de acceso del almacenamiento en el ensamblado es el directorio de instalación de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El nombre de archivo del ensamblado de almacenamiento es Microsoft.WindowsAzure.Storage.dll. A continuación se muestra un ejemplo de los mensajes y los valores especificados:  
  
    ```  
    cmdlet  at command pipeline position 1  
    Supply values for the following parameters:  
    storageAccount: mycloudstorageaccount  
    storageKey: 0BopKY7eEha3gBnistYk+904nf  
    blobContainer: mycontainer   
    storageAssemblyPath: C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Microsoft.WindowsAzure.Storage.dll  
    ```  
  
2.  Si no hay ningún blob que tenga concesiones bloqueadas debe aparecer un mensaje similar al siguiente:  
  
     **No hay ningún blob con el estado de concesión bloqueada**  
  
     Si hay blobs con concesiones bloqueadas, debe ver los mensajes siguientes:  
  
     **Interrumpir concesiones**  
  
     **La concesión de \<URL of the Blob> es una concesión de restauración: solo verá este mensaje si tiene un BLOB con una concesión de restauración que todavía está activa.**  
  
     **La concesión en \<URL of the Blob> no es una concesión de restauración interrumpida en \<URL of the Bob> .**  
  
```powershell
param(  
       [Parameter(Mandatory=$true)]  
       [string]$storageAccount,  
       [Parameter(Mandatory=$true)]  
       [string]$storageKey,  
       [Parameter(Mandatory=$true)]  
       [string]$blobContainer,  
       [Parameter(Mandatory=$true)]  
       [string]$storageAssemblyPath  
)  
  
# Well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# Load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
$container = $client.GetContainerReference($blobContainer)  
  
#list all the blobs  
$allBlobs = $container.ListBlobs()
  
$lockedBlobs = @()  
# filter blobs that are have Lease Status as "locked"  
foreach($blob in $allBlobs)  
{  
    $blobProperties = $blob.Properties
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
    }  
}  
  
if ($lockedBlobs.Count -eq 0)  
{
    Write-Host " There are no blobs with locked lease status"  
}

if($lockedBlobs.Count -gt 0)  
{  
    Write-Host "Breaking leases"  
    foreach($blob in $lockedBlobs )
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease"  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease"  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)"  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
}
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos recomendados y solución de problemas de Copia de seguridad en URL de SQL Server](sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
