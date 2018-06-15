---
title: sp_delete_log_shipping_primary_database (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 76a1b1ac129d33866984eb7a0f428149e4e299a2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258720"
---
# <a name="spdeletelogshippingprimarydatabase-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este procedimiento almacenado quita el trasvase de registros de la base de datos principal, incluyendo el trabajo de copia de seguridad y los historiales local y remoto. Sólo utilice este procedimiento almacenado después de haber quitado las bases de datos secundarias mediante **sp_delete_log_shipping_primary_secondary**.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database =** ] '*base de datos*'  
 Es el nombre de la base de datos principal de trasvase de registros. *base de datos* es **sysname**, no tiene ningún valor predeterminado, y no puede ser NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 **sp_delete_log_shipping_primary_database** se debe ejecutar desde la **maestro** base de datos en el servidor principal. Este procedimiento almacenado hace lo siguiente:  
  
1.  Elimina el trabajo de copia de seguridad para la base de datos principal especificada.  
  
2.  Quita el registro de monitor local de **log_shipping_monitor_primary** en el servidor principal.  
  
3.  Quita las entradas correspondientes en **log_shipping_monitor_history_detail** y **log_shipping_monitor_error_detail**.  
  
4.  Si el servidor de supervisión es diferente del servidor principal, quita el registro de monitor de **log_shipping_monitor_primary** en el servidor de supervisión.  
  
5.  Quita las entradas correspondientes en **log_shipping_monitor_history_detail** y **log_shipping_monitor_error_detail** en el servidor de supervisión.  
  
6.  Quita la entrada de **log_shipping_primary_databases** para esta base de datos principal.  
  
7.  Llamadas **sp_delete_log_shipping_alert_job** en el servidor de supervisión.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En este ejemplo se muestra cómo utilizar **sp_delete_log_shipping_primary_database** para eliminar la base de datos principal **AdventureWorks2012**.  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Acerca del trasvase de registros & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
