---
title: "Habilitar copias de seguridad coordinadas para la replicaci&#243;n transaccional (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
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
  - "replicación transaccional, copia de seguridad y restauración"
  - "sp_replicationdboption"
  - "sincronización con copia de seguridad [replicación de SQL Server]"
  - "copias de seguridad coordinadas [replicación de SQL Server]"
  - "copias de seguridad [replicación de SQL Server], replicación transaccional"
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Habilitar copias de seguridad coordinadas para la replicaci&#243;n transaccional (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  Al habilitar una base de datos para la replicación transaccional, puede especificar que se tenga que realizar una copia de seguridad de todas las transacciones antes de ser entregadas a la base de datos de distribución. También puede habilitar la copia de seguridad coordinada en la base de datos de distribución para que el registro de transacciones de la base de datos de publicación no se trunque hasta que se haya realizado una copia de seguridad de las transacciones que se han propagado al distribuidor. Para más información, consulte [Strategies for Backing Up and Restoring Snapshot and Transactional Replication](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### Para habilitar las copias de seguridad coordinadas de una base de datos publicada con replicación transaccional  
  
1.  En el publicador, use la [DATABASEPROPERTYEX & #40; Transact-SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) función para devolver el **IsSyncWithBackup** propiedad de la base de datos de publicación. Si la función devuelve **1**, las copias de seguridad coordinadas ya están habilitadas para la base de datos publicada.  
  
2.  Si la función en el paso 1 devuelve **0**, ejecute [sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **sync with backup** para **@optname**y **true** para **@value**.  
  
    > [!NOTE]  
    >  Si cambia la opción **sync with backup** a **false**, el punto de la truncación de la base de datos de publicación estará actualizado después de que el Agente de registro del LOG se ejecute o después de un intervalo si el Agente de registro del LOG está ejecutando permanentemente. El intervalo máximo se controla mediante la **– MessageInterval** parámetro de agente (que tiene un valor predeterminado de 30 segundos).  
  
### Para habilitar las copias de seguridad coordinadas para una base de datos de distribución  
  
1.  En el distribuidor, utilice la [DATABASEPROPERTYEX & #40; Transact-SQL & #41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) función para devolver el **IsSyncWithBackup** propiedad de la base de datos de distribución. Si la función devuelve **1**, las copias de seguridad coordinadas ya están habilitadas para la base de datos de distribución.  
  
2.  Si la función en el paso 1 devuelve **0**, ejecute [sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) en el distribuidor de la base de datos de distribución. Especifique un valor de **sync with backup** para **@optname** y **true** para **@value**.  
  
### Para deshabilitar las copias de seguridad coordinadas  
  
1.  En el publicador de la base de datos de publicación o en el distribuidor de la base de datos de distribución, ejecute [sp_replicationdboption & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Especifique un valor de **sync with backup** para **@optname** y **false** para **@value**.  
  
  