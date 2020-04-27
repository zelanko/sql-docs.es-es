---
title: Configurar el trabajo del conjunto de transacciones para un publicador de Oracle (programación de la replicación con Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 48282f08df588f54b6f03a0b99c58a2f0cf039ac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67793544"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Configurar el trabajo del conjunto de transacciones para un publicador de Oracle (programación de la replicación con Transact-SQL)
  El trabajo **Xactset** es un trabajo de base de datos de Oracle creado por replicación que se ejecuta en un publicador de Oracle para crear conjuntos de transacciones cuando el agente de registro del LOG no está conectado al publicador. Puede habilitar y configurar este trabajo desde el distribuidor mediante programación con procedimientos almacenados de replicación. Para obtener más información, consulte [Optimizar el rendimiento de publicadores de Oracle](../non-sql/performance-tuning-for-oracle-publishers.md).  
  
### <a name="to-enable-the-transaction-set-job"></a>Para habilitar el trabajo del conjunto de transacciones  
  
1.  En el publicador de Oracle, establezca el parámetro de inicialización **job_queue_processes** en un valor suficiente para permitir la ejecución del trabajo Xactset. Para obtener más información acerca de este parámetro, vea la documentación de la base de datos del publicador de Oracle.  
  
2.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre `enabled` del publicador de Oracle para `xactsetbatching` ** \@el publicador**, un valor de para ** \@PropertyName**y un valor de para ** \@PropertyValue**.  
  
3.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador `xactsetjobinterval` de Oracle para ** \@el publicador**, un valor de para ** \@PropertyName**y el intervalo del trabajo, en minutos, para ** \@PropertyValue**.  
  
4.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre `enabled` del publicador de Oracle para `xactsetjob` ** \@el publicador**, un valor de para ** \@PropertyName**y un valor de para ** \@PropertyValue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>Para configurar el trabajo del conjunto de transacciones  
  
1.  (Opcional) En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador de Oracle para ** \@el publicador**. De esta forma se devuelven las propiedades del trabajo **Xactset** al publicador.  
  
2.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre del publicador de Oracle para ** \@el publicador**, el nombre de la propiedad del trabajo Xactset que se establece para ** \@PropertyName**y la nueva configuración para ** \@PropertyValue**.  
  
3.  (Opcional) Repita el paso 2 para cada propiedad del trabajo Xactset que se establece. Al cambiar la `xactsetjobinterval` propiedad, debe reiniciar el trabajo en el publicador de Oracle para que el nuevo intervalo surta efecto.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>Para ver las propiedades del trabajo del conjunto de transacciones  
  
1.  En el distribuidor, ejecute [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql). Especifique el nombre del publicador de Oracle para ** \@el publicador**.  
  
### <a name="to-disable-the-transaction-set-job"></a>Para deshabilitar el trabajo del conjunto de transacciones  
  
1.  En el distribuidor, ejecute [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Especifique el nombre `disabled` del publicador de Oracle para `xactsetjob` ** \@el publicador**, un valor de para ** \@PropertyName**y un valor de para ** \@PropertyValue**.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente habilita el trabajo `Xactset` y establece un intervalo de tres minutos entre ejecuciones.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>Consulte también  
 [Optimización del rendimiento para publicadores de Oracle](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
