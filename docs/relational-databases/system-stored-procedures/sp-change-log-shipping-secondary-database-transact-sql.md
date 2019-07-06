---
title: sp_change_log_shipping_secondary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_change_log_shipping_secondary_database
- sp_change_log_shipping_secondary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_change_log_shipping_secondary_database
ms.assetid: 3ebcf2f1-980f-4543-a84b-fbaeea54eeac
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5af98bd479738785c341b2618561eaab3f43b5d1
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586019"
---
# <a name="spchangelogshippingsecondarydatabase-transact-sql"></a>sp_change_log_shipping_secondary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia la configuración de la base de datos secundaria.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_change_log_shipping_secondary_database  
[ @secondary_database = ] 'secondary_database',  
[, [ @restore_delay = ] 'restore_delay']  
[, [ @restore_all = ] 'restore_all']  
[, [ @restore_mode = ] 'restore_mode']  
[, [ @disconnect_users = ] 'disconnect_users']  
[, [ @block_size = ] 'block_size']  
[, [ @buffer_count = ] 'buffer_count']  
[, [ @max_transfer_size = ] 'max_transfer_size']  
[, [ @restore_threshold = ] 'restore_threshold']   
[, [ @threshold_alert = ] 'threshold_alert']   
[, [ @threshold_alert_enabled = ] 'threshold_alert_enabled']   
[, [ @history_retention_period = ] 'history_retention_period']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @restore_delay = ] 'restore_delay'` La cantidad de tiempo, en minutos, que el servidor secundario espera antes de restaurar un archivo de copia de seguridad determinado. *restore_delay* es **int** y no puede ser NULL. El valor predeterminado es 0.  
  
`[ @restore_all = ] 'restore_all'` Si se establece en 1, el servidor secundario restaura todas las copias de seguridad de registro de transacciones disponibles cuando se ejecuta el trabajo de restauración. De lo contrario, se detiene tras haber restaurado un archivo. *restore_all* es **bit** y no puede ser NULL.  
  
`[ @restore_mode = ] 'restore_mode'` El modo de restauración de la base de datos secundaria.  
  
 0 = Restaurar registro con NORECOVERY.  
  
 1 = Restaurar registro con STANDBY.  
  
 *restaurar* es **bit** y no puede ser NULL.  
  
`[ @disconnect_users = ] 'disconnect_users'` Si se establece en 1, los usuarios se desconecta de la base de datos secundaria cuando se realiza una operación de restauración. Valor predeterminado = 0. *disconnect_users* es **bit** y no puede ser NULL.  
  
`[ @block_size = ] 'block_size'` El tamaño, en bytes, que se usa como el tamaño de bloque para el dispositivo de copia de seguridad. *block_size* es **int** con un valor predeterminado de -1.  
  
`[ @buffer_count = ] 'buffer_count'` El número total de búferes utilizados por la operación de copia de seguridad o restauración. *buffer_count* es **int** con un valor predeterminado de -1.  
  
`[ @max_transfer_size = ] 'max_transfer_size'` El tamaño, en bytes, de la entrada máxima o la solicitud de salida emitida por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el dispositivo de copia de seguridad. *max_transfersize* es **int** y puede ser NULL.  
  
`[ @restore_threshold = ] 'restore_threshold'` El número de minutos permitido entre las operaciones de restauración antes de que se genera una alerta. *restore_threshold* es **int** y no puede ser NULL.  
  
`[ @threshold_alert = ] 'threshold_alert'` Es la alerta que se genera cuando se supera el umbral de restauración. *threshold_alert* es **int**, su valor predeterminado es 14420.  
  
`[ @threshold_alert_enabled = ] 'threshold_alert_enabled'` Especifica si va a una alerta se genera cuando *restore_threshold*se supera. 1 = habilitadas; 0 = deshabilitadas. *threshold_alert_enabled* es **bit** y no puede ser NULL.  
  
`[ @history_retention_period = ] 'history_retention_period'` Es el período de tiempo en minutos en el que se retendrá el historial. *history_retention_period* es **int**. Si se especifica ninguno, se usará un valor de 1440.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_change_log_shipping_secondary_database** se debe ejecutar desde la **maestro** base de datos en el servidor secundario. Este procedimiento almacenado hace lo siguiente:  
  
1.  Cambia la configuración de la **log_shipping_secondary_database** registra según sea necesario.  
  
2.  Cambia el registro de monitor local en **log_shipping_monitor_secondary** en el servidor secundario utilizando los argumentos proporcionados, si es necesario.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra cómo utilizar **sp_change_log_shipping_secondary_database** para actualizar los parámetros de la base de datos secundaria de la base de datos **LogShipAdventureWorks**.  
  
```  
EXEC master.dbo.sp_change_log_shipping_secondary_database   
 @secondary_database =  'LogShipAdventureWorks'  
,  @restore_delay = 0  
,  @restore_all = 1  
,  @restore_mode = 0  
,  @disconnect_users = 0  
,  @threshold_alert = 14420  
,  @threshold_alert_enabled = 1  
,  @history_retention_period = 14420;  
```  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
