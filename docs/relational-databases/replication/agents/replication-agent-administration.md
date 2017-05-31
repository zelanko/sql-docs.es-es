---
title: "Administración del Agente de replicación | Microsoft Docs"
ms.custom: 
ms.date: 08/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Snapshot Agent, administering
- Log Reader Agent, administering
- Queue Reader Agent, administering
- shared agents [SQL Server replication]
- Merge Agent, administering
- Distribution Agent, administering
- agents [SQL Server replication], administering
- replication cleanup jobs [SQL Server]
- administering replication, agents
- replication [SQL Server], administering
- independent agents [SQL Server replication]
ms.assetid: f27186b8-b1b2-4da0-8b2b-91f632c2ab7e
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ee0ddd687702068508c54ea60a533fc3c5c75b10
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="replication-agent-administration"></a>Administración del Agente de replicación
  Los agentes de replicación realizan muchas tareas asociadas con la replicación, lo que incluye la creación de copias de esquema y datos, detección de actualizaciones en el publicador o el suscriptor, y propagación de cambios entre servidores. De manera predeterminada, los agentes de replicación se ejecutan en los pasos de trabajo del Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Los agentes son simples ejecutables, por lo que se les puede llamar directamente desde la línea de comandos o desde scripts de proceso por lotes. Cada agente de replicación admite un conjunto de parámetros en tiempo de ejecución que se utilizan para controlar cómo se ejecuta; estos parámetros se especifican en un perfil de agente o en la línea de comandos.  
  
> [!IMPORTANT]  
>  De manera predeterminada, el servicio del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está deshabilitado cuando se instala [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , a menos que se elija explícitamente iniciar el servicio automáticamente durante la instalación.  
  
 Los archivos del agente de replicación se encuentran en [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]\COM. En la tabla siguiente se enumeran los nombres de los ejecutables y de los archivos de replicación. Haga clic en el vínculo de un agente para ver la referencia de parámetros.  
  
|Ejecutable del agente|Nombre de archivo|  
|----------------------|---------------|  
|[Agente de instantáneas de replicación](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|snapshot.exe|  
|[Agente de distribución de replicación](../../../relational-databases/replication/agents/replication-distribution-agent.md)|distrib.exe|  
|[Agente de registro del LOG de replicación](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|logread.exe|  
|[Agente de lectura de cola de replicación](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|qrdrsvc.exe|  
|[Agente de mezcla de replicación](../../../relational-databases/replication/agents/replication-merge-agent.md)|replmerg.exe|  
  
 Además de los trabajos de los agentes de replicación, la replicación tiene una serie de trabajos que realizan el mantenimiento a petición y programado.  
  
 **Para ejecutar trabajos de agentes y de mantenimiento**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y Monitor de replicación: [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   Programación de replicación: [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
## <a name="agent-profiles"></a>Perfiles de agente  
 Cuando se configura la replicación, se instala un conjunto de perfiles de agente en el distribuidor. Un perfil de agente contiene un conjunto de parámetros que se usan cada vez que se ejecuta un agente: cada agente inicia una sesión en el distribuidor durante su proceso de inicio y consulta los parámetros de su perfil. La replicación proporciona un perfil predeterminado para cada agente y perfiles predefinidos adicionales para el Agente de registro del LOG, el Agente de distribución y el Agente de mezcla. Además de los perfiles proporcionados, puede crear perfiles adecuados a los requisitos de su aplicación. Para obtener más información, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 Para obtener información sobre cómo especificar los parámetros de la línea de comandos directamente, vea [Conceptos de los ejecutables del Agente de replicación](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="monitoring-replication-agents"></a>Supervisar agentes de replicación  
 El Monitor de replicación le permite ver información y realizar tareas asociadas con cada agente de replicación. En la siguiente lista se incluye cada agente, las pestañas del Monitor de replicación en las que se puede encontrar y un vínculo a un tema en el que se explica el modo de obtener acceso a dichas pestañas:  
  
-   Los siguientes agentes están asociados con publicaciones en el Monitor de replicación:  
  
    -   Agente de instantáneas  
  
    -   Agente de registro del LOG  
  
    -   Agente de lectura de cola  
  
     Obtenga acceso a la información y a las tareas asociadas con estos agentes a través de la pestaña **Agentes** . Para obtener más información, vea [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
-   Los siguientes agentes están asociados con suscripciones en el Monitor de replicación:  
  
    -   Agente de distribución  
  
    -   Agente de mezcla  
  
     Obtenga acceso a la información y a las tareas asociadas a cada uno de estos agentes a través de las siguientes pestañas: **Lista de supervisión de suscripciones** (disponible para todos los publicadores) o **Todas las suscripciones** (disponible para todas las publicaciones). Para obtener más información, vea [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
## <a name="independent-and-shared-agents"></a>Agentes independientes y compartidos  
 Un agente independiente es un agente que da servicio a una suscripción. Un agente compartido da servicio a varias suscripciones. Cuando varias suscripciones que utilizan el mismo agente tienen que sincronizarse, de manera predeterminada esperan en una cola y el agente compartido da servicio a cada una de ellas al mismo tiempo. La latencia se reduce cuando se utilizan agentes independientes porque el agente está preparado siempre que es necesario sincronizar la suscripción. La replicación de mezcla siempre utiliza agentes independientes, y la replicación transaccional utiliza de manera predeterminada agentes independientes para las publicaciones creadas en el Asistente para nueva publicación (en versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la replicación transaccional utilizaba agentes compartidos de manera predeterminada).  
  
## <a name="replication-maintenance-jobs"></a>Trabajos de mantenimiento de replicación  
 La replicación utiliza los siguientes trabajos para realizar el mantenimiento a petición y programado.  
  
|Trabajo de limpieza|Descripción|Programación predeterminada|  
|------------------|-----------------|----------------------|  
|Limpieza de historial del agente: distribución|Quita de la base de datos de distribución el historial del agente de replicación.|Se ejecuta cada diez minutos.|  
|Limpieza de la distribución: distribución|Quita las transacciones replicadas de la base de datos de distribución. Desactiva las suscripciones que no se han sincronizado dentro del período de retención máximo de la distribución.|Se ejecuta cada diez minutos.|  
|Limpieza de suscripciones expiradas|Detecta y quita las suscripciones expiradas de las bases de datos de publicaciones.|Se ejecuta cada día a las 01:00 a.m.|  
|Reinicializar suscripciones con errores de validación de datos|Detecta todas las suscripciones con errores de validación de datos y las marca para reinicializarse. La próxima vez que se ejecute el Agente de mezcla o el Agente de distribución, se aplicará una nueva instantánea a los suscriptores.|No existe programación predeterminada (no se habilita de forma predeterminada).|  
|Comprobación de agentes de replicación|Detecta los agentes de replicación que no registran activamente un historial. Escribe en el registro de eventos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows si se produce un error en un trabajo.|Se ejecuta cada diez minutos.|  
|Actualizador de supervisión de replicación para distribución|Actualiza las consultas almacenadas en la caché que utiliza el Monitor de replicación.|Se ejecuta continuamente.|  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  

