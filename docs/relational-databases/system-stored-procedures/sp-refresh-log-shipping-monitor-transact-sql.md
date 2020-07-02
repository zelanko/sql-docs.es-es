---
title: sp_refresh_log_shipping_monitor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1db9dfdcb7941db0c253bf0b1c3f65b767a5cdec
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719255"
---
# <a name="sp_refresh_log_shipping_monitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Este procedimiento almacenado actualiza las tablas de supervisión remotas con la información más reciente de un servidor primario o secundario determinado para el agente de trasvase de registros especificado. El procedimiento se invoca en el servidor primario o secundario.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_refresh_log_shipping_monitor  
[ @agent_id = ] 'agent_id',  
[ @agent_type = ] 'agent_type'  
[ @database = ] 'database'  
[ @mode ] n  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @agent_id = ] 'agent_id'`El identificador principal de la copia de seguridad o el ID. secundario de la copia o restauración. *agent_id* es de tipo **uniqueidentifier** y no puede ser null.  
  
`[ @agent_type = ] 'agent_type'`El tipo de trabajo de trasvase de registros.  
  
 0 = Copia de seguridad.  
  
 1 = Copia.  
  
 2 = Restauración.  
  
 *agent_type* es **tinyint** y no puede ser null.  
  
`[ @database = ] 'database'`La base de datos principal o secundaria utilizada por el registro de agentes de copia de seguridad o restauración.  
  
`[ @mode ] n`Especifica si se deben actualizar los datos del monitor o limpiarlos. El tipo de datos de *m* es tinyint y los valores admitidos son:  
  
 1 = actualizar (valor predeterminado)  
  
 2 = eliminar  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 **sp_refresh_log_shipping_monitor** actualiza las tablas **log_shipping_monitor_primary**, **log_shipping_monitor_secondary**, **log_shipping_monitor_history_detail**y **log_shipping_monitor_error_detail** con cualquier información de sesión que todavía no se haya transferido. De esta manera, puede sincronizar el servidor de supervisión con el servidor primario o secundario si el monitor lleva un tiempo sin estar sincronizado. Además, puede eliminar la información del monitor en el servidor de supervisión, si así lo precisa.  
  
 **sp_refresh_log_shipping_monitor** se debe ejecutar desde la base de datos **maestra** en el servidor principal o secundario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
