---
title: sp_refresh_log_shipping_monitor (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_refresh_log_shipping_monitor
- sp_refresh_log_shipping_monitor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_refresh_log_shipping_monitor
ms.assetid: edefb912-31c5-4d99-9aba-06629afd0171
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f2f0bf6df228f7a0948b0c5d295ae6d2cdf4a9b9
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
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
 [  **@agent_id=** ] **'***agent_id***'**  
 Id. principal de la copia de seguridad o Id. secundario de la copia o restauración. *agent_id* es **uniqueidentifier** y no puede ser NULL.  
  
 [  **@agent_type=** ] **'***agent_type***'**  
 Es el tipo de trabajo de trasvase de registros.  
  
 0 = Copia de seguridad.  
  
 1 = Copia.  
  
 2 = Restauración.  
  
 *agent_type* es **tinyint** y no puede ser NULL.  
  
 [  **@database=** ] **'***base de datos***'**  
 Es la base de datos primaria o secundaria que se utiliza en los registros, que utilizan los agentes de copia de seguridad o restauración.  
  
 [ **@mode** ] *n*  
 Especifica si se van a actualizar los datos del monitor o se van a eliminar. Tipo de datos de *m* es tinyint y los valores admitidos son:  
  
 1 = actualizar (valor predeterminado)  
  
 2 = eliminar  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 **sp_refresh_log_shipping_monitor** actualiza el **log_shipping_monitor_primary**, **log_shipping_monitor_secondary**, **log_shipping_monitor_history_detail** , y **log_shipping_monitor_error_detail** tablas con información de sesión que ya no se han transferido. De esta manera, puede sincronizar el servidor de supervisión con el servidor primario o secundario si el monitor lleva un tiempo sin estar sincronizado. Además, puede eliminar la información del monitor en el servidor de supervisión, si así lo precisa.  
  
 **sp_refresh_log_shipping_monitor** se debe ejecutar desde la **maestro** base de datos en el servidor principal o secundario.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
