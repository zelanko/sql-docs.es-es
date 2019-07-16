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
author: stevestein
ms.author: sstein
ms.openlocfilehash: c19f9b99173ca04e6ce15862e22a25f8a2bf06e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002499"
---
# <a name="sprefreshlogshippingmonitor-transact-sql"></a>sp_refresh_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
`[ @agent_id = ] 'agent_id'` El Id. principal para copia de seguridad o el Id. secundario para la copia o restauración. *valor de agent_id* es **uniqueidentifier** y no puede ser NULL.  
  
`[ @agent_type = ] 'agent_type'` El tipo de trabajos de trasvase de registros.  
  
 0 = Copia de seguridad.  
  
 1 = Copia.  
  
 2 = Restauración.  
  
 *agent_type* es **tinyint** y no puede ser NULL.  
  
`[ @database = ] 'database'` La principal o secundaria base de datos utilizado por el registro de agentes de copia de seguridad o restauración.  
  
`[ @mode ] n` Especifica si se debe actualizar los datos del monitor o limpiarlo. Tipo de datos de *m* es tinyint y los valores admitidos son:  
  
 1 = actualizar (valor predeterminado)  
  
 2 = delete  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 **sp_refresh_log_shipping_monitor** actualiza el **log_shipping_monitor_primary**, **log_shipping_monitor_secondary**, **log_shipping_monitor_history_detail** , y **log_shipping_monitor_error_detail** tablas con la información de sesión que no se ha transferido. De esta manera, puede sincronizar el servidor de supervisión con el servidor primario o secundario si el monitor lleva un tiempo sin estar sincronizado. Además, puede eliminar la información del monitor en el servidor de supervisión, si así lo precisa.  
  
 **sp_refresh_log_shipping_monitor** se debe ejecutar desde la **maestro** base de datos en el servidor principal o secundario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
