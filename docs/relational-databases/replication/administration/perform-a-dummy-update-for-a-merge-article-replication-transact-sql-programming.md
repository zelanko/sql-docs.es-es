---
title: "Realizar una actualizaci&#243;n ficticia de un art&#237;culo de mezcla (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
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
  - "sp_mergedummyupdate"
  - "actualizaciones ficticias [replicación de SQL Server]"
ms.assetid: 2f339210-4d85-4843-bd94-e86f7100d3ef
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Realizar una actualizaci&#243;n ficticia de un art&#237;culo de mezcla (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  La replicación de mezcla utiliza los desencadenadores como parte del proceso de la replicación; cuando se actualiza una tabla tabla publicada, se activa un desencadenador de actualización. En algunos casos, los datos pueden actualizarse sin que el desencadenador se active, como durante las operaciones de UPDATETEXT y WRITETEXT. En estos casos, necesita agregar explícitamente una instrucción UPDATE ficticia para replicar el cambio. Puede agregar una instrucción UPDATE ficticia mediante los procedimientos almacenados de replicación.  
  
### Para agregar una instrucción UPDATE ficticia  
  
1.  Ejecute la operación (por ejemplo, UPDATETEXT) en una fila de una tabla publicada de mezcla que requiera una actualización ficticia.  
  
2.  En el servidor (publicador o suscriptor) en la base de datos donde se realizó el cambio, ejecute [sp_mergedummyupdate & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergedummyupdate-transact-sql.md). Especificar la tabla en la que se realizó el cambio para **@source_object**, y el identificador único de la fila modificada para **@rowguid**.  
  
3.  Sincronice la suscripción para replicar la fila cambiada.  
  
  