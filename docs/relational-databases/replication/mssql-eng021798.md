---
title: "MSSQL_ENG021798 | Microsoft Docs"
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
  - "error MSSQL_ENG021798"
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG021798
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21798|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Debe agregar el trabajo de agente '%s' a través de '%s' antes de continuar. Vea la documentación de '%s'.|  
  
## Explicación  
 Para crear una publicación, debe ser miembro de la **sysadmin** rol fijo de servidor en el publicador o un miembro de la **db_owner** rol fijo de base de datos en la base de datos de publicación. Si es un miembro de la **db_owner** rol, este error se produce si:  
  
-   Se ejecutan scripts desde [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. El modelo de seguridad de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ha cambiado, por lo que dichos scripts deben actualizarse.  
  
-   El procedimiento almacenado **sp_addpublication** se ejecuta antes de ejecutar [sp_addlogreader_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Esto es aplicable a todas las publicaciones transaccionales.  
  
-   El procedimiento almacenado **sp_addpublication** se ejecuta antes de ejecutar [sp_addqreader_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Esto se aplica a las publicaciones transaccionales que están habilitadas para suscripciones de actualización en cola (un valor de TRUE para el **@allow_queued_tran** parámetro de **sp_addpublication**).  
  
 Los procedimientos almacenados **sp_addlogreader_agent** y **sp_addqreader_agent** cada uno crea un trabajo de agente y le permiten especificar el [!INCLUDE[msCoName](../../includes/msconame-md.md)] de cuenta de Windows bajo la que se ejecuta el agente. Para los usuarios de la **sysadmin** rol, trabajos del agente se crean implícitamente si **sp_addlogreader_agent** y **sp_addqreader_agent** no se ejecutan; agentes se ejecutan en el contexto de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio del agente en el distribuidor. Aunque **sp_addlogreader_agent** y **sp_addqreader_agent** no son necesarios para los usuarios de la **sysadmin** rol, es recomendable especificar una cuenta independiente para los agentes. Para más información, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## Acción del usuario  
 Asegúrese de ejecutar los procedimientos en el orden correcto. Para más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md). Si tiene scripts de replicación de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], actualice dichos scripts para incluir los procedimientos almacenados y los parámetros requeridos por [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Para obtener más información, consulte [Actualizar Scripts de replicación & #40; Programación de Transact-SQL de replicación & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  