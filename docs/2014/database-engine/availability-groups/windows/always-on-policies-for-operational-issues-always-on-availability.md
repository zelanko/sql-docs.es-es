---
title: Siempre en directivas para problemas operativos con grupos de disponibilidad (SQL Server) Always On | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], troubleshooting
- Availability Groups [SQL Server], policies
ms.assetid: afa5289c-641a-4c03-8749-44862384ec5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 815f549cf9ab6dd7fe748c08ae7f32683c9d8551
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62815760"
---
# <a name="always-on-policies-for-operational-issues-with-always-on-availability-groups-sql-server"></a>Directivas de AlwaysOn para problemas operativos con grupos de disponibilidad AlwaysOn (SQL Server)
  El modelo de estados de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] evalúa un conjunto de directivas predefinidas de administración basada en directiva (PBM). Puede utilizarlas para ver el estado de un grupo de disponibilidad y sus réplicas de disponibilidad y bases de datos en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 
  
##  <a name="TermsAndDefinitions"></a> Términos y definiciones  
 Directivas predefinidas AlwaysOn  
 Un conjunto de directivas integradas que permiten que un administrador de bases de datos pueda comprobar un grupo de disponibilidad, así como sus réplicas y bases de datos de disponibilidad, para probar el cumplimiento de los estados definidos por las directivas de AlwaysOn.  
  
 [Grupos de disponibilidad AlwaysOn](always-on-availability-groups-sql-server.md) una solución de alta disponibilidad y recuperación ante desastres que proporciona una alternativa de nivel empresarial para la creación de reflejo de base de datos.  
  
 grupo de disponibilidad  
 Un contenedor para un conjunto discreto de bases de datos de usuario, conocido como *bases de datos de disponibilidad*, que realizan la conmutación por error conjuntamente.  
  
 réplica de disponibilidad  
 Una instancia de un grupo de disponibilidad hospedado en una instancia específica de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y que mantiene una copia local de cada base de datos de disponibilidad perteneciente al grupo de disponibilidad. Existen dos tipos de réplicas de disponibilidad: una sola *réplica principal* y de una a cuatro *réplicas secundarias*. Las instancias de servidor que hospedan las réplicas de disponibilidad para un grupo de disponibilidad dado deben residir en nodos diferentes de un único clúster de clústeres de conmutación por error (WSFC).  
  
 base de datos de disponibilidad  
 Base de datos que pertenece a un grupo de disponibilidad. Para cada disponibilidad de la base de datos, la disponibilidad del grupo mantiene una sola copia de lectura y escritura ( *base de datos principal*) y de una a cuatro copias de solo lectura (*bases de datos secundarias*).  
  
 Panel de AlwaysOn  
 Un panel [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] que proporciona una vista global del estado de un grupo de disponibilidad. Para obtener más información, vea [Panel AlwaysOn](#Dashboard), más adelante en este tema.  
  
##  <a name="AlwaysOnPBM"></a> Directivas predefinidas y problemas  
 En la siguiente tabla se resumen las directivas predefinidas.  
  
|Nombre de la directiva|Problema|Categoría**<sup>*</sup>**|Faceta|  
|-----------------|-----------|------------------------------|-----------|  
|Estado de clúster de WSFC|[El servicio de clúster de WSFC está sin conexión](wsfc-cluster-service-is-offline.md).|Crítico|Instancia de SQL Server|  
|Estado en línea del grupo de disponibilidad|[Grupo de disponibilidad sin conexión](availability-group-is-offline.md).|Crítico|grupo de disponibilidad|  
|Preparación para la conmutación automática por error del grupo de disponibilidad|[Grupo de disponibilidad no preparado para conmutación automática por error](availability-group-is-not-ready-for-automatic-failover.md).|Crítico|grupo de disponibilidad|  
|Estado de sincronización de datos de las réplicas de disponibilidad|[Algunas réplicas de disponibilidad no sincronizan datos](some-availability-replicas-are-not-synchronizing-data.md).|Advertencia|grupo de disponibilidad|  
|Estado de sincronización de los datos de réplicas sincrónicas|[Algunas réplicas sincrónicas no están sincronizadas](some-synchronous-replicas-are-not-synchronized.md).|Advertencia|grupo de disponibilidad|  
|Estado del rol de réplicas de disponibilidad|[Algunas réplicas de disponibilidad no tienen un rol en buen estado](some-availability-replicas-do-not-have-a-healthy-role.md).|Advertencia|grupo de disponibilidad|  
|Estado de conexión de las réplicas de disponibilidad|[Algunas réplicas de disponibilidad están desconectadas](some-availability-replicas-are-disconnected.md).|Advertencia|grupo de disponibilidad|  
|Estado del rol de réplica de disponibilidad|[La réplica de disponibilidad no tiene un rol en buen estado](availability-replica-does-not-have-a-healthy-role.md).|Crítico|réplica de disponibilidad|  
|Estado de conexión de la réplica de disponibilidad|[Réplica de disponibilidad desconectada](availability-replica-is-disconnected.md).|Crítico|réplica de disponibilidad|  
|Estado de unión de réplica de disponibilidad|[La réplica de disponibilidad no está unida](availability-replica-is-not-joined.md).|Advertencia|réplica de disponibilidad|  
|Estado de sincronización de datos de las réplicas de disponibilidad|[El estado de sincronización de datos de alguna base de datos de disponibilidad no está en buen estado](data-synchronization-state-of-some-availability-database-is-not-healthy.md).|Advertencia|réplica de disponibilidad|  
|Estado de suspensión de la base de datos de disponibilidad|[Base de datos de disponibilidad suspendida](availability-database-is-suspended.md).|Advertencia|Base de datos de disponibilidad|  
|Estado de combinación de la base de datos de disponibilidad|[Base de datos secundaria sin combinar](secondary-database-is-not-joined.md).|Advertencia|Base de datos de disponibilidad|  
|Estado de sincronización de datos de la base de datos de disponibilidad|[El estado de sincronización de datos de bases de datos de disponibilidad no está en buen estado](data-synchronization-state-of-availability-database-is-not-healthy.md).|Advertencia|Base de datos de disponibilidad|  
  
> [!IMPORTANT]  
>  **<sup>*</sup>**  Las directivas de AlwaysOn, los nombres de categoría se usan como identificadores. La acción de cambiar el nombre de una categoría de AlwaysOn interrumpiría la funcionalidad de la evaluación de estado. Por consiguiente, no modifique los nombres de las categorías de AlwaysOn.  
  
##  <a name="Dashboard"></a> Panel AlwaysOn  
 El panel AlwaysOn proporciona una vista global del estado de un grupo de disponibilidad. El panel AlwaysOn incluye las siguientes características:  
  
-   Permite mostrar fácilmente los detalles sobre un grupo de disponibilidad determinado, sus réplicas de disponibilidad y sus bases de datos.  
  
-   Muestra indicaciones visuales de los estados clave para ayudar a los administradores de bases de datos a tomar decisiones operativas rápidas.  
  
-   Proporciona puntos de inicio para escenarios de solución de problemas.  
  
-   Cuando surge un problema operativo determinado, rellena el cuadro de diálogo **Resultado de evaluación de directiva** con información sobre infracciones específicas de la directiva de mantenimiento de AlwaysOn y con vínculos a la ayuda de la corrección.  
  
-   Proporciona un visor de eventos extendidos de mantenimiento que muestra los eventos anteriores para los problemas específicos de AlwaysOn.  
  
-   Si la conmutación por error del grupo de disponibilidad es una solución posible para un problema, proporciona un punto de inicio para los vínculos del[Asistente para grupo de disponibilidad de conmutación por error](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md). Este asistente usa un administrador de bases de datos a través del proceso de conmutación por error manual.  
  
##  <a name="ExtendHealthModel"></a> Extender el modelo de estado de AlwaysOn  
 Extender el modelo de estados de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] es simplemente cuestión de crear sus propias directivas definidas por el usuario y ponerlas en determinadas categorías según el tipo de objeto que se está supervisando.  Después de modificar algunos valores, el panel AlwaysOn evaluará automáticamente sus propias directivas definidas por el usuario, junto con las directivas predefinidas AlwaysOn.  
  
 Una directiva definidas por el usuario puede utilizar cualquiera de las facetas PBM disponibles, incluidas las utilizadas por las directivas predefinidas AlwaysOn (vea [Directiva predefinidas y problemas](#AlwaysOnPBM), anteriormente en este tema). La faceta de servidor proporciona las siguientes propiedades para supervisar el estado de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]: (`IsHadrEnabled` y `HadrManagerStatus`). La faceta de servidor también proporciona a las propiedades las siguientes directivas para supervisar la configuración de clúster de WSFC: `ClusterQuorumType` y `ClusterQuorumState`.  
  
 Para obtener más información, vea [Modelo de estado AlwaysOn Parte 2: el modelo de estado](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx) (un blog del equipo de SQL Server AlwaysOn).  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Usar directivas de AlwaysOn para ver el estado de un grupo de disponibilidad &#40;SQL Server&#41;](use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
-   [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
-   [Recuperación ante desastres del clúster WSFC mediante cuórum forzado &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
-   [Forzar el inicio de un clúster WSFC sin un quórum](../../../sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum.md)  
  
-   [Realizar una conmutación por error manual forzada de un grupo de disponibilidad &#40;SQL Server&#41;](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)  
  
-   [Solución de problemas de una operación de agregar archivos con error &#40;grupos de disponibilidad AlwaysOn&#41;](troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [El modelo de estado de AlwaysOn, parte 1: arquitectura del modelo de estado](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [El modelo de estado AlwaysOn parte 2: Extender el modelo de estado](https://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)  
  
-   [Guía de soluciones de Microsoft SQL Server AlwaysOn para alta disponibilidad y recuperación ante desastres](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>Vea también  
 [Grupos de disponibilidad AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md)   
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Administración de un grupo de disponibilidad &#40;SQL Server&#41;](administration-of-an-availability-group-sql-server.md)   
 [Supervisión de los grupos de disponibilidad &#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)  
  
  
