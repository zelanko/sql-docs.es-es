---
title: Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7c962e1506de5de3b0f7b982a1047f37ca5bd00e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32920710"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tema incluye prácticas recomendadas y sugerencias para la solución de problemas de copias de seguridad y restauraciones de SQL Server en el servicio Blob de Windows Azure.  
  
 Para obtener más información sobre cómo usar el servicio de almacenamiento Blob de Windows Azure para realizar operaciones de copia de seguridad o restauración de SQL Server, vea:  
  
-   [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Tutorial: copias de seguridad y restauración de SQL Server en el servicio de almacenamiento Blob de Windows Azure](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>Administrar copias de seguridad  
 La lista siguiente incluye recomendaciones generales para administrar copias de seguridad:  
  
-   Se recomienda usar un nombre de archivo único para cada copia de seguridad con el fin de evitar que se sobrescriban accidentalmente los blobs.  
  
-   Al crear un contenedor, se recomienda establecer el nivel de acceso en **privado**, de forma que solo los usuarios o las cuentas que puedan proporcionar la información de autenticación necesaria sean capaces de leer o escribir los blobs en el contenedor.  
  
-   En el caso de las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en una máquina virtual de Microsoft Azure, use una cuenta de almacenamiento de la misma región que la máquina virtual para evitar costos de transferencia de datos entre ellas. El uso de la misma región también garantiza un rendimiento óptimo para las operaciones de copia de seguridad y restauración.  
  
-   Una actividad de copia de seguridad con errores puede dar como resultado un archivo de copia de seguridad no válido. Se recomienda identificar periódicamente las copias de seguridad con errores y eliminar los archivos blob. Para obtener más información, consulte [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
-   El uso de la opción `WITH COMPRESSION` durante la copia de seguridad puede reducir al mínimo los costos de almacenamiento y los costos de transacciones de almacenamiento. También puede reducir el tiempo necesario para completar el proceso de copia de seguridad.  

- Establezca los argumentos `MAXTRANSFERSIZE` y `BLOCKSIZE` tal y como se recomienda en [Copia de seguridad en URL de SQL Server](./sql-server-backup-to-url.md).
  
## <a name="handling-large-files"></a>Controlar archivos grandes  
  
-   La operación de copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emplea varios subprocesos para optimizar la transferencia de datos a los servicios de almacenamiento Blob de Windows Azure.  Sin embargo, el rendimiento depende en varios factores, como el ancho de banda del ISV y el tamaño de la base de datos. Si piensa hacer copia de seguridad de bases de datos o grupos de archivos grandes desde una base de datos de SQL Server local, se recomienda que realice primero algunas pruebas de rendimiento. El [SLA de Almacenamiento](http://azure.microsoft.com/support/legal/sla/storage/v1_0/) de Azure tiene unos tiempos máximos de procesamiento para los blobs que puede tener en cuenta.  
  
-   Use la opción `WITH COMPRESSION` como se recomienda en la sección [Administrar copias de seguridad](##managing-backups), ya que es muy importante al realizar la copia de seguridad de archivos grandes.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Resolución de problemas para realizar la copia de seguridad de una dirección URL o una restauración a partir de esta  
 A continuación se indican algunas formas rápidas de solucionar errores al hacer copia de seguridad o restaurar desde el servicio de almacenamiento Blob de Windows Azure.  
  
 Para evitar errores debidos a opciones no admitidas o a limitaciones, consulte la lista de limitaciones y la información de compatibilidad con los comandos BACKUP y RESTORE del artículo [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) .  
  
 **Errores de autenticación:**  
  
-   `WITH CREDENTIAL` es una opción nueva que es necesaria para la copia de seguridad o la restauración con el servicio Microsoft Azure Blob Storage. He aquí algunos errores relacionados con las credenciales:  
  
     La credencial especificada en el comando **BACKUP** o **RESTORE** no existe. Para evitar este problema, puede incluir instrucciones T-SQL para crear la credencial si no existe ninguna en la instrucción de copia de seguridad. He aquí un ejemplo que puede usar:  
  
    ```sql  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
    ```  
  
-   La credencial existe pero la cuenta de inicio de sesión usada para ejecutar el comando de copia de seguridad no tiene permisos de acceso a las credenciales. Use una cuenta de inicio de sesión en el rol **db_backupoperator** con permisos para ***Modificar cualquier credencial*** .  
  
-   Compruebe los valores de clave y nombre de la cuenta de almacenamiento. La información almacenada en la credencial debe coincidir con los valores de propiedad de la cuenta de almacenamiento de Windows Azure que se usa en las operaciones de copia de seguridad y restauración.  
  
 **Errores de copia de seguridad:**  
  
-   Las copias de seguridad en paralelo en el mismo blob produce errores en una de las copias de seguridad y hacen que aparezca un **Error de inicialización** .  
  
-   Use los registros de errores siguientes como ayuda para solucionar problemas de copia de seguridad:  
  
    -   Establezca la marca de seguimiento 3051 para activar el registro en un registro de errores específico con el siguiente formato en:  
  
        `BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log`, donde `\<action>` es uno de los siguientes:  
  
        -   **DB**  
        -   **FILELISTONLY**  
        -   **LABELONLY**  
        -   **HEADERONLY**  
        -   **VERIFYONLY**  
  
    -   También puede encontrar información si examina el registro de eventos de Windows, en los registros de aplicación con el nombre `SQLBackupToUrl`.  
  
-   Al restaurar desde una copia de seguridad comprimida, puede aparecer el siguiente error:  
  
    -   `SqlException 3284 occurred. Severity: 16 State: 5  
        Message Filemark on device 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak' is not aligned.           Reissue the Restore statement with the same block size used to create the backupset: '65536' looks like a possible value.`  
  
        Para resolver este error, vuelva a emitir la instrucción **BACKUP** especificando **BLOCKSIZE = 65536** .  
  
-   Error durante la copia de seguridad porque los blobs tienen una concesión activa: una actividad de copia de seguridad con errores puede dar como resultado blobs con concesiones activas.  
  
     Si se vuelve a intentar una instrucción de copia de seguridad, la operación de copia de seguridad puede producir un error similar al siguiente:  
  
     `Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (412) There is currently a lease on the blob and no lease ID was specified in the request.`  
  
     Si se intenta una instrucción de restauración en un archivo de blob de copia de seguridad que tiene una concesión activa, la operación de restauración produce un error similar al siguiente:  
  
     `Exception Message: The remote server returned an error: (409) Conflict..`  
  
     Cuando se produce ese error, es necesario eliminar los archivos de blob. Para obtener más información sobre este escenario y cómo corregir este problema, vea [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
## <a name="proxy-errors"></a>Errores de proxy  
 Si usa servidores proxy para tener acceso a Internet, pueden producirse los problemas siguientes:  
  
 **Limitación de la conexión por parte de los servidores proxy:**  
  
 Los servidores proxy pueden tener configuraciones que limitan el número de conexiones por minuto. Copia de seguridad en URL es un proceso multiproceso y, por tanto, puede sobrepasar este límite. Si esto ocurre, el servidor proxy elimina la conexión. Para resolver este problema, cambie la configuración de proxy para que SQL Server no utilice el proxy. A continuación se muestran algunos ejemplos de los tipos o mensajes de error que puede ver en el registro de errores:  
  
```
Write on "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak" failed: Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
```
A nonrecoverable I/O error occurred on file "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Error could not be gathered from Remote Endpoint.  
  
Msg 3013, Level 16, State 1, Line 2  
  
BACKUP DATABASE is terminating abnormally.  
```

```
BackupIoRequest::ReportIoError: write failure on backup device http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Operating system error Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
Si activa el registro detallado mediante la marca de seguimiento 3051, puede ver también el mensaje siguiente en los registros:  
  
`HTTP status code 502, HTTP Status Message Proxy Error (The number of HTTP requests per minute exceeded the configured limit. Contact your ISA Server administrator.) ` 
  
 **Configuración de proxy predeterminada no seleccionada:**  
  
A veces la configuración predefinida no se realiza correctamente, lo que provoca errores de autenticación de proxy, como el que se muestra a continuación:
 
 `A nonrecoverable I/O error occurred on file "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (407)* **Proxy Authentication Required.`  
  
Para resolver este problema, cree un archivo de configuración que permita al proceso Copia de seguridad en URL utilizar la configuración de proxy predeterminada mediante los pasos siguientes:  
  
1.  Cree un archivo de configuración denominado `BackuptoURL.exe.config` con el contenido XML siguiente:  
  
    ```xml  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
    ```  
  
2.  Coloque el archivo de configuración en la carpeta Binn de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado en la unidad C del equipo, coloque el archivo de configuración en `C:\Program Files\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Binn`.  
  
## <a name="see-also"></a>Ver también  
 [Restaurar a partir de copias de seguridad archivadas en Microsoft Azure](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)
  
