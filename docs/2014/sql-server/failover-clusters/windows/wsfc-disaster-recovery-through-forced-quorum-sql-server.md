---
title: Recuperación ante desastres del clúster WSFC mediante cuórum forzado (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], WSFC clusters
- quorum [SQL Server], AlwaysOn and WSFC quorum
- failover clustering [SQL Server], AlwaysOn Availability Groups
ms.assetid: 6cefdc18-899e-410c-9ae4-d6080f724046
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3c170fa1b302ccd0a1edec156b3b30429fc2daf8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63224628"
---
# <a name="wsfc-disaster-recovery-through-forced-quorum-sql-server"></a>Recuperación ante desastres del clúster WSFC mediante quórum forzado (SQL Server)
  El error de quórum se produce normalmente por un desastre sistémico, un error de comunicaciones persistente o una configuración incorrecta que afecta a varios nodos del clúster WSFC.  Es necesaria la intervención manual para la recuperación de un error de quórum.  
  
-   **Antes de empezar:**  [requisitos previos](#Prerequisites), [seguridad](#Security)  
  
-   **Recuperación ante desastres de WSFC mediante el procedimiento de quórum forzado** [WSFC recuperación ante desastres mediante el procedimiento de quórum forzado](#Main)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="BeforeYouBegin"></a>Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 El procedimiento de quórum forzado presupone que existía un quórum en estado correcto antes de que se produjera el error.  
  
> [!WARNING]  
>  El usuario debe conocer perfectamente los conceptos y las interacciones de los clústeres de conmutación por error de Windows Server, los modelos de quórum de WSFC, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]y la configuración de implementación específica del entorno.  
>   
>  Para obtener más información, vea:  [Clústeres de conmutación por error de Windows Server (WSFC) con SQL Server](https://msdn.microsoft.com/library/hh270278\(v=SQL.110\).aspx), [Configuración de los votos y modos de cuórum WSFC (SQL Server)](https://msdn.microsoft.com/library/hh270280\(v=SQL.110\).aspx)  
  
###  <a name="Security"></a> Seguridad  
 El usuario debe ser una cuenta de dominio que sea miembro del grupo Administradores en cada nodo del clúster de WSFC.  
  
##  <a name="Main"></a>Recuperación ante desastres de WSFC mediante el procedimiento de quórum forzado  
 Recuerde que el error de quórum provocará que todos los servicios de clúster, instancias de SQL Server y [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]del clúster WSFC se pongan sin conexión porque el clúster, tal y como está configurado, no puede asegurar la tolerancia a errores de nivel de nodo.  Un error de quórum significa que los nodos con derecho en buen estado del clúster WSFC ya no cumplen el modelo de quórum. Puede que se haya producido un error en algunos nodos y puede que algunos simplemente hayan cerrado el servicio del clúster WSFC y de lo contrario estar en buen estado, excepto por la pérdida de la capacidad de comunicarse con un quórum.  
  
 Para poner de nuevo en línea el clúster WSFC, debe corregir la causa principal del error de quórum en virtud de la configuración existente, recuperar las bases de datos afectadas según sea necesario y puede volver a configurar los nodos restantes del clúster WSFC para reflejar la topología de clúster superviviente.  
  
 Puede usar el procedimiento *quórum forzado* en un nodo del clúster WSFC para invalidar los controles de seguridad que pusieron el clúster fuera de conexión.  Esto indica al clúster de forma eficaz que suspenda las comprobaciones de votación de quórum y le permite poner de nuevo en línea los recursos del clúster WSFC y SQL Server en cualquiera de los nodos del clúster.  
  
 Este tipo de proceso de recuperación de desastres debe incluir los siguientes pasos:  
  
#### <a name="to-recover-from-quorum-failure"></a>Para la recuperación de un error de quórum:  
  
1.  **Determinar el ámbito del error.** Identifique los grupos de disponibilidad o las instancias de SQL Server que no responden, los nodos de clúster que están en línea y disponibles para uso después de los desastres, y examine los registros de eventos de Windows y los registros del sistema de SQL Server.  En la práctica, debe mantener los datos de incidentes y los registros del sistema para su análisis posterior.  
  
    > [!TIP]  
    >  En una instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]que responde, puede obtener información sobre el estado de los grupos de disponibilidad que poseen una réplica de disponibilidad en la instancia del servidor local consultando la vista de administración dinámica (DMV) [sys.dm_hadr_availability_group_states](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-group-states-transact-sql) .  
  
2.  **Inicie el clúster de WSFC mediante cuórum forzado en un único nodo.** Identifique un nodo con un número mínimo de errores de componentes, que sean distintos de cerrar el servicio del clúster WSFC.  Compruebe que este nodo puede comunicarse con una mayoría de los demás nodos.  
  
     En este nodo, fuerce manualmente el clúster para ponerlo en línea mediante el procedimiento de quórum forzado.  Para minimizar posibles pérdida de datos, seleccione un nodo que sea el último hospedaje de una réplica principal del grupo de disponibilidad.  
  
     Para obtener más información, vea:  [Forzar el inicio de un clúster WSFC sin un quórum](https://msdn.microsoft.com/library/hh270275\(v=SQL.110\).aspx)  
  
    > [!NOTE]  
    >  El valor del quórum forzado tiene un efecto de todo el clúster que bloquea las comprobaciones de quórum hasta que el clúster WSFC lógico logra una mayoría de votos y, de forma automática, cambia a un modo de funcionamiento normal de quórum.  
  
3.  **Inicie el servicio de WSFC normalmente en cada nodo en buen estado, de uno en uno.** No tiene que especificar la opción de quórum forzado cuando inicia el servicio de clúster de los demás nodos.  
  
     Mientras el servicio del clúster WSFC en cada nodo vuelve a estar en línea, negocia con los otros nodos en buen estado para sincronizar el nuevo estado de configuración del clúster.  Recuerde hacer esto en un nodo cada vez para evitar posibles condiciones de carrera para resolver el último estado conocido del clúster.  
  
    > [!WARNING]  
    >  Asegúrese de que cada nodo que inicia puede comunicarse con los demás nodos recientemente en línea.  Considere deshabilitar el servicio del clúster WSFC en los otros nodos.  De lo contrario, corre el riesgo de crear más de un conjunto de nodos de quórum; esto es un escenario de división de cerebro. Si los resultados del paso 1 son precisos, esto no debe suceder.  
  
4.  **Aplique el nuevo modo de cuórum y la configuración de votación de nodo.** Si al forzar el quórum se reiniciaron correctamente todos los nodos del clúster y la causa del error de quórum se ha corregido, no es necesario realizar cambios en el modo de quórum original y la configuración de voto de nodo.  
  
     De lo contrario, debe evaluar el nodo de clúster recién recuperado y la disponibilidad de la topología de réplica, así como cambiar el modo de quórum y las asignaciones de votos para cada nodo según corresponda. Los nodos no recuperados deben estar establecidos como sin conexión o tener sus votos de nodo establecidos en cero.  
  
    > [!TIP]  
    >  En este momento pueden aparecer los nodos y las instancias de SQL Server del clúster para restaurarlos de nuevo a una operación normal.  Sin embargo, puede que aún no exista un quórum en buen estado.  Compruebe mediante el Administrador de clústeres de conmutación por error o el panel de AlwaysOn de SQL Server Management Studio o los DMV adecuados, que un quórum se ha restaurado.  
  
5.  **Recupere las réplicas de base de datos del grupo de disponibilidad según sea necesario.** Las bases de datos del grupo sin disponibilidad deben recuperarse y volver a ponerse en línea por sí mismas como parte del proceso normal de inicio de SQL Server.  
  
     Puede minimizar la posible pérdida de datos y tiempo de recuperación de las réplicas del grupo de disponibilidad poniéndolas en línea de nuevo mediante esta secuencia: réplica principal, réplicas secundarias sincrónicas, réplicas secundarias asincrónicas.  
  
6.  **Reparar o reemplazar componentes con errores y volver a validar el clúster.** Ahora que se ha recuperado del desastre inicial y error de quórum, debe reparar o reemplazar los nodos erróneos y ajustar las configuraciones del clúster WSFC y AlwaysOn relacionadas en consecuencia.  Esta acción puede incluir quitar las réplicas del grupo de disponibilidad, desalojar los nodos de clúster o quitar y volver a instalar el software en un nodo.  
  
     Debe reparar o quitar todas las réplicas de disponibilidad con errores.  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no truncará el registro de transacciones más allá del punto conocido más lejano de la última réplica de disponibilidad.   Si una réplica con errores no se repara o se quita del grupo de disponibilidad, los registros de transacciones crecerán y se correrá el riesgo de quedarse sin espacio para los registros de transacciones en las otras réplicas.  
  
    > [!NOTE]  
    >  Si ejecuta la Validación de WSFC del Asistente para configuración cuando un agente de grupo de disponibilidad existe en el clúster de WSFC, el asistente genera el mensaje de advertencia incorrecto siguiente:  
    >   
    >  "La propiedad RegisterAllProviderIP para el nombre de red 'Name:<nombre_red>' está establecida en 1. Para la configuración de clúster actual, este valor debería estar establecido en 0".  
    >   
    >  Omita este mensaje.  
  
7.  **Repita el paso 4 según sea necesario.** El objetivo es volver a establecer el nivel adecuado de tolerancia a errores y la alta disponibilidad para las operaciones en buen estado.  
  
8.  **Realice el análisis de RPO/RTO.** Debe analizar los registros del sistema de SQL Server, las marcas de tiempo de la base de datos y los registros de eventos de Windows para determinar la causa principal del error, así como para documentar las experiencias reales del punto de recuperación y del tiempo de recuperación.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Forzar el inicio de un clúster WSFC sin un quórum](force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [Realizar una conmutación por error manual forzada de un grupo de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Ver la configuración de NodeWeight de quórum de clúster](view-cluster-quorum-nodeweight-settings.md)  
  
-   [Configurar los valores de NodeWeight de quórum de clúster](configure-cluster-quorum-nodeweight-settings.md)  
  
-   [Usar el panel de AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md) 
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Ver eventos y registros para un clúster de conmutación por error](https://technet.microsoft.com/library/cc772342\(WS.10\).aspx)  
  
-   [Cmdlet de clúster de conmutación por error Get-ClusterLog](https://technet.microsoft.com/library/ee461045.aspx)  
  
## <a name="see-also"></a>Consulte también  
 [Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](windows-server-failover-clustering-wsfc-with-sql-server.md)  
  
  
