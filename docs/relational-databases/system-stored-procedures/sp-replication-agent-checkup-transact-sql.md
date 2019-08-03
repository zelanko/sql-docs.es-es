---
title: sp_replication_agent_checkup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b434d4bda50cf03442020ba2f0c029aaa1e09cd9
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771231"
---
# <a name="spreplicationagentcheckup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Comprueba en cada base de datos de distribución los Agentes de replicación que se ejecutan pero no tienen un historial registrado en el intervalo de latido especificado. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @heartbeat_interval = ] 'heartbeat_interval'`Es el número máximo de minutos que un agente puede pasar sin registrar un mensaje de progreso. *heartbeat_interval* es de **tipo int**y su valor predeterminado es 10 minutos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **sp_replication_agent_checkup** genera el error 14151 para cada agente que detecta como sospechoso. También registra un mensaje de historial de errores acerca de los agentes.  
  
## <a name="remarks"></a>Comentarios  
 **sp_replication_agent_checkup** se utiliza en la replicación de instantáneas, la replicación transaccional y la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_replication_agent_checkup**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
