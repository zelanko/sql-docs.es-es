---
title: "MSSQL_ENG018752 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG018752"
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018752
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|18752|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|El Agente de registro del LOG y los procedimientos relacionados con el registro (sp_repldone, sp_replcmds y sp_replshowcmds) solamente pueden conectarse a la base de datos de uno en uno. Si ejecutó un procedimiento relacionado con el registro, quite la conexión mediante la cual se ejecutó el procedimiento o ejecute sp_replflush en esa conexión antes de iniciar el Agente de registro del LOG o de ejecutar otro procedimiento relacionado con el registro.|  
  
## Explicación  
 Más de una conexión actual está intentando ejecutar alguno de los siguientes: **sp_repldone**, **sp_replcmds**, o **sp_replshowcmds**. Los procedimientos almacenados [sp_repldone & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) y [sp_replcmds & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) procedimientos almacenados utilizan el agente de lector del registro para buscar y actualizar información sobre transacciones replicadas en una base de datos publicada. El procedimiento almacenado [sp_replshowcmds & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) se utiliza para solucionar cierto tipo de problemas con la replicación transaccional.  
  
 Este error se produce bajo las siguientes circunstancias:  
  
-   Si se está ejecutando el Agente de registro del LOG en una base de datos publicada y un segundo Agente de registro del LOG intenta ejecutarse en la misma base de datos, se produce el error en el segundo agente y aparece en el historial del agente.  
  
     En una situación en la que parece haber varios agentes, es posible que uno de ellos sea el resultado de un proceso huérfano.  
  
-   Si se inicia el agente de lector del registro para una base de datos publicada y un usuario ejecuta **sp_repldone**, **sp_replcmds**, o **sp_replshowcmds** en la misma base de datos, se produce el error en la aplicación donde se ejecutó el procedimiento almacenado (como **sqlcmd**).  
  
-   Si no está ejecutando ningún agente de lector del registro para una base de datos publicada y un usuario ejecuta **sp_repldone**, **sp_replcmds**, o **sp_replshowcmds** y, a continuación, no cierra la conexión en la que se ejecutó el procedimiento, el error se produce cuando el agente de lector del registro intenta conectarse a la base de datos.  
  
## Acción del usuario  
 Los siguientes pasos pueden ayudar a resolver el problema. Si un paso permite al Agente de registro del LOG iniciarse sin errores, no es necesario completar los pasos restantes.  
  
-   Compruebe en el historial del Agente de registro del LOG otros errores que podrían contribuir a este error. Para obtener información acerca de cómo ver los detalles de error y de estado del agente en el Monitor de replicación, consulte [Ver información y realizar tareas para los agentes asociados con una publicación & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md).  
  
-   Compruebe la salida de [sp_who & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) números de identificación de proceso específico (SPID) que están conectados a la base de datos publicada. Cierre todas las conexiones que puedan haber ejecutado **sp_repldone**, **sp_replcmds**, o **sp_replshowcmds**.  
  
-   Reinicie el Agente de registro del LOG. Para obtener más información, consulte [iniciar y detener un agente de replicación & #40; SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   Reinicie el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (déjelo sin conexión o conéctelo en un clúster) en el distribuidor. Si no hay posibilidad de que un trabajo programado pueda haber ejecutado **sp_repldone**, **sp_replcmds**, o **sp_replshowcmds** de cualquier otro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la instancia, reinicie el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente para esas instancias también. Para obtener más información, consulte [iniciar, detener o pausar el servicio Agente SQL Server](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md).  
  
-   Ejecutar [sp_replflush & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) en el publicador en la base de datos de publicación y, a continuación, reinicie el agente de lector del registro.  
  
-   Si el error persiste, aumente el registro del agente y especifique un archivo de salida para el registro. Dependiendo del contexto del error, esto puede proporcionar los pasos que conducen al error o a mensajes de error adicionales.  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Agente de registro del LOG de replicación](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  