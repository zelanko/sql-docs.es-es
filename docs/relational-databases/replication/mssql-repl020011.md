---
title: "MSSQL_REPL020011 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_REPL020011"
ms.assetid: f72072d7-bbb6-48ad-ac88-afa74aeb4d58
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_REPL020011
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|20011|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|El proceso no pudo ejecutar '%1' en '%2'.|  
  
## Explicación  
 Este error se puede generar en una serie de circunstancias durante el procesamiento, como cuando se ejecuta el agente de lector del registro de la replicación transaccional **sp_replcmds** (el proceso no pudo ejecutar 'sp_replcmds' en \< nombreDeServidor>) o **sp_repldone** (el proceso no pudo ejecutar 'sp_repldone' en \< nombreDeServidor>).  
  
## Acción del usuario  
 Si este error se produce en una base de datos que acaba de restaurar una copia de seguridad, asegúrese de haber seguido los pasos descritos en la documentación de copia de seguridad y restauración, incluida la ejecución de **sp_replrestart** Si es necesario. Para más información, consulte [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
 Se trata de un error de procesamiento interno y si se genera en circunstancias diferentes a una restauración, normalmente indica que la replicación se debe quitar y volver a configurar. Si no puede quitar la replicación, póngase en contacto con el soporte técnico para obtener ayuda.  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [sp_replcmds & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)  
  
  