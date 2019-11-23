---
title: Solución de problemas de SQL Server copia de seguridad administrada en Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: a34d35b0-48eb-4ed1-9f19-ea14754650da
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cbdf7f9b9e8a428ed3d3bf6bfcfe14dbd7da68fc
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153933"
---
# <a name="troubleshooting-sql-server-managed--backup-to-azure"></a>Solución de problemas de la copia de seguridad administrada de SQL Server en Azure
  En este tema se describen las tareas y las herramientas que puede usar para solucionar los errores que pueden producirse durante las operaciones de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
## <a name="overview"></a>Información general  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tiene pasos para solucionar problemas y comprobaciones integrados de modo que, en muchos casos, el propio proceso de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] se ocupa de los errores internos.  
  
 Por ejemplo, una eliminación de un archivo de copia de seguridad que da lugar a una interrupción de la cadena de registro que afecta a la capacidad de recuperación: [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] identificará la interrupción en la cadena de registros y programará una copia de seguridad para que se realice inmediatamente. Sin embargo, se recomienda supervisar el estado y solucionar los errores que requieran intervención manual.  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] registra los eventos y los errores usando procedimientos almacenados del sistema, vistas del sistema y eventos extendidos. Las vistas del sistema y los procedimientos almacenados proporcionan información de configuración de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], el estado de las copias de seguridad programadas y también los errores capturados por Eventos extendidos. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usa Eventos extendidos para capturar los errores que se usan para solucionar problemas. Además de registrar los eventos, las Directivas de administración inteligente de SQL Server proporcionan un estado de mantenimiento que un trabajo de notificación por correo electrónico usa para la notificación de errores y problemas. Para obtener más información, consulte [supervisión SQL Server copia de seguridad administrada en Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] también usa el mismo registro que se usa cuando se realiza una copia de seguridad manual en Azure Storage (SQL Server copia de seguridad en dirección URL). Para obtener más información acerca de los problemas relacionados con la copia de seguridad en URL, consulte la sección solución de problemas de [SQL Server procedimientos recomendados y solución de problemas de copia de seguridad en URL](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) .  
  
### <a name="general-troubleshooting-steps"></a>Pasos generales para solucionar problemas  
  
1.  Habilite la notificación por correo electrónico para empezar a recibir mensajes de correo electrónico con los errores y advertencias.  
  
     Como alternativa, también puede ejecutar periódicamente `smart_admin.fn_get_health_status` para comprobar los recuentos y los errores agregados. Por ejemplo, `number_of_invalid_credential_errors` es el número de veces que la copia de seguridad inteligente intentó una copia de seguridad pero obtuvo un error de credencial no válida. `Number_of_backup_loops` y `number_of_retention_loops` no son errores pero indican que el número de veces que el subproceso de copia de seguridad y el de retención examinaron la lista de bases de datos. Normalmente, cuando no se proporcionan @begin_time y @end_time, la función muestra la información de los últimos 30 minutos y, por lo general, deberíamos ver valores distintos de cero para estas dos columnas. Si son cero, implica que el sistema está sobrecargado o incluso que no responde. Para obtener más información, consulte la sección **solución de problemas del sistema** más adelante en este tema.  
  
2.  Revise los registros de Eventos extendidos para obtener más detalles sobre los errores y otros eventos asociados.  
  
3.  Utilice la información de los registros para solucionar el problema.  En caso de un problema o un error del sistema, puede que tenga que reiniciar el servicio del Agente SQL Server.  
  
### <a name="common-causes-of-errors"></a>Causas comunes de los errores  
 A continuación se muestra la lista de las causas comunes que provocan errores:  
  
1.  **Cambios en la credencial de SQL:** Si cambia el nombre de la credencial usada por [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] o si se elimina, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no podrá realizar copias de seguridad. El cambio se debe aplicar a la configuración de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
2.  **Cambios en los valores de clave de acceso de almacenamiento:** Si se cambian los valores de clave de almacenamiento de la cuenta de Azure, pero la credencial de SQL no se actualiza con los nuevos valores, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] producirá un error al autenticarse en el almacenamiento y no se realizarán copias de seguridad de las bases de datos configuradas para usar esta cuenta.  
  
3.  **Cambios en la cuenta de Azure Storage:** Si elimina o cambia el nombre de la cuenta de almacenamiento sin los cambios correspondientes en la credencial SQL, se producirá un error en [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] y no se realizará ninguna copia de seguridad. Si elimina una cuenta de almacenamiento, asegúrese de que las bases de datos se configuran de nuevo con la información válida de la cuenta de almacenamiento. Si se cambia una cuenta de almacenamiento o se cambian los valores de clave, asegúrese de que estos cambios se reflejan en la credencial de SQL que usa [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
4.  **Cambios en las propiedades de la base de datos:** Los cambios en los modelos de recuperación o en el cambio de nombre pueden hacer que se produzca un error en las copias de seguridad.  
  
5.  **Cambios en el modelo de recuperación:** Si el modelo de recuperación de la base de datos se cambia a simple desde completo u optimizado para cargas masivas de registro, se detendrán las copias de seguridad y [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]omitirán las bases de datos. Para obtener más información, consulte [SQL Server copia de seguridad administrada en Azure: interoperabilidad y coexistencia](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>Mensajes de error y soluciones más comunes  
  
1.  **Errores al habilitar o configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:**  
  
     Error: "no se pudo obtener acceso a la dirección URL de almacenamiento.... Proporcione una credencial SQL válida... ": puede ver este y otros errores similares relacionados con las credenciales de SQL.  En tales casos, revise el nombre de la credencial de SQL que proporcionó, así como la información almacenada en la credencial de SQL: el nombre de la cuenta de almacenamiento y la clave de acceso de almacenamiento, y asegúrese de que son actuales y válidos.  
  
     Error: "... no se puede configurar la base de datos.... como es una base de datos del sistema ": verá este error si intenta habilitar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para una base de datos del sistema.  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no admite copias de seguridad de bases de datos del sistema.  Para configurar la copia de seguridad de una base de datos del sistema, utilice otras tecnologías de copia de seguridad de SQL Server como los planes de mantenimiento.  
  
     Error: "... Proporcionar un período de retención.... ": puede ver errores relacionados con el período de retención Si no ha especificado un período de retención para la base de datos o la instancia de al configurar estos valores por primera vez. También puede ver un error si proporciona un valor distinto de un número entre 1 y 30. El valor válido para el período de retención es un número entre 1 y 30.  
  
2.  **Errores de notificación por correo electrónico:**  
  
     Error: "Correo electrónico de base de datos no está habilitado...": verá este error si habilita las notificaciones por correo electrónico, pero Correo electrónico de base de datos no está configurado en la instancia. Debe configurar Correo electrónico de base de datos en la instancia para poder recibir la notificación del estado de mantenimiento de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para obtener información sobre cómo habilitar correo electrónico de base de datos, vea [configurar correo electrónico de base de datos](../relational-databases/database-mail/configure-database-mail.md). También debe habilitar el Agente SQL Server para utilizar Correo electrónico de base de datos para las notificaciones. Para obtener más información, vea [antes de empezar](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin).  
  
     La siguiente es una lista de números de error que podría ver, que están asociados a notificaciones por correo electrónico:  
  
    -   Númeroerror: 45209  
  
    -   Númeroerror: 45210  
  
    -   ErrorNumber: 45211  
  
3.  **Errores de conectividad:**  
  
    -   **Errores relacionados con la conectividad de SQL:** Estos errores se producen cuando hay problemas para conectarse a SQL Server instancia. Los eventos extendidos exponen estos tipos de errores a través del canal de administración. Estos son los dos eventos extendidos que puede ver si hay errores relacionados con este tipo de problemas de conectividad:  
  
         FileRetentionAdminXEvent con event_type = SqlError. Para obtener detalles de este error, busque los valores de error_code, error_message y stack_trace de ese evento. El error_code es el número de error de SqlException.  
  
         SmartBackupAdminXevent con los siguientes mensajes y prefijos de mensaje:  
  
         *"Se produjo un error interno al configurar SQL Server copia de seguridad administrada en la configuración predeterminada de Azure para la instancia. El error puede ser transitorio. "*  
  
         *"Es probable que experimente problemas de conectividad con SQL Server. Omitiendo la base de datos en la iteración actual. "*  
  
         *"Error al consultar la información de uso del registro. El error puede ser transitorio. Omitiendo la base de datos en la iteración actual. "*  
  
         *"Se encontró una excepción de SQL al cargar los metadatos del agente SSMBackup2WA. El error puede ser transitorio. Se volverá a intentar la operación ".*  
  
         *"SSMBackup2WA encontró una excepción de SQL... "*  
  
    -   **Errores al conectarse a la cuenta de almacenamiento:**  
  
         Las excepciones de almacenamiento se notifican en FileRetentionAdminXEvent con el event_type = XstoreError. Para obtener detalles del error, busque los valores de error_message y stack_trace de ese evento.  
  
         Puesto que Copia de seguridad administrada de SQL Server utiliza la tecnología Copia de seguridad en URL subyacente, los errores relacionados con la conectividad al almacenamiento se aplican a ambas funciones. Para obtener más información sobre los pasos de solución de problemas, consulte la **sección solución de problemas** de los [procedimientos recomendados y solución de problemas de copia de seguridad en URL de SQL Server](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) .  
  
### <a name="troubleshooting-system-issues"></a>Solucionar problemas del sistema  
 Los siguientes son algunos escenarios cuando hay un problema con el sistema (SQL Server, Agente SQL Server) y afecta a [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:  
  
-   **Sqlservr. exe deja de responder o deja de funcionar cuando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está en ejecución:** Si SQL Server deja de funcionar, el Agente SQL se cerrará correctamente, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] también se detiene y los eventos se registran en el archivo. out del Agente SQL.  
  
     Si SQL Server deja de responder, los eventos se registran en el canal de administración.  Un ejemplo del registro de eventos:  
  
     *Error de SQL (el motor no responde u obtener SqlException: SqlException:*    
     el *código de error, el mensaje y el seguimiento de seguimiento se mostrarán en un XEvent del canal de administración, junto con información adicional, como:*    
    *"Es probable que experimente problemas de conectividad con SQL Server. Omitiendo la base de datos en la iteración actual "*  
  
-   **El Agente SQL deja de responder o deja de funcionar cuando se está ejecutando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:**  
  
     Si el Agente SQL deja de funcionar, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] también se detiene y los eventos se registran en el canal de administración. Esto es similar a los escenarios en los que SQL Server deja de responder.  
  
     Si el Agente SQL deja de responder, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no podrá continuar con las operaciones de copia de seguridad y los eventos se registran en el canal de administración. Un ejemplo del registro de eventos:  
  
     Los *trabajos se bloquean: Consulte canal de administración xevents*   
    *"No se ha recibido una actualización de progreso de SQL Server en más de" + constantes. DBBackupInfoMsgMaxWaitTime + "horas para la copia de seguridad de base de datos.   La copia de seguridad en la nube de SSM seguirá esperando. "*  
  
 Si ha habilitado la notificación por correo electrónico, recibirá una notificación que incluya el **Número de bucles de copia de seguridad** y el **Número de bucles de retención**. Si el valor devuelto en la notificación para una o ambas columnas es cero, podría ser una indicación de que el sistema no responde.  
  
> [!WARNING]  
>  Los procesos internos que generan los resultados del informe suponen que los registros de diagnóstico del motor están en la misma ubicación que el registro de errores del Agente SQL, que de forma predeterminada se encuentra en la misma carpeta que los registros de errores de la instancia de SQL Server. Si los registros de diagnóstico del motor se mueven a una ubicación distinta de la ubicación del registro de errores del Agente SQL, el sistema no encuentra los registros de diagnóstico de copia de seguridad inteligente y, por tanto, el informe de la notificación por correo electrónico quizás no sea correcto. Por ejemplo, podría ver un valor de **0** en todos los campos notificados, incluido el Número de bucles de copia de seguridad y el Número de bucles de retención. En este caso donde los registros de diagnóstico se mueven a una ubicación diferente, puede no indicar que el sistema no responde, sino que el sistema no encuentra los registros. Asegúrese primero de que la ubicación de los registros de diagnóstico y los registros de errores del Agente SQL están en la misma ubicación. Para comprobar la ubicación actual de los registros de diagnóstico, puede usar [Sys. dm_os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations). La columna `path` devuelve la ubicación actual de los registros de diagnóstico del motor.  Debe estar en la misma carpeta que los registros de errores del Agente SQL. Puede obtener la ruta de acceso del registro de errores del Agente SQL mediante el procedimiento almacenado `dbo.sp_get_sqlagent_properties`.  
  
 Compruebe los registros de eventos extendidos para ver los detalles de los errores. Corrija los errores o reinicie el Agente SQL Server para corregir la situación.  
  
  
