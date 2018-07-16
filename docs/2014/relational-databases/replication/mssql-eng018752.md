---
title: MSSQL_ENG018752 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 14
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b905ecad9ec742ba7cbf3c380eefb8e73950302e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37290381"
---
# <a name="mssqleng018752"></a>MSSQL_ENG018752
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|18752|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|El Agente de registro del LOG y los procedimientos relacionados con el registro (sp_repldone, sp_replcmds y sp_replshowcmds) solamente pueden conectarse a la base de datos de uno en uno. Si ejecutó un procedimiento relacionado con el registro, quite la conexión mediante la cual se ejecutó el procedimiento o ejecute sp_replflush en esa conexión antes de iniciar el Agente de registro del LOG o de ejecutar otro procedimiento relacionado con el registro.|  
  
## <a name="explanation"></a>Explicación  
 Más de una conexión actual intenta ejecutar uno de los siguientes procedimientos: **sp_repldone**, **sp_replcmds**o **sp_replshowcmds**. [Sp_repldone &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-repldone-transact-sql) y [sp_replcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql) son procedimientos almacenados usados por el Agente de registro del LOG para buscar información sobre transacciones replicadas en una base de datos publicada y actualizarla. El procedimiento almacenado [sp_replshowcmds &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql) se usa para resolver ciertos tipos de problemas con la replicación transaccional.  
  
 Este error se produce bajo las siguientes circunstancias:  
  
-   Si se está ejecutando el Agente de registro del LOG en una base de datos publicada y un segundo Agente de registro del LOG intenta ejecutarse en la misma base de datos, se produce el error en el segundo agente y aparece en el historial del agente.  
  
     En una situación en la que parece haber varios agentes, es posible que uno de ellos sea el resultado de un proceso huérfano.  
  
-   Si se inicia el Agente de registro del LOG en una base de datos publicada y un usuario ejecuta **sp_repldone**, **sp_replcmds**o **sp_replshowcmds** en la misma base de datos, se produce el error en la aplicación donde se ejecutó el procedimiento almacenado (por ejemplo **sqlcmd**).  
  
-   Si no se está ejecutando el Agente de registro del LOG en una base de datos publicada y un usuario ejecuta **sp_repldone**, **sp_replcmds**o **sp_replshowcmds** y, a continuación, no cierra la conexión en la que se ejecutó el procedimiento, se produce el error cuando el Agente de registro del LOG intenta conectarse a la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
 Los siguientes pasos pueden ayudar a resolver el problema. Si un paso permite al Agente de registro del LOG iniciarse sin errores, no es necesario completar los pasos restantes.  
  
-   Compruebe en el historial del Agente de registro del LOG otros errores que podrían contribuir a este error. Para obtener información sobre la visualización del estado y los errores del agente del Monitor de replicación, vea [Ver información y realizar tareas para los agentes asociados a una publicación &#40;Monitor de replicación&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md).  
  
-   Compruebe el resultado de [sp_who &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) para los números de identificación de proceso específico (SPID) que estén conectados a la base de datos publicada. Cierre las conexiones que puedan haber ejecutado **sp_repldone**, **sp_replcmds**o **sp_replshowcmds**.  
  
-   Reinicie el Agente de registro del LOG. Para obtener más información, vea [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   Reinicie el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (déjelo sin conexión o conéctelo en un clúster) en el distribuidor. Si existe la posibilidad de que un trabajo programado pueda ejecutar **sp_repldone**, **sp_replcmds**o **sp_replshowcmds** desde cualquier otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reinicie también el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en esas instancias. Para obtener más información, vea [Iniciar, detener o pausar el servicio del Agente SQL Server](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
-   Ejecute [sp_replflush &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replflush-transact-sql) en el publicador de la base de datos de publicación y reinicie el Agente de registro del LOG.  
  
-   Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error o a mensajes de error adicionales.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)   
 [Agente de registro del LOG de replicación](agents/replication-log-reader-agent.md)  
  
  
