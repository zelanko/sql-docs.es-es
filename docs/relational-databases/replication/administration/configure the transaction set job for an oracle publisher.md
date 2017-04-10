---
title: "Configurar el trabajo del conjunto de transacciones para un publicador de Oracle (programaci&#243;n de la replicaci&#243;n con Transact-SQL) | Microsoft Docs"
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
  - "sp_publisherproperty"
  - "publicación de Oracle [replicación de SQL Server], configurar"
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Configurar el trabajo del conjunto de transacciones para un publicador de Oracle (programaci&#243;n de la replicaci&#243;n con Transact-SQL)
  El trabajo **Xactset** es un trabajo de base de datos de Oracle creado por replicación que se ejecuta en un publicador de Oracle para crear conjuntos de transacciones cuando el agente de registro del LOG no está conectado al publicador. Puede habilitar y configurar este trabajo desde el distribuidor mediante programación con procedimientos almacenados de replicación. Para obtener más información, consulte [ajuste del rendimiento de los publicadores de Oracle](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).  
  
### Para habilitar el trabajo del conjunto de transacciones  
  
1.  En el publicador de Oracle, establezca la **job_queue_processes** parámetro de inicialización en un valor suficiente para permitir la ejecución del trabajo Xactset. Para obtener más información acerca de este parámetro, vea la documentación de la base de datos del publicador de Oracle.  
  
2.  En el distribuidor, ejecute [sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique el nombre del publicador de Oracle en **@publisher**, un valor **xactsetbatching** en **@propertyname**y un valor **enabled** en **@propertyvalue**.  
  
3.  En el distribuidor, ejecute [sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique el nombre del publicador de Oracle en **@publisher**, un valor **xactsetjobinterval** en **@propertyname**y el intervalo del trabajo, en minutos, en **@propertyvalue**.  
  
4.  En el distribuidor, ejecute [sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique el nombre del publicador de Oracle en **@publisher**, un valor **xactsetjob** en **@propertyname**y un valor **enabled** en **@propertyvalue**.  
  
### Para configurar el trabajo del conjunto de transacciones  
  
1.  (Opcional) En el distribuidor, ejecute [sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique el nombre del publicador de Oracle en **@publisher**. De esta forma se devuelven las propiedades del trabajo **Xactset** al publicador.  
  
2.  En el distribuidor, ejecute [sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique el nombre del publicador de Oracle en **@publisher**, el nombre de la propiedad del trabajo Xactset que se establece en **@propertyname**y la nueva configuración en **@propertyvalue**.  
  
3.  (Opcional) Repita el paso 2 para cada propiedad del trabajo Xactset que se establece. Al cambiar la propiedad **xactsetjobinterval** , debe reiniciar el trabajo en el publicador de Oracle para que se aplique el nuevo intervalo.  
  
### Para ver las propiedades del trabajo del conjunto de transacciones  
  
1.  En el distribuidor, ejecute [sp_helpxactsetjob](../../../relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql.md). Especifique el nombre del publicador de Oracle en **@publisher**.  
  
### Para deshabilitar el trabajo del conjunto de transacciones  
  
1.  En el distribuidor, ejecute [sp_publisherproperty & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql.md). Especifique el nombre del publicador de Oracle en **@publisher**, un valor **xactsetjob** en **@propertyname**y un valor **disabled** en **@propertyvalue**.  
  
## Ejemplo  
 El ejemplo siguiente habilita el trabajo `Xactset` y establece un intervalo de tres minutos entre ejecuciones.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../relational-databases/replication/codesnippet/tsql/configure-the-transactio_1.sql)]  
  
## Vea también  
 [Optimizar el rendimiento de publicadores de Oracle](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  