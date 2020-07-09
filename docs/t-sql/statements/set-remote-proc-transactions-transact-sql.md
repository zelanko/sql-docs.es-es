---
title: SET REMOTE_PROC_TRANSACTIONS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- REMOTE_PROC_TRANSACTIONS_TSQL
- SET REMOTE_PROC_TRANSACTIONS
- REMOTE_PROC_TRANSACTIONS
- SET_REMOTE_PROC_TRANSACTIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- SET REMOTE_PROC_TRANSACTIONS statement
- distributed transactions [SQL Server], starting
- REMOTE_PROC_TRANSACTIONS option
- active transactions
ms.assetid: 4d284ae9-3f5f-465a-b0dd-1328a4832a03
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b327105398388615aa507ceaf30734347fbf2683
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882587"
---
# <a name="set-remote_proc_transactions-transact-sql"></a>SET REMOTE_PROC_TRANSACTIONS (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Especifica que, cuando haya una transacción local activa, la ejecución de un procedimiento almacenado remoto iniciará una transacción distribuida de [!INCLUDE[tsql](../../includes/tsql-md.md)] administrada por el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Esta opción se proporciona por compatibilidad con versiones anteriores de aplicaciones que utilizan procedimientos almacenados remotos. En lugar de emitir llamadas de procedimiento almacenado remotas, utilice consultas distribuidas que hagan referencia a los servidores vinculados. Los servidores vinculados se definen mediante [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
  
SET REMOTE_PROC_TRANSACTIONS { ON | OFF }   
```  
  
## <a name="arguments"></a>Argumentos  
 ON | OFF  
 Cuando es ON, al ejecutarse un procedimiento almacenado remoto desde una transacción local, se inicia una transacción distribuida de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cuando es OFF, al llamar a procedimientos almacenados remotos desde una transacción local, no se inicia una transacción distribuida de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="remarks"></a>Observaciones  
 Cuando REMOTE_PROC_TRANSACTIONS es ON, al llamar a un procedimiento almacenado remoto se inicia una transacción distribuida y se da de alta en MS DTC. La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que efectúa la llamada al procedimiento almacenado remoto es el originador de la transacción y controla su realización. Posteriormente, cuando se ejecuta para la conexión una instrucción COMMIT TRANSACTION o ROLLBACK TRANSACTION, la instancia que controla la transacción solicita a MS DTC que administre la realización de la transacción distribuida entre los servidores participantes.  
  
 Una vez iniciada una transacción distribuida de [!INCLUDE[tsql](../../includes/tsql-md.md)], se pueden realizar llamadas a procedimientos almacenados remotos en otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se hayan definido como servidores remotos. Todos los servidores remotos se dan de alta en la transacción distribuida de [!INCLUDE[tsql](../../includes/tsql-md.md)] y MS DTC se asegura de que la transacción se complete en cada uno de ellos.  
  
 REMOTE_PROC_TRANSACTIONS es una opción de nivel de conexión que se puede usar para reemplazar la opción **sp_configure remote proc trans** de nivel de instancia.  
  
 Cuando REMOTE_PROC_TRANSACTIONS es OFF, las llamadas a procedimientos almacenados remotos no son parte de una transacción local. Las modificaciones realizadas por el procedimiento almacenado remoto se confirman o deshacen en el momento en que el procedimiento almacenado se completa. Si la conexión que llamó al procedimiento almacenado remoto ejecuta después instrucciones COMMIT TRANSACTION o ROLLBACK TRANSACTION, éstas no tendrán efecto en el procesamiento realizado por el procedimiento.  
  
 REMOTE_PROC_TRANSACTIONS es una opción de compatibilidad que afecta solo a las llamadas a procedimientos almacenados remotos que se realizan en instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definidas como servidores remotos mediante **sp_addserver**. Esta opción no se aplica a las consultas distribuidas que ejecutan un procedimiento almacenado en una instancia definida como servidor vinculado mediante **sp_addlinkedserver**.  
  
 La opción SET REMOTE_PROC_TRANSACTIONS se establece en tiempo de ejecución, no en tiempo de análisis.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Consulte también  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
