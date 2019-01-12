---
title: MSSQL_ENG014151 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014151 error
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f292841c227db26f1c518b2eaef896f7ce3570c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54134626"
---
# <a name="mssqleng014151"></a>MSSQL_ENG014151
    
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
  
-   Reinicie el agente en el que se ha producido el error para ver si se ejecuta correctamente. Para obtener más información, vea [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) y [Conceptos de los ejecutables del Agente de replicación](concepts/replication-agent-executables-concepts.md).  
  
-   Compruebe el historial del agente y el historial de trabajos para ver otros errores que se hayan producido aproximadamente a la misma hora. Para obtener información acerca de cómo ver los detalles de error y de estado del agente en el Monitor de replicación, vea [ver información y realizar tareas con el Monitor de replicación](monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
-   Compruebe que la conectividad básica funciona entre los equipos a los que el agente tiene acceso y, a continuación, conecte a cada equipo con una herramienta como [sqlcmd Utility](../../tools/sqlcmd-utility.md). Para conectar, utilice la misma cuenta con la que el agente realiza las conexiones. Para obtener más información acerca de los permisos que necesita cada cuenta de agente, vea [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
-   Si se producen errores al crear o aplicar una instantánea, compruebe los archivos del directorio de la instantánea.  
  
-   Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error o a mensajes de error adicionales.  
  
## <a name="see-also"></a>Vea también  
 [Administración del Agente de replicación](agents/replication-agent-administration.md)   
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)   
 [Agente de distribución de replicación](agents/replication-distribution-agent.md)   
 [Agente de registro del LOG de replicación](agents/replication-log-reader-agent.md)   
 [Agente de mezcla de replicación](agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](agents/replication-queue-reader-agent.md)   
 [Agente de instantáneas de replicación](agents/replication-snapshot-agent.md)  
  
  
