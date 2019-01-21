---
title: MSSQL_ENG014151 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014151 error
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fe24bc816174f7e3ee21d91bd7c2028427655e3c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133116"
---
# <a name="mssqleng014151"></a>MSSQL_ENG014151
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14151|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Replicación-%s: error en el agente %s. %s|  
  
## <a name="explanation"></a>Explicación  
 Este error se produce en caso de fallo del agente de replicación. El texto al final del mensaje depende del contexto del error.  
  
## <a name="user-action"></a>Acción del usuario  
 Este error se puede producir en una serie de situaciones; aplique las siguientes soluciones según corresponda:  
  
-   Reinicie el agente en el que se ha producido el error para ver si se ejecuta correctamente. Para obtener más información, vea [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [Conceptos de los ejecutables del Agente de replicación](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
-   Compruebe el historial del agente y el historial de trabajos para ver otros errores que se hayan producido aproximadamente a la misma hora. Para obtener información sobre la visualización del estado y los errores en Monitor de replicación, vea [Visualización de información y realización de tareas mediante el Monitor de replicación](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
-   Compruebe que la conectividad básica funciona entre los equipos a los que el agente tiene acceso y, a continuación, conecte a cada equipo con una herramienta como [sqlcmd Utility](../../tools/sqlcmd-utility.md). Para conectar, utilice la misma cuenta con la que el agente realiza las conexiones. Para obtener más información acerca de los permisos que necesita cada cuenta de agente, vea [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Si se producen errores al crear o aplicar una instantánea, compruebe los archivos del directorio de la instantánea. 
  
-   Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error o a mensajes de error adicionales.  
  
## <a name="see-also"></a>Consulte también  
 [Administración del Agente de replicación](../../relational-databases/replication/agents/replication-agent-administration.md)   
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de distribución de replicación](../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente de registro del LOG de replicación](../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de mezcla de replicación](../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](../../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Agente de instantáneas de replicación](../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
