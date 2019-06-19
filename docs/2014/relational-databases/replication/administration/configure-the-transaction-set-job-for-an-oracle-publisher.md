---
title: Configurar el trabajo de conjunto de transacciones para un publicador de Oracle (programación de replicación Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfa83609f4040fc9875a63217b0e86d6a3ff99bc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187016"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Configurar el trabajo del conjunto de transacciones para un publicador de Oracle (programación de la replicación con Transact-SQL)
  El trabajo **Xactset** es un trabajo de base de datos de Oracle creado por replicación que se ejecuta en un publicador de Oracle para crear conjuntos de transacciones cuando el agente de registro del LOG no está conectado al publicador. Puede habilitar y configurar este trabajo desde el distribuidor mediante programación con procedimientos almacenados de replicación. Para obtener más información, consulte [Optimizar el rendimiento de publicadores de Oracle](../non-sql/performance-tuning-for-oracle-publishers.md).  
  
### <a name="to-enable-the-transaction-set-job"></a>Para habilitar el trabajo del conjunto de transacciones  
  
1.  En el publicador de Oracle, establezca el parámetro de inicialización **job_queue_processes** en un valor suficiente para permitir la ejecución del trabajo Xactset. Para obtener más información acerca de este parámetro, vea la documentación de la base de datos del publicador de Oracle.  
  
2.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador de Oracle en **@publisher** , un valor de `xactsetbatching` para **@propertyname** y un valor de `enabled` para **@propertyvalue** .  
  
3.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador de Oracle en **@publisher** , un valor de `xactsetjobinterval` para **@propertyname** y el intervalo del trabajo, en minutos, para **@propertyvalue** .  
  
4.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador de Oracle en **@publisher** , un valor de `xactsetjob` para **@propertyname** y un valor de `enabled` para **@propertyvalue** .  
  
### <a name="to-configure-the-transaction-set-job"></a>Para configurar el trabajo del conjunto de transacciones  
  
1.  (Opcional) En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador de Oracle en **@publisher** . De esta forma se devuelven las propiedades del trabajo **Xactset** al publicador.  
  
2.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador de Oracle en **@publisher** , el nombre de la propiedad del trabajo Xactset que se establece en **@propertyname** y la nueva configuración en **@propertyvalue** .  
  
3.  (Opcional) Repita el paso 2 para cada propiedad del trabajo Xactset que se establece. Al cambiar el `xactsetjobinterval` propiedad, debe reiniciar el trabajo en el publicador de Oracle para el nuevo intervalo surta efecto.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>Para ver las propiedades del trabajo del conjunto de transacciones  
  
1.  En el distribuidor, ejecute [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql). Especifique el nombre del publicador de Oracle en **@publisher** .  
  
### <a name="to-disable-the-transaction-set-job"></a>Para deshabilitar el trabajo del conjunto de transacciones  
  
1.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador de Oracle en **@publisher** , un valor de `xactsetjob` para **@propertyname** y un valor de `disabled` para **@propertyvalue** .  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente habilita el trabajo `Xactset` y establece un intervalo de tres minutos entre ejecuciones.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>Vea también  
 [Optimizar el rendimiento de publicadores de Oracle](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
