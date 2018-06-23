---
title: 'Copia de seguridad en Windows Azure administradas de SQL Server: interoperabilidad y coexistencia | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 78fb78ed-653f-45fe-a02a-a66519bfee1b
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4da5bf7083be26f12a140bf5b3465882e150b215
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108414"
---
# <a name="sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence"></a>Copia de seguridad administrada de SQL Server en Microsoft Azure: interoperabilidad y coexistencia
  En este tema se describen la interoperabilidad y la coexistencia de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] con varias características de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Estas características son: Grupos de disponibilidad AlwaysOn, creación de reflejo de la base de datos, planes de mantenimiento de copia de seguridad, trasvase de registros, copias de seguridad ad hoc, separar base de datos y quitar base de datos.  
  
### <a name="alwayson-availability-groups"></a>Grupos de disponibilidad AlwaysOn  
 Los Grupos de disponibilidad AlwaysOn configurados como una solución solo de Windows Azure admitida para [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Las configuraciones solo en local o Grupo de disponibilidad AlwaysOn híbrido no se admiten. Para obtener más información y otras consideraciones, consulte [configurar SQL Server Managed Backup to Windows Azure para grupos de disponibilidad](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)  
  
### <a name="database-mirroring"></a>Creación de reflejo de base de datos  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] solo se admite en la base de datos principal. Si configura tanto la entidad de seguridad como el reflejo para utilizar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], la base de datos reflejada se omite y no se realiza su copia de seguridad. Sin embargo, en caso de conmutación por error, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] iniciará el proceso de copia de seguridad una vez que el reflejo haya completado la conmutación de roles y esté en línea. Las copias de seguridad se almacenarán en un nuevo contenedor en este caso. Si el reflejo no está configurado para utilizar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], en caso de que se produzca una conmutación por error, no se realiza ninguna copia de seguridad. Se recomienda configurar [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] tanto en la entidad de seguridad como en el reflejo de modo que las copias de seguridad continúen en caso de que se produzca una conmutación por error.  
  
> [!TIP]  
>  Si va a crear una base de datos reflejada en una instancia con la configuración predeterminada de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], puede ser preferible deshabilitar los valores predeterminados de la instancia de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], por lo que no se aplican a la base de datos reflejada, y después volver a habilitar los valores predeterminados de la instancia tras configurar la entidad de seguridad y el reflejo.  
  
### <a name="maintenance-plan"></a>Plan de mantenimiento  
 No se permite el uso de planes de mantenimiento para crear copias de seguridad de una base de datos cuando se habilita [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]. Los planes de mantenimiento ocasionarán que la cadena de registros se interrumpa y [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] no pueda admitir la capacidad de recuperación garantizada de la base de datos durante la restauración. Esto también se aplica cuando [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] está habilitado en el nivel de instancia.  
  
> [!TIP]  
>  Se admiten planes de mantenimiento con copias de seguridad de solo copia con [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] configurado para la misma base de datos o instancia.  
  
### <a name="log-shipping"></a>Trasvase de registros  
 No puede configurar el trasvase de registros y [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para la misma base de datos al mismo tiempo. Si hace esto, afectará a las capacidades de recuperación de la base de datos con cualquier funcionalidad.  
  
### <a name="ad-hoc-backups-using-transact-sql-and-sql-server-management-studio"></a>Copias de seguridad ad hoc con Transact-SQL y SQL Server Management Studio  
 Las copias de seguridad ad hoc o de una vez creadas fuera de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] con Transact-SQL o SQL Server Management Studio pueden afectar al proceso de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] según el tipo de copia de seguridad y los medios de almacenamiento utilizados. Las copias de seguridad de registros en otra cuenta de almacenamiento de Windows Azure diferente de la que [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] usa o cualquier otro destino que no sea el servicio de almacenamiento Blob de Windows Azure ocasionarán una interrupción de la cadena de registros. Se recomienda que realice la [smart_admin.sp_backup_on_demand &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) procedimiento almacenado para iniciar una copia de seguridad en las bases de datos [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitado. Puede iniciar una base de datos completa o la copia de seguridad de registros mediante este procedimiento almacenado.  
  
### <a name="drop-database-and-detach-database"></a>Quitar la base de datos y separar la base de datos  
 Si se quita o se separa una base de datos que tenga habilitada [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], aunque no se pueda realizar copias de seguridad adicionales, las copias de seguridad anteriores permanecen en el almacenamiento hasta que haya transcurrido el período de retención, momento en que las copias de seguridad se purgarán.  
  
### <a name="changes-to-recovery-model"></a>Cambios del modelo de recuperación  
  
-   Si cambia el modelo de recuperación de una base de datos **Simple** a **completa** o **Bulk-Logged**, tiene la opción de configuración [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para la base de datos. Se considerará una base de datos nueva desde la perspectiva de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)].  
  
-   Si cambia el modelo de recuperación de una base de datos **completa** o **Bulk-Logged** a **Simple**, cuya [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ya no estará habilitadas, copia de seguridad de las operaciones programado. La configuración del periodo de retención estará todavía activa y los archivos de copia de seguridad permanecerán en la cuenta de almacenamiento hasta que haya transcurrido el período de retención. Si desea conservar las copias de seguridad, se recomienda descargar los archivos en una cuenta de almacenamiento diferente o en una ubicación local. Los valores de configuración se conservan y se puede reutilizar si el modelo de recuperación se vuelve a establecer en **completa** o **Bulk-Logged** nuevo.  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>Copias de seguridad de registros con otras herramientas de copia de seguridad o scripts personalizados  
 Dos copias de seguridad cualesquiera que estén configuradas para realizar copias de seguridad de registros en la misma base de datos interrumpirán la cadena de registro de copia de seguridad. Aunque [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] intente remediar la interrupción en la cadena de copias de seguridad programando copias de seguridad completas cuando se detecta una interrupción en la cadena, ello significa actualizar continuamente las interrupciones y las copias de seguridad de registros periódicas realizadas por las dos herramientas competidoras. También puede afectar a la capacidad de recuperación de la base de datos, ya que no se puede esperar que ninguna herramienta tenga un conjunto completo de copias de seguridad en orden. Aunque esto se aplica a dos características o herramientas cualesquiera que realizan copias de seguridad de registros, resulta útil ver ejemplos específicos como se describe a continuación. También es la base de los problemas de configuración de planes de mantenimiento o del trasvase de registros, como se ha descrito en secciones anteriores de este tema.  
  
 **Data Protection Manager (DPM) en función de las copias de seguridad:** Microsoft Data Protection Manager permite realizar copias de seguridad completas e incrementales. Las copias de seguridad incrementales son copias de seguridad de registros que realizan un truncamiento del registro después de crear una copia de seguridad de registros T. Por tanto, no se admite la configuración de DPM y [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] para la misma base de datos.  
  
 **Herramientas de terceros o secuencias de comandos:** cualquier herramienta de terceros o scripts que realizan copias de seguridad de registros que producen el truncamiento del registro no es compatible con [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]y no se admite.  
  
 Si tiene [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] habilitada para una instancia de base de datos y desea realizar una copia de seguridad ad hoc que se puede usar el [smart_admin.sp_backup_on_demand &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql) procedimiento almacenado como se describe en la anterior sección. Si también tiene necesidad de programar o hacer copias de seguridad periódicamente fuera de [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)], puede utilizar la Copia de seguridad de solo copia.  Para obtener más información, vea [Copias de seguridad de solo copia &#40;SQL Server&#41;](../relational-databases/backup-restore/copy-only-backups-sql-server.md).  
  
  
