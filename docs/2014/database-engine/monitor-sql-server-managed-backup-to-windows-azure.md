---
title: Supervisión de SQL Server copia de seguridad administrada en Azure | Microsoft Docs
description: En este artículo se describen las herramientas que puede usar para determinar el estado general de las copias de seguridad con SQL Server copia de seguridad administrada en Azure e identificar los errores.
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: cfb9e431-7d4c-457c-b090-6f2528b2f315
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: baec99e63c70befde0cfce76e42dd6202ebc0bad
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930646"
---
# <a name="monitor-sql-server-managed-backup-to-azure"></a>Supervisión de copia de seguridad administrada de SQL Server en Azure
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tiene medidas integradas para identificar los problemas y los errores durante los procesos de copia de seguridad y remediarlos con la acción correctiva, si es posible.  Aunque hay ciertas situaciones en las que se requiere la intervención del usuario. Este tema describe las herramientas que puede utilizar para determinar el estado de mantenimiento total de las copias de seguridad e identificar los errores que deban solucionarse.  
  
## <a name="overview-of-ss_smartbackup-built-in-debugging"></a>Introducción a la depuración integrada de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 El [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] revisa periódicamente las copias de seguridad programadas e intenta volver a programar las que no se hayan podido realizar. Sondea periódicamente la cuenta de almacenamiento para identificar las interrupciones en las cadenas de registros que afectan a la capacidad de recuperación de la base de datos y programa las nuevas copias de seguridad en consecuencia. También tiene en cuenta las directivas de limitación de Azure y tiene mecanismos para administrar varias copias de seguridad de bases de datos. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usa eventos extendidos para realizar el seguimiento de todas las actividades. Los canales de eventos extendidos que usa el agente [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] son el de administración, operativo, analítico y depuración. Los eventos que entran en la categoría de administración suelen relacionarse con errores y requerir la intervención del usuario y se habilitan de forma predeterminada. Los eventos analíticos se activan de forma predeterminada pero por lo general no están relacionados con errores que requieran la intervención del usuario. Los eventos operativos suelen ser informativos. Por ejemplo, los eventos operativos incluyen la programación de una copia de seguridad, la finalización correcta de una copia de seguridad, etc. La depuración es la más detallada y se usa internamente [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para determinar los problemas y corregirlos si es necesario.  
  
### <a name="configure-monitoring-parameters-for-ss_smartbackup"></a>Configurar parámetros de supervisión para [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 El procedimiento almacenado del sistema **smart_admin. sp_set_parameter** le permite especificar la configuración de supervisión. En las secciones siguientes se recorre el proceso para habilitar Eventos extendidos y para habilitar la notificación por correo electrónico de los errores y las advertencias.  
  
 La función **smart_admin. fn_get_parameter** se puede utilizar para obtener la configuración actual de un parámetro concreto o de todos los parámetros configurados. Si los parámetros no se han configurado nunca, la función no devuelve ningún valor.  
  
1.  Conéctese con el [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el ejemplo siguiente en la ventana de consulta y, a continuación, haga clic en **Ejecutar**. De este modo se devuelve la configuración actual de Eventos extendidos y las notificaciones por correo electrónico.  
  
```sql
Use msdb  
Go  
SELECT * FROM smart_admin.fn_get_parameter (NULL)  
GO  
```  
  
 Para obtener más información, vea [smart_admin. fn_get_parameter &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)  
  
### <a name="extended-events-for-monitoring"></a>Eventos extendidos para la supervisión  
 De forma predeterminada, los eventos de administración, operativos y analíticos están activados. Los eventos de administración son los más importantes, útiles para identificar los errores que requieren intervención manual para solucionar el problema. Puede ser conveniente activar los eventos operativos y de depuración pero debe tener en cuenta que son muy detallados y pueden requerir un filtrado. Los procedimientos siguientes describen cómo supervisar los eventos registrados mediante Eventos extendidos.  
  
> [!IMPORTANT]  
>  A diferencia de Eventos extendidos para el Motor SQL, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no admite los conceptos relativos a la sesión de Eventos extendidos. Las funciones y los procedimientos almacenados del sistema son las herramientas que se usan para interactuar con los eventos extendidos. También puede ver el registro de eventos extendidos desde el directorio de registro.  
  
##### <a name="to-configure-and-view-extended-events"></a>Para configurar y ver Eventos extendidos  
  
1.  Para ver los canales de Eventos extendidos disponibles y su estado actual ejecutando la siguiente consulta:  
  
    ```sql
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     El resultado de esta consulta mostrará el event_name, si es configurable o no, y si está habilitado.  Para obtener más información, vea [smart_admin. fn_get_current_xevent_settings &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql).  
  
2.  Para habilitar los eventos de depuración, ejecute la consulta siguiente:  
  
    ```sql
    --  to enable debug events  
    Use msdb;  
    GO 
    EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
     Para obtener más información acerca del procedimiento almacenado, vea [smart_admin. sp_set_parameter &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql).  
  
3.  Para ver los eventos registrados, ejecute la consulta siguiente:  
  
    ```sql
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;
    ```  
  
    ```sql
    --  view all admin events  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'
    ```  
  
### <a name="aggregated-error-countshealth-status"></a>Estado de mantenimiento y recuentos de errores agregados  
 La función **smart_admin. fn_get_health_status** devuelve una tabla de recuentos de errores agregados para cada categoría que se puede usar para supervisar el estado de mantenimiento de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] . Esta misma función también la utiliza el mecanismo de notificación por correo electrónico configurado en el sistema que se describe más adelante en este tema.   
Estos recuentos agregados se pueden utilizar para supervisar el estado del sistema. Por ejemplo, si el number_ of_retention_loops columna es 0 en 30 minutos, es posible que la administración de la retención tarde mucho tiempo o incluso no funcione correctamente. Las columnas de errores que no son cero pueden indicar que hay problemas y los registros de Eventos extendidos se deben comprobar para detectarlos. También puede llamar a **smart_admin. sp_get_backup_diagnostics** procedimiento almacenado para buscar los detalles del error.  
  
### <a name="using-agent-notification-for-assessing-backup-status-and-health"></a>Usar la notificación del agente para evaluar el estado de la copia de seguridad y los estados  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] incluye un mecanismo de notificación que se fundamenta en las directivas de administración basada en directivas de SQL Server.  
  
 **Requisitos previos:**  
  
-   Para usar esta funcionalidad, se requiere el Correo electrónico de base de datos. Para obtener más información acerca de cómo habilitar el correo electrónico de base de datos para la instancia de SQL Server, vea [configurar correo electrónico de base de datos](../relational-databases/database-mail/configure-database-mail.md).  
  
-   Las propiedades del sistema de alertas del Agente SQL Server se deben establecer para utilizar el Correo electrónico de base de datos.  
  
 **Arquitectura de notificación:**  
  
-   **Administración basada en directivas:** Se establecen dos directivas para supervisar el estado de la copia de seguridad: **Directiva de mantenimiento del sistema de administración inteligente**y la **Directiva de estado de acción de usuario de administrador inteligente**. La directiva de estado del sistema de Administración inteligente evalúa los errores críticos como la falta de credenciales de SQL o si no son válidas y los errores de conectividad y notifica el estado del sistema. Se suele requerir intervención para solucionar el problema subyacente. La directiva de estado de acción del usuario de Administración inteligente evalúa las advertencias, por ejemplo las copias de seguridad dañadas.  Estas pueden no requerir ninguna intervención sino que solo son una advertencia de un evento. Se espera que el agente [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] se ocupe de tales problemas.  
  
-   **Agente SQL Server** Trabajo: la notificación se realiza mediante un trabajo Agente SQL Server que tiene tres pasos de trabajo. En el primer paso, detecta si [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está configurado para una base de datos o una instancia. Si encuentra [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado y configurado, realiza el segundo paso: ejecuta el cmdlet de PowerShell que evalúa el estado evaluando las directivas de administración basada en directivas de SQL Server. Si detecta un error o una advertencia, da error y desencadena el tercer paso: envía una notificación por correo electrónico con el informe de la advertencia o el error.  Sin embargo, este trabajo del Agente SQL Server no está habilitado de forma predeterminada. Para habilitar el trabajo de notificación de correo electrónico, utilice el procedimiento almacenado del sistema **smart_admin. sp_set_backup_parameter** .  En el siguiente procedimiento se describen los pasos detalladamente:  
  
##### <a name="enabling-email-notification"></a>Habilitar la notificación por correo electrónico  
  
1.  Si aún no se ha configurado Correo electrónico de base de datos, siga los pasos descritos en [configurar correo electrónico de base de datos](../relational-databases/database-mail/configure-database-mail.md).  
  
2.  Establecer la base de datos como sistema de correo para SQL Server sistema de alerta: haga clic con el botón secundario en **Agente SQL Server**, seleccione **sistema de alerta**, active la casilla **Habilitar perfil de correo** , seleccione **correo electrónico de base de datos** como **sistema de correo**y seleccione un perfil de correo creado previamente.  
  
3.  Ejecute la consulta siguiente en una ventana de consulta y proporcione la dirección de correo electrónico a la que desea que se envíe la notificación:  
  
    ```sql
    Use msdb  
    Go  
    EXEC smart_admin.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'
    ```  
  
     Así se crea un trabajo del Agente SQL Server que se utiliza para recopilar el estado y enviar notificaciones cuando se produce un error o un problema con las copias de seguridad.  
  
 A continuación se muestra un script de ejemplo para habilitar Correo electrónico de base de datos y configurar la notificación por correo electrónico mediante el trabajo del Agente SQL Server  
  
```sql
-- Prereq: Make sure that SQL Server service runs in a service account that has  
--  access to SMTP Server   
-- set SQL Server service account as domain account   
  
EXEC sp_configure 'show advanced', 1  
RECONFIGURE  
GO  
  
-- Enable DBMail  
EXEC sp_configure 'Database Mail XPs',1  
GO  
RECONFIGURE  
GO  
  
-- Configure DBMail  
DECLARE @emailid NVARCHAR(255)  
-- Note: change this email to your own email id  
SET @emailid = N'emailalias@mycompany.com'  
  
DECLARE @smtpserver NVARCHAR(255)  
SET @smtpserver = N'smtphost.domainname.com'  
  
DECLARE @mailprofile NVARCHAR(255)  
SET @mailprofile = N'my_profile'  
  
EXEC msdb.dbo.sysmail_add_account_sp @account_name=N'myaccount',  
                @email_address = @emailid,  
                @replyto_address = @emailid,  
                @mailserver_name = @smtpserver,  
                @use_default_credentials = 1  
  
EXEC msdb.dbo.sysmail_add_profile_sp @profile_name=@mailprofile  
EXEC msdb.dbo.sysmail_add_profileaccount_sp @profile_name=@mailprofile, @account_name=N'myaccount', @sequence_number=1  
  
-- Set SQL Agent to use DBMail profile  
EXEC msdb.dbo.sp_set_sqlagent_properties @databasemail_profile = @mailprofile  
  
-- Configure Notifications   
EXEC msdb.smart_admin.sp_set_parameter  
@parameter_name = 'SSMBackup2WANotificationEmailIds',  
@parameter_value = @emailid  
  
-- To test is you are receiving notifications  
-- delete few backup files from your storage container, Wait for 15 minutes & see if you get any email notification
```  
  
### <a name="using-powershell-to-setup-custom-health-monitoring"></a>Usar PowerShell para configurar la supervisión personalizada del estado  
 El cmdlet **Test-SqlSmartAdmin** se puede usar para crear una supervisión de estado personalizada. Por ejemplo, la opción de notificación descrita en la sección anterior se puede configurar en el nivel de instancia.  Si tiene varias instancias de SQL Server configuradas para utilizar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], el cmdlet de PowerShell se puede utilizar para crear scripts y recopilar el estado de las copias de seguridad de todas las instancias.  
  
 El cmdlet **Test-SqlSmartAdmin** evalúa los errores y las advertencias que devuelve el SQL Server directivas de administración basadas en directivas y notifica el estado acumulado.  De forma predeterminada, este cmdlet utiliza las directivas del sistema. Para incluir una directiva personalizada, utilice el parámetro `-AllowUserPolicies`.  
  
 A continuación se muestra un script de PowerShell de ejemplo que devuelve un informe de los errores y las advertencias basados en las directivas de sistema y de las directivas de usuario creadas:  
  
```powershell
$policyResults = Get-SqlSmartAdmin | Test-SqlSmartAdmin -AllowUserPolicies  
$policyResults.PolicyEvaluationDetails | Select Name, Category, Expression, Result, Exception | fl
```  
  
 El script siguiente devuelve un informe detallado de los errores y advertencias de la instancia predeterminada ( `\SQL\COMPUTER\DEFAULT` ):  
  
```powershell
(Get-SqlSmartAdmin ).EnumHealthStatus()  
```  
  
### <a name="objects-in-msdb-database"></a>Objetos de la base de datos MSDB  
 Hay objetos que se instalan para implementar la funcionalidad. Estos objetos están reservados para uso interno. Sin embargo, hay una tabla del sistema que puede ser útil a la hora supervisar el estado de la copia de seguridad: smart_backup_files. La mayor parte de la información almacenada en esta tabla relevante para la supervisión como el tipo de copia de seguridad, el nombre de la base de datos, el primer y último LSN, las fechas de expiración de copia de seguridad se exponen a través de la función del sistema [smart_admin&#41;&#40;fn_available_backups. ](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql) No obstante, la columna state de la tabla smart_backup_files que indica el estado del archivo de copia de seguridad no está disponible con esa función. A continuación se muestra una consulta de ejemplo que puede utilizar para recuperar cierta información, incluido el estado de la tabla del sistema:  
  
```sql
USE msdb  
GO  
SELECT  
 database_name AS [Database Name] ,backup_path AS [Backup Destination and File]  
,[Backup Type] =  
CASE backup_type  
WHEN 1 THEN 'FULL'  
WHEN 2 THEN 'LOG'  
END  
,[Backup Status] =  
CASE [status]  
WHEN 'A' THEN 'Available'  
WHEN 'B' THEN 'Copy In Progress'  
WHEN 'C' THEN 'Corrupted'  
WHEN 'D' THEN 'Deleted'  
WHEN 'F' THEN 'Copy Failed'  
WHEN 'U' THEN 'Unknown'  
END  
,first_lsn AS [First LSN]  
,last_lsn AS [Last LSN]  
,backup_start_date AS [Backup Start Time]  
,backup_finish_date AS [Backup Completion Time]  
,expiration_date AS [Backup Expiry Date/Time]  
FROM  
smart_backup_files;
```  
  
 A continuación se muestra una explicación detallada de los distintos estados devueltos:  
  
-   **Disponible** : Se trata de un archivo de copia de seguridad normal. La copia de seguridad se ha completado y también se ha comprobado que está disponible en Azure Storage.  
  
-   **Copia en curso-B:** Este estado es específico para las bases de datos del grupo de disponibilidad. Si [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] detecta una interrupción en la cadena de registro de copia de seguridad, primero intentará identificar la copia de seguridad que pueda haber producido la interrupción en la cadena de copias de seguridad. Al buscar el archivo de copia de seguridad, intenta copiar el archivo en Azure Storage. Cuando el proceso de copia está en curso, muestra este estado.  
  
-   **Error de copia-F:** De forma similar a la copia en curso, se trata de bases de datos de grupos de disponibilidad t específicas. Si se produce un error en el proceso de copia, se marca el estado como F.  
  
-   **Dañado-C:** Si [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no puede comprobar el archivo de copia de seguridad en el almacenamiento mediante la realización de un comando restore HEADER_ONLY incluso después de varios intentos, marca este archivo como dañado. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] programará una copia de seguridad para asegurarse de que el archivo dañado no produce una interrupción de la cadena de copia de seguridad.  
  
-   **Eliminado-D:** No se encuentra el archivo correspondiente en Azure Storage. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] programará una copia de seguridad si el archivo eliminado produce una interrupción en la cadena de copia de seguridad.  
  
-   **Desconocido-U:** Este estado indica que [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] aún no se ha podido comprobar la existencia de archivos y sus propiedades en Azure Storage. La próxima vez que se ejecute el proceso, que es aproximadamente cada 15 minutos, se actualizará este estado.  
