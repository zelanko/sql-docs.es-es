---
title: "Ver comandos replicados y otra informaci&#243;n en la base de datos de distribuci&#243;n (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_browsereplcmds"
  - "replicación transaccional, supervisar"
  - "bases de datos de distribución [replicación de SQL Server], ver comandos replicados"
  - "ver comandos replicados"
ms.assetid: 9c20acec-8fab-4483-b9c1-dfe3768f85dd
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Ver comandos replicados y otra informaci&#243;n en la base de datos de distribuci&#243;n (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  Al utilizar la replicación transaccional, los comandos de transacción están almacenados en la base de datos de distribución hasta que el Agente de distribución los propaga a todos los suscriptores o un Agente de distribución del suscriptor extrae los cambios. Estos comandos pendientes en la base de datos de distribución se pueden ver utilizando mediante programación los procedimientos almacenados de replicación. Para obtener más información, consulte [procedimientos almacenados de replicación & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).  
  
### Para ver los comandos replicados de todas las publicaciones transaccionales en la base de datos de distribución  
  
1.  En el distribuidor en la base de datos de distribución, ejecute [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md).  
  
### Para ver los comandos replicados en la base de datos de distribución de un artículo concreto o de una base de datos concreta publicada utilizando replicación transaccional  
  
1.  (Opcional) En el publicador de la base de datos de publicación, ejecute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Especifique **@publication** y **@article**. Anote el valor de **article** del conjunto de resultados.  
  
2.  En el distribuidor en la base de datos de distribución, ejecute [sp_browsereplcmds](../../../relational-databases/system-stored-procedures/sp-browsereplcmds-transact-sql.md). (Opcional) Especifique el identificador de artículo del paso 2 para **@article_id**. (Opcional) Especifique el identificador de la base de datos de publicación para **@publisher_database_id**, que puede obtenerse desde el **database_id** columna en el [sys.databases](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo.  
  
## Vea también  
 [Supervisar la replicación mediante programación](../../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  