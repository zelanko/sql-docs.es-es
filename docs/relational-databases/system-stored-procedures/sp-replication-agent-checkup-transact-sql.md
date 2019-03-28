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
manager: craigg
ms.openlocfilehash: 73335322d9e4c8602e299255ebcd3b3b183aaaec
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58529877"
---
# <a name="spreplicationagentcheckup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Comprueba en cada base de datos de distribución los Agentes de replicación que se ejecutan pero no tienen un historial registrado en el intervalo de latido especificado. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @heartbeat_interval = ] 'heartbeat_interval'` Es el número máximo de minutos que un agente puede ejecutarse sin registrar un mensaje de progreso. *heartbeat_interval* es **int**, su valor predeterminado es de 10 minutos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **sp_replication_agent_checkup** genera el error 14151 para cada agente que detecta como sospechoso. También registra un mensaje de historial de errores acerca de los agentes.  
  
## <a name="remarks"></a>Comentarios  
 **sp_replication_agent_checkup** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_replication_agent_checkup**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
