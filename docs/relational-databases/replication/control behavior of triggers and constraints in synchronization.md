---
title: "Controlar el comportamiento de desencadenadores y restricciones durante la sincronizaci&#243;n (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
ms.custom: ""
ms.date: "03/29/2017"
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
  - "identidades [replicación de SQL Server]"
  - "restricciones [SQL Server], replicación"
  - "desencadenadores [SQL Server], replicación"
  - "desencadenadores [replicación de SQL Server]"
  - "restricciones [replicación de SQL Server]"
  - "NOT FOR REPLICATION, opción"
  - "NFR, opción"
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Controlar el comportamiento de desencadenadores y restricciones durante la sincronizaci&#243;n (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  Durante la sincronización, ejecutan agentes de replicación [Insertar & #40; Transact-SQL & #41;](../../t-sql/statements/insert-transact-sql.md), [actualización & #40; Transact-SQL & #41;](../../t-sql/queries/update-transact-sql.md), y [Eliminar & #40; Transact-SQL & #41;](../../t-sql/statements/delete-transact-sql.md) instrucciones en las tablas replicadas, lo que pueden provocar la manipulación de datos desencadenadores DML (lenguaje) en estas tablas para ejecutarse. Hay casos en los que quizá necesite evitar que se activen estos desencadenadores o que se apliquen restricciones durante la sincronización. Este comportamiento depende de cómo se cree el desencadenador o la restricción.  
  
### Para evitar que los desencadenadores se ejecuten durante la sincronización  
  
1.  Al crear un nuevo desencadenador, especifique la opción NOT FOR REPLICATION de [CREATE TRIGGER & #40; Transact-SQL & #41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
2.  Para un desencadenador existente, especifique la opción NOT FOR REPLICATION de [ALTER TRIGGER & #40; Transact-SQL & #41;](../../t-sql/statements/alter-trigger-transact-sql.md).  
  
### Para evitar que se apliquen restricciones durante la sincronización  
  
1.  Al crear una nueva restricción CHECK o FOREIGN KEY, especifique la opción CHECK NOT FOR REPLICATION en la definición de restricción de [CREATE TABLE & #40; Transact-SQL & #41;](../../t-sql/statements/create-table-transact-sql.md).  
  
## Vea también  
 [Crear tablas & #40; el motor de base de datos & #41;](../../relational-databases/tables/create-tables-database-engine.md)  
  
  