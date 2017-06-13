---
title: "Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: c0e55c0e35039490f0ce4cd8a7fb6d7e232c05aa
ms.openlocfilehash: b76a0f262fd12e53797c0ad86c991a6e4423927a
ms.contentlocale: es-es
ms.lasthandoff: 04/15/2017

---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>Prácticas recomendadas y solución de problemas de Copia de seguridad en URL de SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Este tema incluye prácticas recomendadas y sugerencias para la solución de problemas de copias de seguridad y restauraciones de SQL Server en el servicio Blob de Windows Azure.  
  
 Para obtener más información sobre cómo usar el servicio de almacenamiento Blob de Windows Azure para realizar operaciones de copia de seguridad o restauración de SQL Server, vea:  
  
-   [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [Tutorial: copias de seguridad y restauración de SQL Server en el servicio de almacenamiento Blob de Windows Azure](~/relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups"></a>Administrar copias de seguridad  
 La lista siguiente incluye recomendaciones generales para administrar copias de seguridad:  
  
-   Se recomienda usar un nombre de archivo único para cada copia de seguridad con el fin de evitar que se sobrescriban accidentalmente los blobs.  
  
-   Al crear un contenedor, se recomienda establecer el nivel de acceso en **privado**, de forma que solo los usuarios o las cuentas que puedan proporcionar la información de autenticación necesaria sean capaces de leer o escribir los blobs en el contenedor.  
  
-   En el caso de bases de datos de SQL Server en una instancia de SQL Server que se ejecuta en una máquina virtual de Windows Azure, use una cuenta de almacenamiento de la misma región que la máquina virtual para evitar costos de transferencia de datos entre las regiones. El uso de la misma región también garantiza un rendimiento óptimo para las operaciones de copia de seguridad y restauración.  
  
-   Una actividad de copia de seguridad con errores puede dar como resultado un archivo de copia de seguridad no válido. Se recomienda identificar periódicamente las copias de seguridad con errores y eliminar los archivos blob. Para obtener más información, consulte [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
-   El uso de la opción **WITH COMPRESSION** durante la copia de seguridad puede reducir al mínimo los costos de almacenamiento y los costos de transacciones de almacenamiento. También puede reducir el tiempo necesario para completar el proceso de copia de seguridad.  
  
## <a name="handling-large-files"></a>Controlar archivos grandes  
  
-   La operación de copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emplea varios subprocesos para optimizar la transferencia de datos a los servicios de almacenamiento Blob de Windows Azure.  Sin embargo, el rendimiento depende en varios factores, como el ancho de banda del ISV y el tamaño de la base de datos. Si piensa hacer copia de seguridad de bases de datos o grupos de archivos grandes desde una base de datos de SQL Server local, se recomienda que realice primero algunas pruebas de rendimiento. El [SLA de Almacenamiento](http://azure.microsoft.com/support/legal/sla/storage/v1_0/) de Azure tiene unos tiempos máximos de procesamiento para los blobs que puede tener en cuenta.  
  
-   Usar la opción **WITH COMPRESSION** como se recomienda en la sección **Administrar la copia de seguridad** es muy importante al realizar la copia de seguridad de archivos grandes.  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>Resolución de problemas para realizar la copia de seguridad de una dirección URL o una restauración a partir de esta  
 A continuación se indican algunas formas rápidas de solucionar errores al hacer copia de seguridad o restaurar desde el servicio de almacenamiento Blob de Windows Azure.  
  
 Para evitar errores debidos a opciones no admitidas o a limitaciones, consulte la lista de limitaciones y la información de compatibilidad con los comandos BACKUP y RESTORE del artículo [Copia de seguridad y restauración de SQL Server con el servicio de Almacenamiento de blobs de Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) .  
  
 **Errores de autenticación:**  
  
-   WITH CREDENTIAL es una opción nueva que es necesaria para la copia de seguridad o la restauración con el servicio de almacenamiento Blob de Windows Azure. He aquí algunos errores relacionados con las credenciales:  
  
     La credencial especificada en el comando **BACKUP** o **RESTORE** no existe. Para evitar este problema, puede incluir instrucciones T-SQL para crear la credencial si no existe ninguna en la instrucción de copia de seguridad. He aquí un ejemplo que puede usar:  
  
    ```  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
  
    ```  
  
-   La credencial existe pero la cuenta de inicio de sesión usada para ejecutar el comando de copia de seguridad no tiene permisos de acceso a las credenciales. Use una cuenta de inicio de sesión en el rol **db_backupoperator** con permisos para **Modificar cualquier credencial** .  
  
-   Compruebe los valores de clave y nombre de la cuenta de almacenamiento. La información almacenada en la credencial debe coincidir con los valores de propiedad de la cuenta de almacenamiento de Windows Azure que se usa en las operaciones de copia de seguridad y restauración.  
  
 **Errores de copia de seguridad:**  
  
-   Las copias de seguridad en paralelo en el mismo blob produce errores en una de las copias de seguridad y hacen que aparezca un **Error de inicialización** .  
  
-   Use los registros de errores siguientes como ayuda para solucionar problemas de copia de seguridad:  
  
    -   Establezca la marca de seguimiento 3051 para activar el registro en un registro de errores específico con el siguiente formato en:  
  
         BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log, donde \<action> es uno de los siguientes elementos:  
  
        -   **DB**  
  
        -   **FILELISTONLY**  
  
        -   **LABELONLY**  
  
        -   **HEADERONLY**  
  
        -   **VERIFYONLY**  
  
    -   También puede encontrar información si examina el registro de eventos de Windows, en los registros de aplicación con el nombre 'SQLBackupToUrl'.  
  
-   Al restaurar desde una copia de seguridad comprimida, puede aparecer el siguiente error:  
  
    -   `SqlException 3284 occurred. Severity: 16 State: 5`  
        **Mensaje la marca de archivo en el dispositivo `'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak'` no está alineada. Emita de nuevo la instrucción Restore con el mismo tamaño de bloque usado para crear el conjunto de copia de seguridad: '65536' parece un valor posible.**  
  
         Para resolver este error, vuelva a emitir la instrucción **BACKUP** especificando **BLOCKSIZE = 65536** .  
  
-   Error durante la copia de seguridad porque los blobs tienen una concesión activa: una actividad de copia de seguridad con errores puede dar como resultado blobs con concesiones activas.  
  
     Si se vuelve a intentar una instrucción de copia de seguridad, la operación de copia de seguridad puede producir un error similar al siguiente:  
  
     **BACKUP TO URL recibió una excepción del extremo remoto. Mensaje de excepción: Error en el servidor remoto: (412) Actualmente hay una concesión en el blob y no se especificó ningún identificador de concesión en la solicitud**.  
  
     Si se intenta una instrucción de restauración en un archivo de blob de copia de seguridad que tiene una concesión activa, la operación de restauración produce un error similar al siguiente:  
  
     **Mensaje de la excepción: Error en el servidor remoto: (409) Conflicto.**  
  
     Cuando se produce ese error, es necesario eliminar los archivos de blob. Para obtener más información sobre este escenario y cómo corregir este problema, vea [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md).  
  
## <a name="proxy-errors"></a>Errores de proxy  
 Si usa servidores proxy para tener acceso a Internet, pueden producirse los problemas siguientes:  
  
 **Limitación de la conexión por parte de los servidores proxy:**  
  
 Los servidores proxy pueden tener configuraciones que limitan el número de conexiones por minuto. Copia de seguridad en URL es un proceso multiproceso y, por tanto, puede sobrepasar este límite. Si esto ocurre, el servidor proxy elimina la conexión. Para resolver este problema, cambie la configuración de proxy para que SQL Server no utilice el proxy.   A continuación se muestran algunos ejemplos de los tipos o mensajes de error que puede ver en el registro de errores:  
  
-   Error de escritura en "http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak": BACKUP TO URL recibió una excepción del extremo remoto. Mensaje de excepción: No se pueden leer datos de la conexión de transporte: La conexión se cerró.  
  
-   Error de E/S irrecuperable en el archivo "`http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:`" no se pudo recopilar el Error del extremo remoto.  
  
     Mensaje 3013, nivel 16, estado 1, línea 2  
  
     Fin anómalo de BACKUP DATABASE.  
  
-   BackupIoRequest::ReportIoError: error de escritura en el dispositivo de copia de seguridad http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Error de sistema operativo Copia de seguridad en URL recibió una excepción del extremo remoto. Mensaje de excepción: No se pueden leer datos de la conexión de transporte: La conexión se cerró.  
  
 Si activa el registro detallado mediante la marca de seguimiento 3051, puede ver también el mensaje siguiente en los registros:  
  
 Código de estado HTTP 502, error de proxy del mensaje de estado HTTP (El número de peticiones HTTP por minuto superó el límite configurado. Póngase en contacto con el administrador del servidor ISA.  )  
  
 **Configuración de proxy predeterminada no seleccionada:**  
  
 A veces la configuración predeterminada no se recoge produce errores de autenticación, como se muestra a continuación de proxy:*un error de E/S irrecuperable en el archivo "`http://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:`" Backup to URL recibió una excepción del extremo remoto. Mensaje de excepción: Error en el servidor remoto: (407)* **Se requiere autorización del proxy**.  
  
 Para resolver este problema, cree un archivo de configuración que permita al proceso Copia de seguridad en URL utilizar la configuración de proxy predeterminada mediante los pasos siguientes:  
  
1.  Cree un archivo de configuración denominado BackuptoURL.exe.config con el código XML siguiente:  
  
    ```  
    \<?xml version ="1.0"?>  
    <configuration>   
                    \<system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    \</system.net>  
    </configuration>  
  
    ```  
  
2.  Coloque el archivo de configuración en la carpeta Binn de la instancia de SQL Server. Por ejemplo, si SQL Server está instalado en la unidad C de la máquina, coloque el archivo de configuración aquí: *C:\Archivos de programa\Microsoft SQL Server\MSSQL13.\<nombreDeInstancia>\MSSQL\Binn*.  
  
## <a name="see-also"></a>Vea también  
 [Restaurar a partir de copias de seguridad archivadas en Microsoft Azure](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)
  

