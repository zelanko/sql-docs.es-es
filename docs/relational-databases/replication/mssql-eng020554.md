---
title: MSSQL_ENG020554 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020554 error
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 40454c042381db8e7f4165e72a40d0ccbf30e176
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353167"
---
# <a name="mssqleng020554"></a>MSSQL_ENG020554
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|20554|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|El agente de replicación no ha registrado un mensaje de progreso en %ld minutos. Esto podría indicar que un agente no responde o una gran actividad en el sistema. Compruebe que se están replicando los registros en el destino y que las conexiones al suscriptor, publicador y distribuidor están activas.|  
  
## <a name="explanation"></a>Explicación  
 El trabajo **Comprobación de agentes de replicación** se ejecuta con un intervalo especificado (10 minutos de manera predeterminada) para comprobar el estado de cada agente de replicación. Si un agente no ha registrado ningún progreso desde la última vez que se ejecutó el trabajo de comprobación del agente, se puede generar el error MSSQL_ENG020554. Se espera que el agente registre al menos los mensajes del historial incluso si no se produce ninguna otra actividad de replicación. Aunque el agente de replicación no está respondiendo como se esperaba, no necesariamente se ha detenido ni se ha producido un error (si se ha producido un error en un agente, se genera el error MSSQL_ENG020536).  
  
 Los siguientes problemas pueden dar como resultado que se genere el error MSSQL_ENG020554:  
  
-   El agente está ocupado.  
  
     Si el agente está demasiado ocupado para responder cuando el trabajo de comprobación del agente le sondea, el trabajo de comprobación del agente no podrá informar de si el agente de replicación está funcionando correctamente. Existen una serie de razones por las que el agente de replicación puede estar ocupado: puede que se estén replicando muchos datos o que haya problemas en el diseño o la configuración de la aplicación que den como resultado procesos que se ejecutan durante un período de tiempo prolongado.  
  
-   El agente no puede iniciar sesión en uno de los equipos de la topología.  
  
     Todos los agentes tienen un parámetro **-LoginTimeOut** (establecido en 15 segundos de manera predeterminada), que controla el tiempo que un agente intenta iniciar sesión en un nodo de replicación, por ejemplo, como Agente de mezcla que inicia sesión en el publicador. Si el valor **-LoginTimeOut** está establecido en un valor mayor que el intervalo en el que se ejecuta el trabajo de comprobación del agente de replicación, un problema de inicio de sesión podría ser la causa raíz del error: el error MSSQL_ENG020554 se genera antes de que el agente pueda generar un error más específico.  
  
## <a name="user-action"></a>Acción del usuario  
 La acción requerida depende de la causa del error.  
  
-   Para todos los casos en los que se genera el error:  
  
     Compruebe los detalles del error en el Monitor de replicación y, a continuación, reinicie el agente si se ha detenido. Los detalles del error pueden ofrecer información adicional sobre el motivo por el que el agente no se estaba ejecutando correctamente. Si el agente se está ejecutando, no lo detenga y lo reinicie porque esto puede agravar el problema. Para obtener información sobre el modo de ver el estado del agente y los detalles del error en el Monitor de replicación, vea los siguientes temas:  
  
    -   Para el Agente de instantáneas, el Agente de registro del LOG y el Agente de lectura de cola, vea [Cómo ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
    -   Para el Agente de distribución y el Agente de mezcla, vea [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
-   Si este error se genera con frecuencia porque el agente está ocupado:  
  
     Es posible que tenga que volver a diseñar la aplicación para que el agente pase menos tiempo procesando.  
  
     Puede incrementar el intervalo en el que el estado del agente se comprueba usando el cuadro de diálogo **Propiedades del trabajo** . Para obtener información sobre el acceso a este cuadro de diálogo para trabajos de replicación, vea [Ver información y realizar tareas para un publicador &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md).  
  
-   Si un agente no puede iniciar sesión en uno de los equipos de la topología:  
  
     Se recomienda que establezca **-LoginTimeOut** en un valor inferior al intervalo en el que se ejecuta el trabajo de comprobación del agente de replicación. En algunos casos, **-LoginTimeOut** se establece en un valor mayor debido a problemas de red que causan que los inicios de sesión agoten el tiempo de espera. Si **-LoginTimeOut** se establece en un valor menor, la replicación puede informar sobre errores más específicos, lo que le permite solucionar problemas de inicio de sesión que pueden estar causados por permisos, problemas de red u otros factores. Los parámetros del agente se pueden especificar en los perfiles del agente y en la línea de comandos. Para obtener más información, vea:  
  
    -   [Trabajar con perfiles del Agente de replicación](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Ver y modificar parámetros del símbolo del sistema de los agentes de replicación &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Ver también  
 [Administración del Agente de replicación](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de distribución de replicación](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente de registro del LOG de replicación](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de mezcla de replicación](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
