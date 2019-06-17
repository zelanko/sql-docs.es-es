---
title: Instalar un Service Pack en un sistema con el tiempo de inactividad mínimo para bases de datos reflejadas | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- hotfixes [SQL Server]
- database mirroring [SQL Server], upgrading system
- rolling upgrades [SQL Server]
- service packs [SQL Server]
- upgrading mirrored database systems
- upgrading SQL Server, mirrored databases
ms.assetid: bdc63142-027d-4ead-9d3e-147331387ef5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 821fd05e94ac820dff50bd08c70c75e7e9cc653d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779599"
---
# <a name="install-a-service-pack-on-a-system-with-minimal-downtime-for-mirrored-databases"></a>Instalar un Service Pack en un sistema con un tiempo de inactividad mínimo para bases de datos reflejadas
  En este tema se describe cómo minimizar el tiempo de inactividad de las bases de datos reflejadas cuando instale los Service Pack o las revisiones. Este proceso conlleva la actualización secuencial de las instancias de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] que forman parte de la creación de reflejo de la base de datos. Este formulario de actualización, que se conoce como un *actualización gradual*, reduce el tiempo de inactividad a solo una conmutación por error único. Tenga en cuenta que para las sesiones de modo de alto rendimiento en el que el servidor reflejado está geográficamente distante del servidor principal, una actualización gradual podría ser inadecuada.  
  
 Una actualización gradual es un proceso de varias fase que consta de las siguientes fases:  
  
-   Protección de los datos.  
  
-   Si la sesión incluye un testigo, recomendamos que lo quite. Si no lo hace, al actualizar la instancia del servidor reflejado, la disponibilidad de la base de datos depende del testigo que sigue estando conectado a la instancia del servidor principal. Después de quitar un testigo, puede actualizarlo en cualquier momento durante el proceso de actualización gradual sin aumentar el tiempo de inactividad de la base de datos.  
  
    > [!NOTE]  
    >  Para más información, vea [Cuórum: cómo un testigo afecta a la disponibilidad de la base de datos &#40;creación de reflejo de la base de datos&#41;](database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
-   Si una sesión se está ejecutando en modo de alto rendimiento, cambie el modo de funcionamiento al modo de alta seguridad.  
  
-   Actualice cada instancia del servidor implicada en la creación de reflejo de la base de datos. Una actualización gradual implica actualizar la instancia del servidor que es actualmente el servidor reflejado, conmutación manual por cada uno de sus bases de datos reflejadas y actualizar la instancia del servidor que primero era el servidor principal (y ahora es el nuevo servidor reflejado). En este momento, tendrá que reanudar la creación de reflejo.  
  
    > [!NOTE]  
    >  Antes de iniciar una actualización gradual, recomendamos que realice un ejercicio de conmutación manual por error en al menos una de las sesiones de creación de reflejo.  
  
-   Revierta al modo de alto rendimiento, si es necesario.  
  
-   Devuelva al testigo a la sesión de creación de reflejo, si es necesario.  
  
 A continuación se describen los procedimientos para estas fases.  
  
> [!IMPORTANT]  
>  Una instancia del servidor podría estar realizando roles de creación de reflejo distintos (servidor principal, servidor reflejado o testigo) en sesiones de creación de reflejo simultáneas. En ese caso, tendrá que adaptar el proceso básico de actualización gradual como corresponda.  
  
### <a name="to-protect-your-data-before-an-update-a-best-practice"></a>Para proteger los datos antes de una actualización (práctica recomendada)  
  
1.  Realizar una copia de seguridad de base de datos completa en cada base de datos principal.  
  
     **Para realizar una copia de seguridad de una base de datos**  
  
    -   [Cree una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
2.  Ejecute el comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) en cada base de datos principal.  
  
### <a name="to-remove-a-witness-from-a-session"></a>Para quitar un testigo de una sesión  
  
1.  Si una sesión de creación de reflejo conlleva un testigo, recomendamos que lo quite antes de realizar una actualización gradual.  
  
     **Para quitar el testigo**  
  
    -   [Quitar el testigo de una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
### <a name="to-change-a-session-from-high-performance-mode-to-high-safety-mode"></a>Para cambiar una sesión del modo de alto rendimiento al modo de alta seguridad  
  
1.  Si una sesión de creación de reflejo se está ejecutando en modo de alto rendimiento, antes de realizar una actualización gradual, cambie al modo operativo de seguridad alta sin conmutación automática por error. Utilice uno de los métodos siguientes:  
  
    -   En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]: Cambiar el **modo de funcionamiento** opción a **seguridad alta sin conmutación automática por error (sincrónico)** mediante el uso de la [página creación de reflejo](../relational-databases/databases/database-properties-mirroring-page.md) de la **base de datos Propiedades** cuadro de diálogo. Para obtener información sobre cómo obtener acceso a esta página, vea [Iniciar el Asistente para la configuración de seguridad de la creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](database-mirroring/start-the-configuring-database-mirroring-security-wizard.md).  
  
    -   En [!INCLUDE[tsql](../includes/tsql-md.md)]: Seguridad de las transacciones se establece en FULL. Para obtener más información, vea [Cambiar la seguridad de las transacciones en una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md).  
  
### <a name="to-perform-the-rolling-update"></a>Para realizar la actualización gradual  
  
1.  Para minimizar el tiempo de inactividad, se recomienda lo siguiente: Iniciar la actualización gradual actualizando cualquier asociado de creación de reflejo que es actualmente el servidor reflejado en todas sus sesiones de creación de reflejo. Podría tener que actualizar varias instancias del servidor en este momento.  
  
    > [!NOTE]  
    >  Un testigo se puede actualizar en cualquier momento del proceso de actualización gradual. Por ejemplo, si una instancia del servidor es un servidor reflejado en la sesión 1 y es un testigo en la sesión 2, puede actualizar ahora la instancia del servidor.  
  
     La instancia del servidor que actualice primero depende de las sesiones de creación de reflejo, la configuración actual como sigue:  
  
    -   Si cualquier instancia del servidor ya es el servidor reflejado en todas sus sesiones de creación de reflejo, instale el Service Pack o la revisión en dicha instancia del servidor.  
  
    -   Si todas las instancias de servidor se encuentra el servidor principal en las sesiones de creación de reflejo, seleccione una instancia del servidor que actualice primero. Manualmente, a continuación, conmutar por error cada uno de sus bases de datos principales y actualizar esa instancia del servidor instalando el service pack o la revisión.  
  
     Después de actualizarse, una instancia del servidor automáticamente vuelve a unir cada uno de sus sesiones de creación de reflejo.  
  
     **Para realizar una conmutación manual por error**  
  
    -   [Realizar manualmente la conmutación por error de una sesión de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [Realizar una conmutación por error manualmente de una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md).  
  
     Para obtener más información sobre el funcionamiento de la conmutación por error manual, vea [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md).  
  
2.  Para cada sesión de creación de reflejo cuya instancia del servidor reflejado se acaba de actualizar, espere a la sesión de sincronización. A continuación, conéctese a la instancia del servidor principal y realice una conmutación manual por error de la sesión. En la conmutación por error, la instancia del servidor actualizada se convierte en el servidor principal para esa sesión y el servidor principal anterior se convierte en el servidor reflejado.  
  
     El objetivo de este paso es que otra instancia del servidor se convierta en el servidor reflejado en cada sesión de creación de reflejo en la que es un asociado.  
  
3.  Después de la conmutación por error, recomendamos que ejecute el comando [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) en la base de datos principal.  
  
4.  Instale el Service Pack o la revisión en cada una de las instancias del servidor que actualmente sean servidor reflejado, para todas aquellas sesiones de reflejado en las que sea un asociado. Podría tener que actualizar varios servidores en este momento.  
  
    > [!IMPORTANT]  
    >  En una configuración de creación de reflejo compleja, alguna instancia de servidor podría seguir siendo el servidor principal original en una o varias sesiones de creación de reflejo. Repita los pasos 2 a 4 para esas instancias de servidor hasta que se actualicen todas las instancias implicadas.  
  
5.  Reanude la sesión de creación de reflejo.  
  
    > [!NOTE]  
    >  Conmutación automática por error no funcionará hasta que se ha actualizado el testigo.  
  
6.  Instale el Service Pack o la revisión en el resto de instancias del servidor que sean testigo para todas las sesiones de reflejo. Después de un testigo actualizado se vuelve a unir a una sesión de creación de reflejo, conmutación automática por error vuelve a posibles. Podría tener que actualizar varios servidores en este momento.  
  
### <a name="to-return-a-session-to-high-performance-mode"></a>Para devolver una sesión al modo de alto rendimiento  
  
1.  Si lo desea, vuelva al modo de alto rendimiento utilizando uno de los métodos siguientes:  
  
    -   En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]: Cambio la **modo de funcionamiento** opción a **rendimiento alto (asincrónico)** mediante el uso de la [página creación de reflejo](../relational-databases/databases/database-properties-mirroring-page.md) de la **propiedades de la base de datos**cuadro de diálogo.  
  
    -   En [!INCLUDE[tsql](../includes/tsql-md.md)]: Use [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) para establecer la seguridad de las transacciones en OFF.  
  
### <a name="to-return-a-witness-to-a-mirroring-session"></a>Para devolver un testigo a una sesión de creación de reflejo  
  
1.  Si lo desea, en modo de alta seguridad, restablezca el testigo en cada sesión de creación de reflejo.  
  
     **Para restablecer el testigo**  
  
    -   [Agregar o reemplazar un testigo de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
    -   [Agregar un testigo de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;Transact-SQL&#41;](database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Reflejo de la base de datos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [Modos de funcionamiento de la creación de reflejo de la base de datos](database-mirroring/database-mirroring-operating-modes.md)   
 [Conmutación de roles durante una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [Ver el estado de una base de datos reflejada &#40;SQL Server Management Studio&#41;](database-mirroring/view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
  
