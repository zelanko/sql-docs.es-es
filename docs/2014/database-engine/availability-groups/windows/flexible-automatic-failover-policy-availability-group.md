---
title: Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], flexible failover policy
- Availability Groups [SQL Server], failover
- flexible failover policy
- failover [SQL Server], AlwaysOn Availability Groups
ms.assetid: 8c504c7f-5c1d-4124-b697-f735ef0084f0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 63c9f56894ede1002b358c624ab763935fd42fc1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62789897"
---
# <a name="flexible-failover-policy-for-automatic-failover-of-an-availability-group-sql-server"></a>Directiva de conmutación por error flexible para conmutación automática por error de un grupo de disponibilidad (SQL Server)
  Una directiva de conmutación por error flexible proporciona mayor control sobre las condiciones que produce una [conmutación automática por error](failover-and-failover-modes-always-on-availability-groups.md) para un grupo de disponibilidad. Al cambiar las condiciones de error que activan una conmutación automática por error y la frecuencia de comprobaciones de estado, se puede aumentar o reducir la probabilidad de una conmutación automática por error que sea compatible con su SLA por tener alta disponibilidad.  
  
 La directiva flexible de conmutación por error de un grupo de disponibilidad se define por su nivel de condición de error y el umbral de tiempo de espera de comprobación de estado. Al detectar que un grupo de disponibilidad ha superado su nivel de condición de error o su umbral de tiempo de espera de comprobación de estado, la DLL de recursos del grupo de disponibilidad responde a los clústeres de conmutación por error de Windows Server (WSFC). El clúster WSFC entonces inicia una conmutación automática por error a la réplica secundaria.  
  
> [!IMPORTANT]  
>  Si un grupo de disponibilidad supera su umbral de error de WSFC, el clúster de WSFC no intentará una conmutación automática por error para dicho grupo. Además, el grupo de recursos de WSFC del grupo de disponibilidad permanece en un estado de error hasta que el administrador del clúster conecta manualmente el grupo de recursos con error o el administrador de la base de datos realiza una conmutación por error manual del grupo de disponibilidad. El *umbral de error de WSFC* se define como el número máximo de errores admitidos para el grupo de disponibilidad en un período de tiempo determinado. El período predeterminado es de seis horas, y el valor predeterminado del número máximo de errores durante este período es *n*-1, donde *n* es el número de nodos de WSFC. Para cambiar los valores del umbral de error de un grupo de disponibilidad determinado, use la consola del administrador de conmutación por error de WSFC.  
  
  
  
##  <a name="HCtimeout"></a> Umbral de tiempo de espera de comprobación de estado  
 La DLL de recursos del clúster WSFC del grupo de disponibilidad realiza una *comprobación de estado* de la réplica principal, llamando al procedimiento almacenado [sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) en la instancia de SQL Server que hospeda la réplica principal. **sp_server_diagnostics** devuelve resultados en un intervalo que iguala 1/3 del umbral de tiempo de espera de comprobación de estado del grupo de disponibilidad. El umbral de tiempo de espera de comprobación de estado predeterminado es 30 segundos, lo que hace que **sp_server_diagnostics** devuelva en un intervalo de 10 segundos. Si **sp_server_diagnostics** es lento o no devuelve información, la DLL de recursos esperará al intervalo completo del umbral de tiempo de espera de comprobación de estado antes de determinar que la réplica primaria no responde. Si la réplica primaria no responde, se inicia una conmutación automática por error, si se admite actualmente.  
  
> [!IMPORTANT]  
>  **sp_server_diagnostics** no realiza comprobaciones de estado en el nivel de base de datos.  
  
##  <a name="FClevel"></a> Nivel de condición de error  
 Si **sp_server_diagnostics** devuelve los datos de diagnóstico y la información de estado, se garantiza que una conmutación automática por error dependa del nivel de condición de error del grupo de disponibilidad. El *nivel de condición de error* especifica qué condiciones de error desencadenan una conmutación automática por error. Hay cinco niveles de condición de error que abarcan desde el nivel menos restrictivo (nivel uno) al más restrictivo (nivel cinco). Un nivel dado abarca los niveles menos restrictivos. Así pues, el nivel de condición más estricto, cinco, incluye las condiciones menos restrictivas, y así sucesivamente.  
  
> [!IMPORTANT]  
>  Ningún nivel de condición de error detecta las bases de datos dañadas ni las bases de datos sospechosas. Por tanto, una base de datos que está dañada o es sospechosa (debido a un error de hardware, a daños en los datos o a otro problema) nunca desencadena una conmutación automática por error.  
  
 En la tabla siguiente se describen las condiciones de error correspondientes a cada nivel.  
  
|Nivel|Condición de error|[!INCLUDE[tsql](../../../includes/tsql-md.md)] Valor|Valor de PowerShell|  
|-----------|-----------------------|------------------------------|----------------------|  
|Uno|Por inactividad de servidor. Este es el nivel menos restrictivo. Especifica que se inicia una conmutación automática por error en los casos siguientes:<br /><br /> El servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está inactivo.<br /><br /> La concesión del grupo de disponibilidad para conectarse al clúster de WSFC expira porque no se ha recibido ninguna confirmación de la instancia del servidor. Para más información, vea [Cómo funciona: Tiempo de espera de concesión de AlwaysOn SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx).|1|`OnServerDown`|  
|Dos|Al dejar de responder el servidor. Especifica que se inicia una conmutación automática por error en los casos siguientes:<br /><br /> La instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se conecta al clúster y se ha superado el umbral de tiempo de espera de comprobación de estado del grupo de disponibilidad definido por el usuario.<br /><br /> La réplica de disponibilidad tiene un estado de error.|2|`OnServerUnresponsive`|  
|Tres|En errores de servidor críticos. Especifica que se inicia una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] graves, como bloqueos por subproceso huérfanos, infracciones serias de acceso de escritura o volcado excesivo. Es el nivel predeterminado.|3|`OnCriticalServerError`|  
|Cuatro|En errores de servidor moderados. Especifica que se inicia una conmutación automática por error en caso de errores internos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] moderados, tales como una condición persistente de falta de memoria en el grupo de recursos de servidor interno de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|4|`OnModerateServerError`|  
|Cinco|En cualquier condición de error apta. Es el nivel más restrictivo. Especifica que se inicia una conmutación automática por error en el caso de condiciones de error aptas, incluidas las siguientes:<br /><br /> Se han agotado los subprocesos de trabajo del motor de SQL.<br /><br /> Detección de un interbloqueo irresoluble.|5|`OnAnyQualifiedFailureConditions`|  
  
> [!NOTE]  
>  La falta de respuesta de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a solicitudes del cliente no es pertinente a los grupos de disponibilidad.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
 **Para configurar la conmutación automática por error**  
  
-   [Cambiar el modo de disponibilidad de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-availability-mode-of-an-availability-replica-sql-server.md) (la conmutación automática por error necesita el modo de disponibilidad de confirmación sincrónica)  
  
-   [Cambiar el modo de conmutación por error de una réplica de disponibilidad &#40;SQL Server&#41;](change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
-   [Configurar la directiva de conmutación por error Flexible para controlar las condiciones para la conmutación por error automática (grupos de disponibilidad AlwaysOn)](configure-flexible-automatic-failover-policy.md)  
  
##  <a name="RelatedContent"></a> Contenido relacionado  
  
-   [Cómo funciona: Tiempo de espera de concesión de AlwaysOn SQL Server](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx)  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Modos de disponibilidad (grupos de disponibilidad AlwaysOn)](availability-modes-always-on-availability-groups.md)   
 [Conmutación por error y modos de conmutación por error &#40;grupos de disponibilidad AlwaysOn&#41;](failover-and-failover-modes-always-on-availability-groups.md)   
 [Clústeres de conmutación por error de Windows Server &#40;WSFC&#41; con SQL Server](../../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)   
 [Directiva de conmutación por error para instancias de clústeres de conmutación por error](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)   
 [sp_server_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)  
  
  
