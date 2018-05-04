---
title: sp_add_log_shipping_alert_job (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_log_shipping_alert_job_TSQL
- sp_add_log_shipping_alert_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_shipping_alert_job
ms.assetid: dd95d96e-8963-4aa9-bdcc-3e4b1bc002d3
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 83d4e78c383fbbecc498812fa97946eec910c399
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spaddlogshippingalertjob-transact-sql"></a>sp_add_log_shipping_alert_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este procedimiento almacenado comprueba si se ha creado un trabajo de alerta en este servidor. Si un trabajo de alerta no existe, este procedimiento almacenado crea el trabajo de alerta y agrega su Id. de trabajo para el **log_shipping_monitor_alert** tabla. El trabajo de alerta está habilitado de forma predeterminada y se ejecuta según un programa de una vez cada dos minutos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_add_log_shipping_alert_job  
[, [ @alert_job_id = ] alert_job_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@alert_job_id =** ] *alert_job_id* salida  
 El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Id. de trabajo del agente de trabajo de alerta de trasvase de registros.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_add_log_shipping_alert_job** se debe ejecutar desde la **maestro** base de datos en el servidor de supervisión.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra la ejecución de **sp_add_log_shipping_alert_job** para crear un identificador de trabajo de alerta.  
  
```  
USE master  
GO  
EXEC sp_add_log_shipping_alert_job;  
```  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
