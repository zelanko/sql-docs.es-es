---
title: "Actualización de instancias de la réplica del grupo de disponibilidad AlwaysOn | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
caps.latest.revision: "14"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b4be12e82f4df3c15fbf465863174b0cdde051af
ms.sourcegitcommit: e904c2a85347a93dcb15bb6b801afd39613d3ae7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/16/2017
---
# <a name="upgrading-always-on-availability-group-replica-instances"></a>Actualización de instancias de la réplica del grupo de disponibilidad AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Al actualizar un grupo de disponibilidad AlwaysOn de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a una nueva versión de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] , a un Service Pack o una actualización acumulativa de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o bien al instalarse en una nueva versión acumulativa o un nuevo Service Pack de Windows, puede reducir el tiempo de inactividad de la réplica principal a solo una conmutación por error manual realizando una actualización gradual (o dos conmutaciones por error manuales si conmuta por recuperación a la base de datos primaria original). Durante el proceso de actualización, una réplica secundaria no estará disponible para la conmutación por error u operaciones de solo lectura y, después de la actualización, puede pasar algún tiempo antes de que la réplica secundaria se ponga al día con el nodo de la réplica principal según el volumen de actividad del nodo de la réplica principal (así que debe esperar un tráfico de red elevado).  
  
> [!NOTE]  
>  En este tema nos limitamos a explicar el proceso de actualización de SQL Server. No trataremos la actualización del sistema operativo que contiene el clúster de conmutación por error de Windows Server (WSFC). No se puede actualizar el sistema operativo Windows que hospeda el clúster de conmutación por error en sistemas operativos anteriores a Windows Server 2012 R2. Para actualizar un nodo de clúster que se ejecute en Windows Server 2012 R2, vea [Cluster Operating System Rolling Upgrade](https://technet.microsoft.com/library/dn850430.aspx)(Actualización gradual del sistema operativo de clústeres).  
  
## <a name="prerequisites"></a>Prerequisites  
 Antes de empezar, revise la siguiente información importante:  
  
-   [Supported Version and Edition Upgrades](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): Compruebe que puede actualizar a SQL Server 2016 desde su versión del sistema operativo Windows y la versión de SQL Server. Por ejemplo, no puede actualizar directamente desde una instancia de SQL Server 2005 a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
-   [Choose a Database Engine Upgrade Method](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): seleccione el método y los pasos de actualización adecuados en función de la revisión de versiones admitidas y actualizaciones de ediciones, y también teniendo en cuenta otros componentes instalados en el entorno con el fin de actualizar los componentes en el orden correcto.  
  
-   [Planeamiento y prueba del plan de actualización del motor de base de datos](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): revise las notas de la versión y los problemas conocidos de actualización, la lista de comprobación previa a la actualización y desarrolle y pruebe el plan de actualización.  
  
-   [Requisitos de hardware y software para instalar SQL Server 2016:](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)revise los requisitos de software para instalar [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Si se requiere software adicional, puede instalarlo en cada nodo antes de comenzar el proceso de actualización para reducir los posibles tiempos de inactividad.  

> [!NOTE]  
>  No se permite mezclar versiones de SQL Server en el mismo AG. Para migrar a una versión nueva con grupos de disponibilidad, el único método admitido es un grupo de disponibilidad distribuido que esté en SQL Server 2016 Enterprise Edition o en una versión posterior.

## <a name="rolling-upgrade-best-practices-for-always-on-availability-groups"></a>Prácticas recomendadas de las actualizaciones graduales en grupos de disponibilidad AlwaysOn  
 Las siguientes prácticas recomendadas deberían tenerse en cuenta al realizar actualizaciones de servidor con el fin de reducir el tiempo de inactividad y la pérdida de datos en los grupos de disponibilidad:  
  
-   Antes de comenzar la actualización gradual, siga estos pasos:  
  
    -   Realice una conmutación por error manual de prueba en al menos una de las instancias de las réplicas de confirmación sincrónica.  
  
    -   Proteja los datos realizando una copia de seguridad de la base de datos completa en cada base de datos de disponibilidad  
  
    -   Ejecute DBCC CHECKDB en cada base de datos de disponibilidad  
  
-   Actualice siempre primero las instancias de las réplicas secundarias remotas, después las de las locales y, a continuación, la de la réplica principal en último lugar.  
  
-   No se pueden realizar copias de seguridad en una base de datos que está en proceso de actualización.  Antes de actualizar las réplicas secundarias, configure la preferencia de copia de seguridad automatizada para ejecutar copias de seguridad solo en la réplica primaria.  Durante una actualización de versión, no habrá réplicas legibles o disponibles para copias de seguridad. Durante una actualización que no sea de versión, puede configurar copias de seguridad automatizadas para ejecutarse en réplicas secundarias antes de actualizar la principal.  
  
-   Durante una actualización de versión, no se pueden leer las réplicas secundarias legibles después de que se actualice una secundaria legible y antes de que la réplica principal conmute por error a una secundaria actualizada, o bien de que se actualice la principal.  
  
-   Para impedir las conmutaciones por error no intencionadas del grupo de disponibilidad durante el proceso de actualización, quite la conmutación por error de disponibilidad de las réplicas de confirmación sincrónica antes de comenzar.  
  
-   No actualice la instancia de la réplica principal antes de conmutar por error el grupo de disponibilidad a una instancia actualizada con una réplica secundaria en primer lugar. De lo contrario, las aplicaciones cliente pueden sufrir un tiempo de inactividad ampliado durante la actualización en la instancia de la réplica principal.  
  
-   Conmute por error el grupo de disponibilidad siempre a una instancia de una réplica secundaria de confirmación sincrónica. Si conmuta por error a una instancia de una réplica secundaria de confirmación asincrónica, las bases de datos sufrirán la pérdida de datos y el movimiento de datos se suspende automáticamente hasta que reanude de forma manual el movimiento de datos.  
  
-   No actualice la instancia de la réplica principal antes de actualizar cualquier otra instancia de una réplica secundaria. Una réplica principal actualizada ya no puede entregar registrar a ninguna réplica secundaria cuya instancia de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] aún no haya sido actualizada a la misma versión. Cuando el movimiento de datos a una réplica secundaria se suspenda, no puede producirse la conmutación por error automática para dicha réplica y las bases de datos de disponibilidad son vulnerables ante la pérdida de datos.  
  
-   Ante de conmutar por error un grupo de disponibilidad, compruebe que el estado de sincronización del destino de la conmutaicón es SINCRONIZADO.  
  
## <a name="rolling-upgrade-process"></a>Proceso de actualización gradual  
 En la práctica, el proceso exacto dependerá de factores como la topología de implementación de los grupos de disponibilidad y del modo de confirmación de cada réplica. Pero, en un escenario más sencillo, una actualización gradual es un proceso de varias fases que en su forma más sencilla implica los pasos siguientes:  
  
 ![Actualización de un grupo de disponibilidad en un escenario de HADR](../../../database-engine/availability-groups/windows/media/alwaysonupgrade-ag-hadr.gif "Actualización de un grupo de disponibilidad en un escenario de HADR")  
  
1.  Quitar la conmutación por error automática en todas las réplicas de confirmación sincrónica  
  
2.  Actualizar todas las instancias de réplica secundaria que ejecutan réplicas secundarias de confirmación asincrónica  
  
3.  Actualizar todas las instancias de réplica local que no se ejecutan actualmente en la principal  
  
4.  Conmutar por error el grupo de disponibilidad de forma manual a una réplica secundaria de confirmación sincrónica local  
  
5.  Actualizar la instancia de réplica local que antes hospedaba la principal  
  
6.  Configurar los asociados de conmutación por error automática según convenga  
  
 Si es necesario, puede realizar una conmutación por error manual adicional para devolver al grupo de disponibilidad a su configuración original.  
  
## <a name="availability-group-with-one-remote-secondary-replica"></a>Grupo de disponibilidad con una réplica secundaria remota  
 Si ha implementado un grupo de disponibilidad para la recuperación de desastres, puede que tenga que conmutar por error el grupo de disponibilidad a una réplica secundaria de confirmación asincrónica. Tal configuración se muestra en la ilustración siguiente:  
  
 ![Actualización de un grupo de disponibilidad en un escenario de DR](../../../database-engine/availability-groups/windows/media/agupgrade-ag-dr.gif "Actualización de un grupo de disponibilidad en un escenario de DR")  
  
 En esta situación, debe conmutar por error el grupo de disponibilidad a la réplica secundaria de confirmación asincrónica durante la actualización gradual. Para impedir la pérdida de datos, cambie el modo de confirmación a confirmación sincrónica y espere a que la réplica secundaria se sincronice antes de conmutar por error al grupo de disponibilidad. Por lo tanto, el proceso de actualización puede ser similar al siguiente:  
  
1.  Actualizar la instancia de réplica secundaria en el sitio remoto  
  
2.  Cambiar el modo de confirmación a confirmación sincrónica  
  
3.  Esperar hata que el estado de sincronización sea SINCRONIZADO  
  
4.  Conmutar por error el grupo de disponibilidad a la réplica secundaria del sitio remoto  
  
5.  Cambiar o actualizar la instancia de réplica local (sitio principal)  
  
6.  Conmutar por error el grupo de disponibilidad al sitio principal  
  
7.  Cambiar el modo de confirmación a confirmación asincrónica  
  
 Dado que el modo de confirmación sincrónica no es una opción recomendada para la sincronización de datos en un sitio remoto, las aplicaciones de cliente pueden apreciar un aumento inmediato en la latencia de las bases de datos tras el cambio de configuración. Además, realizar una conmutación por error provocará que todos los mensajes de registro no reconocidos se descarten. La cantidad de mensajes de registro descartados puede ser bastante grande debido a la alta latencia de red entre dos sitios, lo que ocasiona que los clientes experimenten un gran volumen de errores de transacciones. Puede aminorar el impacto en las aplicaciones cliente si hace lo siguiente:  
  
-   Seleccionar cuidadosamente una ventana de mantenimiento durante el tráfico lento de cliente  
  
-   Mientras actualiza [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] en el sitio principal, cambiar el modo de disponibilidad de nuevo a la confirmación asincrónica y luego revertir al modo sincrónico cuando esté listo para conmutar por error al sitio principal de nuevo.  
  
## <a name="availability-group-with-failover-cluster-instance-nodes"></a>Grupo de disponibilidad con nodos de instancia del clúster de conmutación por error  
 Si un grupo de disponibilidad contiene nodos de instancia de clúster de conmutación por error (FCI), debe actualizar los nodos inactivos antes de actualizar los nodos activos. La ilustración siguiente muestra un escenario de grupos de disponibilidad común con FCI para la confirmación asincrónica y una alta disponibilidad local entre los FCI pra la recuperación de desastres remota y la secuencia de actualización.  
  
 ![Actualización de un grupo de disponibilidad con FCI](../../../database-engine/availability-groups/windows/media/agupgrade-ag-fci-dr.gif "Actualización de un grupo de disponibilidad con FCI")  
  
1.  Actualizar REMOTE2  
  
2.  Conmutar por error FCI2 a REMOTE2  
  
3.  Actualizar REMOTE1  
  
4.  Actualizar PRIMARY2  
  
5.  Conmutar por error FCI1 a PRIMARY2  
  
6.  Actualizar PRIMARY1  
  
## <a name="upgrade-update-sql-server-instances-with-multiple-availability-groups"></a>Actualizar las instancias de SQL Server con varios grupos de disponibilidad  
 Si ejecuta varios grupos de disponibilidad con réplicas principales en nodos de servidor independientes (una configuración activa/activa), la ruta de actualización implica más pasos de conmutación por error para presentar una alta disponibilidad en el proceso. Suponga que ejecuta tres grupos de disponibilidad en tres nodos de servidor según se muestra en la tabla siguiente y que todas las réplicas secundarias se ejecutan en el modo de confirmación sincrónica.  
  
|Grupo de disponibilidad|Nodo1|Nodo2|Nodo3|  
|------------------------|-----------|-----------|-----------|  
|AG1|Principal|||  
|AG2||Principal||  
|AG3|||Principal|  
  
 Puede ser apropiado en su situación realizar una actualización gradual con equilibrio de carga en la secuencia siguiente:  
  
1.  Conmutar por error AG2 a Nodo3 (para liberar Nodo2)  
  
2.  Actualizar Node2  
  
3.  Conmutar por error AG1 a Nodo2 (para liberar Nodo1)  
  
4.  Actualizar Node1  
  
5.  Conmutar por error AG2 y AG3 a Nodo1 (para liberar Nodo3)  
  
6.  Actualizar Node3  
  
7.  No se puede realizar la conmutación por error de AG3 a Nodo3  
  
 Esta secuencia de actualización tiene un tiempo de inactividad promedio de menos de dos conmutaciones por error por cada grupo de disponibilidad. La configuración resultante se muestra en la tabla siguiente.  
  
|Grupo de disponibilidad|Nodo1|Nodo2|Nodo3|  
|------------------------|-----------|-----------|-----------|  
|AG1||Principal||  
|AG2|Principal|||  
|AG3|||Principal|  
  
 Según su implementación concreta, la ruta de actualización puede variar y el tiempo de inactividad que las aplicaciones cliente experimentan puede variar también.  
  
> [!NOTE]  
>  En muchos casos, una vez completada la actualización gradual, se conmutará por recuperación a la réplica principal original.  
  
## <a name="see-also"></a>Ver también  
 [Actualización a SQL Server 2016 mediante el Asistente para instalación &#40;programa de instalación&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Instalar SQL Server 2016 desde el símbolo del sistema](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  
  
  
