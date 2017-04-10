---
title: "MSSQL_ENG020554 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG020554"
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG020554
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|20554|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|El agente de replicación no ha registrado un mensaje de progreso en %ld minutos. Esto podría indicar que un agente no responde o una gran actividad en el sistema. Compruebe que se están replicando los registros en el destino y que las conexiones al suscriptor, publicador y distribuidor están activas.|  
  
## Explicación  
 El **comprobación de agentes de replicación** trabajo se ejecuta en un intervalo especificado (10 minutos de forma predeterminada) para comprobar el estado de cada agente de replicación. Si un agente no ha registrado ningún progreso desde la última vez que se ejecutó el trabajo de comprobación del agente, se puede generar el error MSSQL_ENG020554. Se espera que el agente registre al menos los mensajes del historial incluso si no se produce ninguna otra actividad de replicación. Aunque el agente de replicación no está respondiendo como se esperaba, no necesariamente se ha detenido ni se ha producido un error (si se ha producido un error en un agente, se genera el error MSSQL_ENG020536).  
  
 Los siguientes problemas pueden dar como resultado que se genere el error MSSQL_ENG020554:  
  
-   El agente está ocupado.  
  
     Si el agente está demasiado ocupado para responder cuando el trabajo de comprobación del agente le sondea, el trabajo de comprobación del agente no podrá informar de si el agente de replicación está funcionando correctamente. Existen una serie de razones por las que el agente de replicación puede estar ocupado: puede que se estén replicando muchos datos o que haya problemas en el diseño o la configuración de la aplicación que den como resultado procesos que se ejecutan durante un período de tiempo prolongado.  
  
-   El agente no puede iniciar sesión en uno de los equipos de la topología.  
  
     Todos los agentes tienen un parámetro **- LoginTimeOut** (establecido en 15 segundos de forma predeterminada), que controla el tiempo que un agente intenta iniciar sesión en un nodo de replicación, como un agente de mezcla que inicie sesión en el publicador. Si el **- LoginTimeOut** valor es mayor que el intervalo en el que se ejecuta el trabajo de comprobación del agente de replicación, un problema de inicio de sesión podría ser la causa del error: error MSSQL_ENG020554 se genera antes de que el agente se pueda generar un error más específico.  
  
## Acción del usuario  
 La acción requerida depende de la causa del error.  
  
-   Para todos los casos en los que se genera el error:  
  
     Compruebe los detalles del error en el Monitor de replicación y, a continuación, reinicie el agente si se ha detenido. Los detalles del error pueden ofrecer información adicional sobre el motivo por el que el agente no se estaba ejecutando correctamente. Si el agente se está ejecutando, no lo detenga y lo reinicie porque esto puede agravar el problema. Para obtener información sobre el modo de ver el estado del agente y los detalles del error en el Monitor de replicación, vea los siguientes temas:  
  
    -   Para el agente de instantáneas, agente de lector del registro y el agente de lector de cola, consulte [Ver información y realizar tareas para los agentes asociados con una publicación & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
    -   Para el agente de distribución y el agente de mezcla, vea [Ver información y realizar tareas para los agentes asociados a una suscripción & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view information and perform tasks for subscription agents.md).  
  
-   Si este error se genera con frecuencia porque el agente está ocupado:  
  
     Es posible que tenga que volver a diseñar la aplicación para que el agente pase menos tiempo procesando.  
  
     Puede incrementar el intervalo en el que el estado del agente se comprueba usando el cuadro de diálogo **Propiedades del trabajo** . Para obtener información sobre el acceso a este cuadro de diálogo para trabajos de replicación, consulte [Ver información y realizar tareas para un publicador & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md).  
  
-   Si un agente no puede iniciar sesión en uno de los equipos de la topología:  
  
     Se recomienda que el **- LoginTimeOut** Establecer valor menor que el intervalo en el que se ejecuta el trabajo de comprobación del agente de replicación. En algunos casos, el valor de **- LoginTimeOut** se establece mayor debido a problemas de red que provocan los inicios de sesión para el tiempo de espera. Si el **- LoginTimeOut** se establece inferior, la replicación puede informar de errores más específicos, lo que le permite solucionar problemas de inicio de sesión que podrían deberse a permisos, problemas de red u otros problemas. Los parámetros del agente se pueden especificar en los perfiles del agente y en la línea de comandos. Para obtener más información, vea:  
  
    -   [Trabajar con perfiles del Agente de replicación](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Ver y modificar los parámetros de línea de comandos del agente de replicación & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/view and modify replication agent command prompt parameters.md)  
  
    -   [Conceptos de los ejecutables del agente de replicación](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Vea también  
 [Administración del Agente de replicación](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de distribución de replicación](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente de registro del LOG de replicación](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de mezcla de replicación](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Agente de instantáneas de replicación](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  