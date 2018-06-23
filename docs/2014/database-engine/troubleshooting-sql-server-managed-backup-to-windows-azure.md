---
title: Solucionar problemas de SQL Server administra la copia de seguridad en Windows Azure | Documentos de Microsoft
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a34d35b0-48eb-4ed1-9f19-ea14754650da
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ffe54aa0c911b659283784196d52f073c772a3af
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103128"
---
# <a name="troubleshooting-sql-server-managed--backup-to-windows-azure"></a>Solucionar problemas de SQL Server administra la copia de seguridad en Windows Azure
  En este tema se describen las tareas y las herramientas que puede usar para solucionar los errores que pueden producirse durante las operaciones de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
## <a name="overview"></a>Información general  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tiene pasos para solucionar problemas y comprobaciones integrados de modo que, en muchos casos, el propio proceso de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] se ocupa de los errores internos.  
  
 Un ejemplo de un caso como este es una eliminación de un archivo de copia de seguridad que da lugar a una interrupción de la cadena de registros que afectan a la capacidad de recuperación: [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] identificará la interrupción en la cadena de registros y programará una copia de seguridad que se realizará inmediatamente. Sin embargo, se recomienda supervisar el estado y solucionar los errores que requieran intervención manual.  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] registra los eventos y los errores usando procedimientos almacenados del sistema, vistas del sistema y eventos extendidos. Las vistas del sistema y los procedimientos almacenados proporcionan información de configuración de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], el estado de las copias de seguridad programadas y también los errores capturados por Eventos extendidos. [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usa Eventos extendidos para capturar los errores que se usan para solucionar problemas. Además de registrar los eventos, las Directivas de administración inteligente de SQL Server proporcionan un estado de mantenimiento que un trabajo de notificación por correo electrónico usa para la notificación de errores y problemas. Para obtener más información, consulte [Monitor de SQL Server Managed Backup to Windows Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md).  
  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] también usa el mismo registro que el utilizado para realizar la copia de seguridad del almacenamiento de Microsoft Azure (Copia de seguridad en URL de SQL Server). Para obtener más información sobre la copia de seguridad en URL relacionados con problemas, vea la sección Solución de problemas en [SQL Server Backup to URL Best Practices y solución de problemas](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
### <a name="general-troubleshooting-steps"></a>Pasos generales para solucionar problemas  
  
1.  Habilite la notificación por correo electrónico para empezar a recibir mensajes de correo electrónico con los errores y advertencias.  
  
     Como alternativa, también puede ejecutar periódicamente `smart_admin.fn_get_health_status` para comprobar los recuentos y los errores agregados. Por ejemplo, `number_of_invalid_credential_errors` es el número de veces que la copia de seguridad inteligente intentó una copia de seguridad pero obtuvo un error de credencial no válida. `Number_of_backup_loops` y `number_of_retention_loops` no son errores pero indican que el número de veces que el subproceso de copia de seguridad y el de retención examinaron la lista de bases de datos. Normalmente, cuando @begin_time y @end_time son no siempre, la función muestra la información de los últimos 30 minutos, normalmente debemos ver los valores distintos de cero para estas dos columnas. Si son cero, implica que el sistema está sobrecargado o incluso que no responde. Para obtener más información, consulte **solucionar problemas del sistema** sección más adelante en este tema.  
  
2.  Revise los registros de Eventos extendidos para obtener más detalles sobre los errores y otros eventos asociados.  
  
3.  Utilice la información de los registros para solucionar el problema.  En caso de un problema o un error del sistema, puede que tenga que reiniciar el servicio del Agente SQL Server.  
  
### <a name="common-causes-of-errors"></a>Causas comunes de los errores  
 A continuación se muestra la lista de las causas comunes que provocan errores:  
  
1.  **Cambios en la credencial de SQL:** si utiliza el nombre de la credencial [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] se cambia o si se elimina, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no será posible realizar copias de seguridad. El cambio se debe aplicar a la configuración de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
2.  **Cambios en los valores de clave de acceso de almacenamiento:** si se cambian los valores de clave de almacenamiento para la cuenta de Windows Azure, pero la credencial de SQL no se actualiza con los nuevos valores, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] se producirá un error al autenticar en el almacenamiento y se produce un error en la copia de seguridad bases de datos configuradas para utilizar esta cuenta.  
  
3.  **Cambios en la cuenta de almacenamiento de Windows Azure:** eliminar o cambiar el nombre de cuenta de almacenamiento sin los cambios correspondientes en la credencial SQL provocará [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] un error y no se realice ninguna copia de seguridad. Si elimina una cuenta de almacenamiento, asegúrese de que las bases de datos se configuran de nuevo con la información válida de la cuenta de almacenamiento. Si se cambia una cuenta de almacenamiento o se cambian los valores de clave, asegúrese de que estos cambios se reflejan en la credencial de SQL que usa [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
4.  **Cambios en las propiedades de la base de datos:** cambios en los modelos de recuperación o el nombre pueden ocasionar errores en las copias.  
  
5.  **Cambios en el modelo de recuperación:** si el modelo de recuperación de la base de datos se cambia a simple de completa u optimizado para cargas masivas, se detendrán las copias de seguridad y omitirá las bases de datos [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para obtener más información, vea [SQL Server Managed Backup to Windows Azure: interoperabilidad y coexistencia](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
### <a name="most-common-error-messages-and-solutions"></a>Mensajes de error y soluciones más comunes  
  
1.  **Errores al habilitar o configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:**  
  
     Error: “No se pudo tener acceso a la dirección URL de almacenamiento…. Proporcione una credencial de SQL válida..." : Se puede ver este y otros errores similares sobre las credenciales SQL.  En casos como este, revise el nombre de la credencial de SQL proporcionado, así como la información almacenada en la credencial de SQL (el nombre de cuenta de almacenamiento y la clave de acceso de almacenamiento) y asegúrese de que son actuales y válidos.  
  
     Error: "... no se puede configurar la base de datos porque es una base de datos": verá este error si intenta habilitar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para una base de datos del sistema.  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no admite copias de seguridad de bases de datos del sistema.  Para configurar la copia de seguridad de una base de datos del sistema, utilice otras tecnologías de copia de seguridad de SQL Server como los planes de mantenimiento.  
  
     Error: "... Proporcione un período de retención …" : Se pueden encontrar errores relacionados con el período de retención si uno no ha especificado un período de retención de la base de datos o la instancia al configurar estos valores por primera vez. También puede ver un error si proporciona un valor distinto de un número entre 1 y 30. El valor válido para el período de retención es un número entre 1 y 30.  
  
2.  **Errores de notificación de correo electrónico:**  
  
     Error: "correo electrónico de base de datos no está habilitado …" : El usuario verá este error si se habilitan las notificaciones de correo electrónico, pero no está configurado el correo electrónico de base de datos en la instancia. Debe configurar Correo electrónico de base de datos en la instancia para poder recibir la notificación del estado de mantenimiento de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Para obtener información acerca de cómo habilitar el correo electrónico de base de datos, vea [configurar correo electrónico de base de datos](../relational-databases/database-mail/configure-database-mail.md). También debe habilitar el Agente SQL Server para utilizar Correo electrónico de base de datos para las notificaciones. Para obtener más información, consulte [antes de comenzar](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md#BeforeYouBegin).  
  
     La siguiente es una lista de números de error que podría ver, que están asociados a notificaciones por correo electrónico:  
  
    -   ErrorNumber: 45209  
  
    -   ErrorNumber: 45210  
  
    -   ErrorNumber: 45211  
  
3.  **Errores de conectividad:**  
  
    -   **Errores relacionados con la conectividad de SQL:** estos errores tienen lugar cuando hay problemas para conectarse a la instancia de SQL Server. Los eventos extendidos exponen estos tipos de errores a través del canal de administración. Estos son los dos eventos extendidos que puede ver si hay errores relacionados con este tipo de problemas de conectividad:  
  
         FileRetentionAdminXEvent con event_type = SqlError. Para obtener detalles de este error, busque los valores de error_code, error_message y stack_trace de ese evento. El error_code es el número de error de SqlException.  
  
         SmartBackupAdminXevent con los siguientes mensajes y prefijos de mensaje:  
  
         *"Se produjo un error interno al configurar la copia de seguridad de SQL Server administrada a la configuración predeterminada de Windows Azure para la instancia. Error puede ser transitorio."*  
  
         *"Probablemente experimentando problemas de conectividad con SQL Server. "Omitiendo la base de datos en la iteración actual."*  
  
         *"No se pudo obtener información de uso de registro de consultas. El error puede ser transitorio. "Omitiendo la base de datos en la iteración actual."*  
  
         *"Excepción de SQL al cargar los metadatos del agente SSMBackup2WA. El error puede ser transitorio. Operación se reintentará."*  
  
         *"SSMBackup2WA encontró excepción de SQL al … "*  
  
    -   **Errores de conexión con la cuenta de almacenamiento:**  
  
         Las excepciones de almacenamiento se notifican en FileRetentionAdminXEvent con el event_type = XstoreError. Para obtener detalles del error, busque los valores de error_message y stack_trace de ese evento.  
  
         Puesto que Copia de seguridad administrada de SQL Server utiliza la tecnología Copia de seguridad en URL subyacente, los errores relacionados con la conectividad al almacenamiento se aplican a ambas funciones. Para obtener más información sobre pasos para solucionar problemas, consulte **sección de solución de problemas** de la [SQL Server Backup to URL Best Practices and Troubleshooting](../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md) artículo.  
  
### <a name="troubleshooting-system-issues"></a>Solucionar problemas del sistema  
 Los siguientes son algunos escenarios cuando hay un problema con el sistema (SQL Server, Agente SQL Server) y afecta a [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]:  
  
-   **Sqlservr.exe deja de responder o deja de funcionar cuando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está ejecutando:** si SQL Server deja de funcionar, Agente SQL se cerrará correctamente, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] también se detiene y los eventos se registran en el archivo SQL Agent.out.  
  
     Si SQL Server deja de responder, los eventos se registran en el canal de administración.  Un ejemplo del registro de eventos:  
  
     *Error de SQL (motor no responde u obtener sqlException: SqlException:*   
     *seguimiento de la pila, el mensaje y el código de error se mostrará en un canal de administración xevent, junto con cierta información adicional, como:*   
    *"Probablemente experimentando problemas de conectividad con SQL Server. "Omitiendo la base de datos en la iteración actual"*  
  
-   **Agente SQL deja de responder o deja de funcionar cuando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está ejecutando:**  
  
     Si el Agente SQL deja de funcionar, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] también se detiene y los eventos se registran en el canal de administración. Esto es similar a los escenarios en los que SQL Server deja de responder.  
  
     Si el Agente SQL deja de responder, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no podrá continuar con las operaciones de copia de seguridad y los eventos se registran en el canal de administración. Un ejemplo del registro de eventos:  
  
     *Trabajo no responde: vea los xevents del canal de administración*   
    *"No se ha recibido una actualización de progreso de SQL Server en más de" + Constants.DBBackupInfoMsgMaxWaitTime + "horas para la copia de seguridad de base de datos.   Copia de seguridad de nube de SSM continuará esperando."*  
  
 Si ha habilitado la notificación por correo electrónico, recibirá una notificación que incluya **número de bucles de copia de seguridad** y **número de bucles de retención**. Si el valor devuelto en la notificación para una o ambas columnas es cero, podría ser una indicación de que el sistema no responde.  
  
> [!WARNING]  
>  Los procesos internos que generan los resultados del informe suponen que los registros de diagnóstico del motor están en la misma ubicación que el registro de errores del Agente SQL, que de forma predeterminada se encuentra en la misma carpeta que los registros de errores de la instancia de SQL Server. Si los registros de diagnóstico del motor se mueven a una ubicación distinta de la ubicación del registro de errores del Agente SQL, el sistema no encuentra los registros de diagnóstico de copia de seguridad inteligente y, por tanto, el informe de la notificación por correo electrónico quizás no sea correcto. Por ejemplo, podría ver un valor de **0** en todos los campos notificados, incluido el número de bucles de copia de seguridad y el número de bucles de retención. En este caso donde los registros de diagnóstico se mueven a una ubicación diferente, puede no indicar que el sistema no responde, sino que el sistema no encuentra los registros. Asegúrese primero de que la ubicación de los registros de diagnóstico y los registros de errores del Agente SQL están en la misma ubicación. Para comprobar la ubicación actual de los registros de diagnóstico, puede usar [sys.dm_os_server_diagnostics_log_configurations](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-server-diagnostics-log-configurations). La `path` columna devuelve la ubicación actual del motor de registros de diagnóstico.  Debe estar en la misma carpeta que los registros de errores del Agente SQL. Puede obtener la ruta de acceso del registro de errores del Agente SQL mediante el procedimiento almacenado `dbo.sp_get_sqlagent_properties`.  
  
 Compruebe los registros de eventos extendidos para ver los detalles de los errores. Corrija los errores o reinicie el Agente SQL Server para corregir la situación.  
  
  
