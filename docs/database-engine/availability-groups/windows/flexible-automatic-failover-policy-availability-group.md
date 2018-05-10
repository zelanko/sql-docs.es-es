---
title: Directiva de conmutación por error automática flexible - Grupo de disponibilidad | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- flexible failover policy
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 8c504c7f-5c1d-4124-b697-f735ef0084f0
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8624c517ddbaa4b1b48feab2f13fc577a30d0ea0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="flexible-automatic-failover-policy---availability-group"></a>Directiva de conmutación por error automática flexible - Grupo de disponibilidad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Una directiva de conmutación por error flexible proporciona mayor control sobre las condiciones que produce una [conmutación automática por error](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md) para un grupo de disponibilidad. Al cambiar las condiciones de error que activan una conmutación automática por error y la frecuencia de comprobaciones de estado, se puede aumentar o reducir la probabilidad de una conmutación automática por error que sea compatible con su SLA por tener alta disponibilidad.  
  
 La directiva flexible de conmutación por error de un grupo de disponibilidad se define por su nivel de condición de error y el umbral de tiempo de espera de comprobación de estado. Al detectar que un grupo de disponibilidad ha superado su nivel de condición de error o su umbral de tiempo de espera de comprobación de estado, la DLL de recursos del grupo de disponibilidad responde a los clústeres de conmutación por error de Windows Server (WSFC). El clúster WSFC entonces inicia una conmutación automática por error a la réplica secundaria.  
  
> [!IMPORTANT]  
>  Si un grupo de disponibilidad supera su umbral de error de WSFC, el clúster de WSFC no intentará una conmutación automática por error para dicho grupo. Además, el grupo de recursos de WSFC del grupo de disponibilidad permanece en un estado de error hasta que el administrador del clúster conecta manualmente el grupo de recursos con error o el administrador de la base de datos realiza una conmutación por error manual del grupo de disponibilidad. El *umbral de error de WSFC* se define como el número máximo de errores admitidos para el grupo de disponibilidad en un período de tiempo determinado. El período predeterminado es de seis horas, y el valor predeterminado del número máximo de errores durante este período es *n*-1, donde *n* es el número de nodos de WSFC. Para cambiar los valores del umbral de error de un grupo de disponibilidad determinado, use la consola del administrador de conmutación por error de WSFC.  
  
 Este tema contiene las siguientes secciones:  
  
-   [Umbral de tiempo de espera de comprobación de estado](#HCtimeout)  
  
-   [Nivel de condición de error](#FClevel)  
  
-   [Tareas relacionadas](#RelatedTasks)  
  
-   [Contenido relacionado](#RelatedContent)  
  
##  <a name="HCtimeout"></a> Umbral de tiempo de espera de comprobación de estado  
 La DLL de recursos del clúster WSFC del grupo de disponibilidad realiza una *comprobación de estado* de la réplica principal, llamando al procedimiento almacenado [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) en la instancia de SQL Server que hospeda la réplica principal. **sp_server_diagnostics** devuelve resultados en un intervalo que iguala 1/3 del umbral de tiempo de espera de comprobación de estado del grupo de disponibilidad. El umbral de tiempo de espera de comprobación de estado predeterminado es 30 segundos, lo que hace que **sp_server_diagnostics** devuelva en un intervalo de 10 segundos. Si **sp_server_diagnostics** es lento o no devuelve información, la DLL de recursos esperará al intervalo completo del umbral de tiempo de espera de comprobación de estado antes de determinar que la réplica primaria no responde. Si la réplica primaria no responde, se inicia una conmutación automática por error, si se admite actualmente.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** no realiza comprobaciones de estado en el nivel de base de datos.  
  
##  <a name="FClevel"></a> Nivel de condición de error  
 Si **sp_server_diagnostics** devuelve los datos de diagnóstico y la información de estado, se garantiza que una conmutación automática por error dependa del nivel de condición de error del grupo de disponibilidad. El *nivel de condición de error* especifica qué condiciones de error desencadenan una conmutación automática por error. Hay cinco niveles de condición de error que abarcan desde el nivel menos restrictivo (nivel uno) al más restrictivo (nivel cinco). Un nivel dado abarca los niveles menos restrictivos. Así pues, el nivel de condición más estricto, cinco, incluye las condiciones menos restrictivas, y así sucesivamente.  
  
> [!IMPORTANT]  
>  Ningún nivel de condición de error detecta las bases de datos dañadas ni las bases de datos sospechosas. Por tanto, una base de datos que está dañada o es sospechosa (debido a un error de hardware, a daños en los datos o a otro problema) nunca desencadena una conmutación automática por error.  
  
 En la tabla siguiente se describen las condiciones de error correspondientes a cada nivel.  
  
|Nivel|Condición de error|[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valor|Valor de PowerShell|  
|-----------|-----------------------|------------------------------|----------------------|  
|Uno|Por inactividad de servidor. Especifica que se inicia una conmutación automática por error en alguno de los casos siguientes:<br /><br /> El servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está inactivo.<br /><br /> La concesión del grupo de disponibilidad para conectarse al clúster de WSFC expira porque no se ha recibido ninguna confirmación de la instancia del servidor. Para obtener más información, vea [Cómo funciona: tiempo de espera de concesión de AlwaysOn de SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx).<br /><br /> <br /><br /> Este es el nivel menos restrictivo.|1|**OnServerDown**|  
|Dos|Al dejar de responder el servidor. Especifica que se inicia una conmutación automática por error en alguno de los casos siguientes:<br /><br /> La instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se conecta al clúster y se ha superado el umbral de tiempo de espera de comprobación de estado del grupo de disponibilidad definido por el usuario.<br /><br /> La réplica de disponibilidad tiene un estado de error.|2|**OnServerUnresponsive**|  
|Tres|En errores de servidor críticos. Especifica que se inicia una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] graves, como bloqueos por subproceso huérfanos, infracciones serias de acceso de escritura o volcado excesivo.<br /><br /> Es el nivel predeterminado.|3|**OnCriticalServerError**|  
|Cuatro|En errores de servidor moderados. Especifica que se inicia una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] moderados, tales como una condición persistente de falta de memoria en el grupo de recursos de servidor interno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|4|**OnModerateServerError**|  
|Cinco|En cualquier condición de error apta. Especifica que se inicia una conmutación automática por error en el caso de condiciones de error aptas, incluidas las siguientes:<br /><br /> Detección de un interbloqueo del programador.<br /><br /> Detección de un interbloqueo irresoluble.<br /><br /> <br /><br /> Es el nivel más restrictivo.|5|**OnAnyQualifiedFailureConditions**|  
  
> [!NOTE]  
>  La falta de respuesta de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a solicitudes del cliente no es pertinente a los grupos de disponibilidad.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar la conmutación automática por error**  
  
-   [Cambiar el modo de disponibilidad de una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md) (la conmutación automática por error necesita el modo de disponibilidad de confirmación sincrónica)  
  
-   [Cambiar el modo de conmutación por error de una réplica de disponibilidad &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Configurar la directiva de conmutación por error flexible para controlar las condiciones de la conmutación automática por error &#40;grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Cómo funciona: tiempo de espera de concesión de AlwaysOn de SQL Server](http://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-Always%20On-lease-timeout.aspx)  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidad &#40;grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Conmutación por error y modos de conmutación por error &#40;Grupos de disponibilidad AlwaysOn&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Directiva de conmutación por error para instancias de clústeres de conmutación por error](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)  
  
  
