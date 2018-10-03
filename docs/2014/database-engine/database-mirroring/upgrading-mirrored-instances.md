---
title: Minimizar el tiempo de inactividad para las bases de datos reflejadas al actualizar instancias de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading SQL Server, rolling upgrade of mirrored databases
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
ms.assetid: 0e73bd23-497d-42f1-9e81-8d5314bcd597
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a0ac6ea9d3437e22a1493c9888ccb75e7996f1c5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219865"
---
# <a name="minimize-downtime-for-mirrored-databases-when-upgrading-server-instances"></a>Minimizar el tiempo de inactividad de las bases de datos reflejadas al actualizar instancias de servidor
  Al actualizar instancias de servidor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], puede reducir el tiempo de inactividad de cada base de datos reflejada a solo una sola conmutación por error manual realizando una actualización secuencial, conocido como un *actualización gradual*. Una actualización gradual es un proceso de varias etapas que, en su forma más simple, implica la actualización de la instancia de servidor que está actuando actualmente como servidor reflejado en una sesión de creación de reflejo, la conmutación por error manual de la base de datos reflejada, la actualización del servidor principal anterior y la reanudación de la creación de reflejo. En la práctica, el proceso exacto dependerá del modo de funcionamiento y del número y diseño de la sesión de creación de reflejo que se ejecute en las instancias de servidor que va a actualizar.  
  
> [!NOTE]  
>  Para obtener información acerca de cómo realizar una actualización gradual para instalar un service pack o revisión, consulte [instalar un Service Pack en un sistema con el tiempo de inactividad mínimo para bases de datos reflejadas](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md).  
  
 **Preparación recomendada (prácticas recomendadas)**  
  
 Antes de iniciar una actualización gradual, es recomendable que:  
  
1.  Realice una conmutación por error manual de prueba en al menos una de las sesiones de creación de reflejo:  
  
    -   [Realizar manualmente la conmutación por error de una sesión de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [Realizar una conmutación por error manualmente de una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](manually-fail-over-a-database-mirroring-session-transact-sql.md).  
  
    > [!NOTE]  
    >  Para obtener más información sobre el funcionamiento de la conmutación por error manual, vea [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).  
  
2.  Proteja los datos:  
  
    1.  Realice una copia de seguridad completa de cada base de datos principal:  
  
         [Cree una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
    2.  Ejecute el comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) en cada base de datos principal.  
  
 **Fases de una actualización gradual**  
  
 Los pasos específicos de una actualización gradual dependen del modo de funcionamiento de la configuración de creación de reflejo. No obstante, las etapas básicas son las mismas.  
  
> [!NOTE]  
>  Para obtener información sobre los modos de funcionamiento, vea [Modos de funcionamiento de la creación de reflejo de la base de datos](database-mirroring-operating-modes.md).  
  
 La ilustración siguiente es un diagrama de flujo en el que se muestran las etapas básicas de una actualización gradual para cada modo de funcionamiento. Los procedimientos correspondientes se describen después de la ilustración.  
  
 ![Diagrama de flujo que muestra los pasos de una actualización gradual](../media/dbm-rolling-upgrade.gif "Diagrama de flujo que muestra los pasos de una actualización gradual")  
  
> [!IMPORTANT]  
>  Una instancia del servidor podría estar realizando roles de creación de reflejo distintos (servidor principal, servidor reflejado o testigo) en sesiones de creación de reflejo simultáneas. En ese caso, tendrá que adaptar el proceso básico de actualización gradual a la función. Para obtener más información, vea [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md).  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>Para cambiar una sesión del modo de alto rendimiento al modo de alta seguridad  
  
1.  Si una sesión de creación de reflejo se está ejecutando en modo de alto rendimiento, antes de realizar una actualización gradual, cambie al modo de seguridad alta sin conmutación automática por error.  
  
    > [!IMPORTANT]  
    >  Si el servidor reflejado está geográficamente distante del servidor principal, puede no ser conveniente realizar una actualización gradual.  
  
    -   En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: cambie la opción **Modo de funcionamiento** a **Seguridad alta sin conmutación automática por error (sincrónico)** mediante la página [Creación de reflejo](../../relational-databases/databases/database-properties-mirroring-page.md) del cuadro de diálogo **Propiedades de la base de datos**. Para obtener información sobre cómo obtener acceso a esta página, vea [Iniciar el Asistente para la configuración de seguridad de la creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md).  
  
    -   En [!INCLUDE[tsql](../../includes/tsql-md.md)]: establezca la seguridad de transacciones en FULL. Para obtener más información, vea [Cambiar la seguridad de las transacciones en una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](change-transaction-safety-in-a-database-mirroring-session-transact-sql.md).  
  
### <a name="to-remove-a-witness-from-a-session"></a>Para quitar un testigo de una sesión  
  
1.  Si una sesión de creación de reflejo conlleva un testigo, recomendamos que lo quite antes de realizar una actualización gradual. Si no lo hace, al actualizar la instancia del servidor reflejado, la disponibilidad de la base de datos depende del testigo que sigue estando conectado a la instancia del servidor principal. Después de quitar un testigo, puede actualizarlo en cualquier momento durante el proceso de actualización gradual sin aumentar el tiempo de inactividad de la base de datos.  
  
    > [!NOTE]  
    >  Para obtener más información, vea [Cuórum: cómo un testigo afecta a la disponibilidad de la base de datos &#40;reflejo de la base de datos&#41;](quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
    -   [Quitar el testigo de una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-perform-the-rolling-upgrade"></a>Para realizar la actualización gradual  
  
1.  Para minimizar el tiempo de inactividad, recomendamos que inicie la actualización gradual actualizando todos los asociados de creación de reflejo que sean actualmente el servidor reflejado en todas sus sesiones de creación de reflejo. Podría tener que actualizar varias instancias del servidor en este momento.  
  
    > [!NOTE]  
    >  Un testigo se puede actualizar en cualquier momento del proceso de actualización gradual. Por ejemplo, si una instancia del servidor es un servidor reflejado en la Sesión 1 y es un testigo en la Sesión 2, puede actualizar ahora la instancia del servidor.  
  
     La instancia del servidor que se debe actualizar en primer lugar depende de la configuración actual de las sesiones de creación de reflejo, como se indica a continuación:  
  
    -   Si cualquier instancia del servidor ya es el servidor reflejado en todas sus sesiones de creación de reflejo, actualice la instancia del servidor a la nueva versión.  
  
    -   Si todas las instancias del servidor son actualmente el servidor principal en cualquier sesión de creación de reflejo, seleccione una instancia del servidor para actualizarla primero. A continuación, conmute por error manualmente cada una de sus bases de datos principales y actualice esa instancia del servidor.  
  
     Una vez que se ha actualizado, una instancia del servidor vuelve a unirse automáticamente a cada una de sus sesiones de creación de reflejo.  
  
2.  En cada sesión de creación de reflejo cuya instancia del servidor reflejado se acaba de actualizar, espere a que la sesión se sincronice. A continuación, conéctese a la instancia del servidor principal y realice una conmutación manual por error de la sesión. Tras la conmutación por error, la instancia del servidor actualizada se convierte en el servidor principal para esa sesión y el servidor principal anterior se convierte en el servidor reflejado.  
  
     El objetivo de este paso es que otra instancia del servidor se convierta en el servidor reflejado en cada sesión de creación de reflejo en la que es un asociado.  
  
     **Restricciones después de la conmutación por error a una instancia del servidor actualizada.**  
  
     Después de la conmutación por error de una instancia de servidor anterior a una instancia de servidor de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , la sesión de la base de datos se suspende. No se puede reanudar hasta que se haya actualizado el otro asociado. Sin embargo, el servidor principal sigue aceptando conexiones, y permitiendo acceso y modificaciones a datos en la base de datos principal.  
  
    > [!NOTE]  
    >  El establecimiento de una nueva sesión de creación de reflejo requiere que todas las instancias del servidor se ejecuten en la misma versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Después de conmutar, le recomendamos que ejecute la [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) comando theprincipal base de datos.  
  
4.  Actualice todas las instancias del servidor que es ahora el servidor reflejado en todas las sesiones de creación de reflejo en las que sea asociado. Podría tener que actualizar varios servidores en este momento.  
  
    > [!IMPORTANT]  
    >  En una configuración de creación de reflejo compleja, alguna instancia de servidor podría seguir siendo el servidor principal original en una o varias sesiones de creación de reflejo. Repita los pasos 2 a 4 para esas instancias de servidor hasta que se actualicen todas las instancias implicadas.  
  
5.  Reanude la sesión de creación de reflejo.  
  
    > [!NOTE]  
    >  La conmutación automática por error no funcionará hasta que el testigo se haya actualizado y agregado de nuevo a la sesión de creación de reflejo.  
  
6.  Actualice cualquier instancia de servidor que quede y sea testigo en todas sus sesiones de creación de reflejo. Cuando un testigo actualizado se vuelva a unir a una sesión de creación de reflejo, la conmutación automática por error vuelve a ser posible. Podría tener que actualizar varios servidores en este momento.  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>Para devolver una sesión al modo de alto rendimiento  
  
1.  Si lo desea, vuelva al modo de alto rendimiento utilizando uno de los métodos siguientes:  
  
    -   En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: cambie la opción **Modo de funcionamiento** a **Rendimiento alto (asincrónico)** mediante la página [Creación de reflejo](../../relational-databases/databases/database-properties-mirroring-page.md) del cuadro de diálogo **Propiedades de la base de datos** .  
  
    -   En [!INCLUDE[tsql](../../includes/tsql-md.md)]: utilice [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)para desactivar la seguridad de las transacciones.  
  
### <a name="to-add-a-witness-back-into-a-mirroring-session"></a>Para volver a agregar un testigo a una sesión de creación de reflejo  
  
1.  Si lo desea, en modo de alta seguridad, restablezca el testigo en cada sesión de creación de reflejo.  
  
     **Para devolver un testigo**  
  
    -   [Agregar o reemplazar un testigo de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [Agregar un testigo de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;Transact-SQL&#41;](add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Reflejo de la base de datos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Ver el estado de una base de datos reflejada &#40;SQL Server Management Studio&#41;](view-the-state-of-a-mirrored-database-sql-server-management-studio.md)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Instalar un Service Pack en un sistema con el tiempo de inactividad mínimo para bases de datos reflejadas](../install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases.md)   
 [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Forzar el servicio en una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](force-service-in-a-database-mirroring-session-transact-sql.md)   
 [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Database Mirroring Operating Modes](database-mirroring-operating-modes.md)  
  
  
