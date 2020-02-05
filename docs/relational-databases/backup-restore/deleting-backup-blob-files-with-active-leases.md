---
title: Eliminación de archivos de blob de copia de seguridad con concesiones activas | Microsoft Docs
ms.custom: ''
ms.date: 08/17/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cdc58884e65fb243bbb75f257e19ccef3faa2b9f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "72908935"
---
# <a name="delete-backup-blob-files-with-active-leases"></a>Eliminar archivos de blob de copia de seguridad con concesiones activas

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Cuando se hace una copia de seguridad en Microsoft Azure Storage, o cuando se restaura del mismo, SQL Server adquiere una concesión infinita para bloquear el acceso exclusivo al blob. Cuando el proceso de copia de seguridad o de restauración se ha completado correctamente, se libera la concesión. Si una copia de seguridad o una restauración dan error, el proceso de copia de seguridad intenta limpiar los blobs no válidos. Sin embargo, si el error de la copia de seguridad se debe a un error de conectividad en la red mantenido o prolongado, es posible que el proceso de copia de seguridad no pueda obtener acceso al blob y este podría quedar huérfano. Esto significa que no se puede escribir en el blob o que el blob no se puede eliminar hasta que no se libera la concesión. En este tema, se describe cómo liberar (interrumpir) la concesión y eliminar el blob.
  
Para obtener más información sobre los tipos de concesiones, lea este [artículo](https://go.microsoft.com/fwlink/?LinkId=275664).  
  
Si se produce un error en la operación de copia de seguridad, se puede obtener un archivo de copia de seguridad no válido. El archivo blob de copia de seguridad también podría tener una concesión activa, impidiendo su eliminación o sobrescritura. Para eliminar o sobrescribir estos blobs, primero se debe liberar (interrumpir) la concesión. Si hay errores de copia de seguridad, se recomienda que limpie las concesiones y elimine los blobs. Además, puede limpiar periódicamente las concesiones y eliminar los blobs como parte de las tareas de administración del almacenamiento.  
  
Si se produce un error de restauración, las restauraciones posteriores no se bloquean, por lo que la concesión activa puede no suponer ningún problema. Solo es necesario interrumpir la concesión cuando se tiene que sobrescribir o eliminar el blob.  
  
## <a name="manage-orphaned-blobs"></a>Administrar blobs huérfanos

En los pasos siguientes se describe cómo realizar la limpieza después de una actividad de copia de seguridad o restauración con errores. Puede realizar todos los pasos mediante scripts de PowerShell. En la sección siguiente, se incluye un ejemplo de script de PowerShell:  
  
1. **Identificar blobs con concesiones**: si tiene un script o un proceso que ejecuta los procesos de copia de seguridad, es posible que pueda capturar el error dentro del script o del proceso y usarlo para limpiar los blobs.  También puede usar las propiedades LeaseStats y LeastState para identificar blobs con concesiones. Una vez identificados los blobs, revise la lista y compruebe la validez del archivo de copia de seguridad antes de eliminar el blob.  
  
1. **Interrumpir la concesión**: una solicitud autorizada puede interrumpir la concesión sin proporcionar un identificador de concesión. Vea [aquí](https://go.microsoft.com/fwlink/?LinkID=275664) para obtener más información.  
  
    > [!TIP]  
    > SQL Server emite un identificador de concesión para establecer acceso exclusivo durante la operación de restauración. El identificador de concesión de restauración es BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2.  
  
1. **Eliminar el blob**: para eliminar un blob con una concesión activa, debe interrumpir primero la concesión.  

###  <a name="Code_Example"></a> Ejemplo de script de PowerShell  
  
> [!IMPORTANT]
> Si está ejecutando PowerShell 2.0, quizás tenga problemas al cargar el ensamblado de Microsoft WindowsAzure.Storage.dll. Recomendamos que actualice [PowerShell](https://docs.microsoft.com/powershell/) para resolver el problema. También puede usar la solución alternativa siguiente para crear o modificar el archivo powershell.exe.config para cargar los ensamblados de .NET 2.0 y .NET 4.0 en tiempo de ejecución con lo siguiente:  
>
> ```xml
> <?xml version="1.0"?>
>     <configuration>
>         <startup useLegacyV2RuntimeActivationPolicy="true">
>             <supportedRuntime version="v4.0.30319"/>
>             <supportedRuntime version="v2.0.50727"/>
>         </startup>
>     </configuration>  
> ```  
  
 El siguiente script de ejemplo identifica blobs con concesiones activas y, después, las interrumpe. En el ejemplo también se muestra cómo filtrar los identificadores de concesión de versión.  
  
#### <a name="tips-on-running-this-script"></a>Sugerencias para ejecutar este script
  
> [!WARNING]  
> Si una copia de seguridad del servicio de almacenamiento de blobs de Azure se ejecuta a la vez que este script, se puede producir un error en la copia de seguridad porque este script interrumpirá la concesión que la copia de seguridad intenta adquirir al mismo tiempo. Ejecute este script durante un período de mantenimiento o cuando no se esté ejecutando ninguna copia de seguridad ni esté previsto que se vaya a ejecutar ninguna.  
  
- Antes de ejecutar este script, debe agregar valores para la cuenta de almacenamiento, la clave de almacenamiento, el contenedor, y los parámetros de ruta de acceso y nombre de ensamblado de almacenamiento de Azure. La ruta de acceso del almacenamiento en el ensamblado es el directorio de instalación de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El nombre de archivo del ensamblado de almacenamiento es Microsoft.WindowsAzure.Storage.dll.
  
- Si no hay blobs con concesiones bloqueadas, debería ver el mensaje siguiente: `There are no blobs with locked lease status`.
  
- Si hay blobs con concesiones bloqueadas, debe ver los mensajes siguientes: `Breaking Leases`, `The lease on <URL of the Blob> is a restore lease: You will see this message only if you have a blob with a restore lease that is still active.` y `The lease on <URL of the Blob> is not a restore lease Breaking lease on <URL of the Bob>.`
  
```powershell
$storageAccount = "<myStorageAccount>"
$storageKey = "<myStorageKey>"
$blobContainer = "<myBlobContainer>"
$storageAssemblyPathName = "<myStorageAssemblyPathName>"
  
# well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
$container = $client.GetContainerReference($blobContainer)  
  
# list all the blobs  
$blobs = $container.ListBlobs($null,$true)
  
# filter blobs that are have Lease Status as "locked"
$lockedBlobs = @()  
foreach($blob in $blobs)  
{  
    $blobProperties = $blob.Properties
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
    }  
}  

if($lockedBlobs.Count -gt 0)  
{  
    Write-Host "Breaking leases..."
    foreach($blob in $lockedBlobs )
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease."  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease."  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)."  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
} else { Write-Host " There are no blobs with locked lease status." }
```  
  
## <a name="see-also"></a>Consulte también

[Procedimientos recomendados y solución de problemas de Copia de seguridad en URL de SQL Server](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
