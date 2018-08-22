---
title: sp_post_msx_operation (Transact-SQL) | Microsoft Docs
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
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a1524f9e3f20a774d32c491bc264f2c6c63e7b18
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393555"
---
# <a name="sppostmsxoperation-transact-sql"></a>sp_post_msx_operation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inserta operaciones (filas) en el **sysdownloadlist** tabla del sistema para servidores de destino descargar y ejecutar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_post_msx_operation  
     [ @operation = ] 'operation'  
     [ , [ @object_type = ] 'object' ]   
     { , [ @job_id = ] job_id }   
     [ , [ @specific_target_server = ] 'target_server' ]   
     [ , [ @value = ] value ]  
     [ , [ @schedule_uid = ] schedule_uid ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@operation =**] **'***operación***'**  
 Tipo de la operación expuesta. *operación*es **varchar(64)**, no tiene ningún valor predeterminado. Las operaciones válidas dependen *object_type*.  
  
|Tipo de objeto|Operación|  
|-----------------|---------------|  
|**TRABAJO**|INSERT<br /><br /> UPDATE<br /><br /> Delete<br /><br /> START<br /><br /> STOP|  
|**SERVIDOR**|RE-ENLIST<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**PROGRAMACIÓN**|INSERT<br /><br /> UPDATE<br /><br /> Delete|  
  
 [  **@object_type =**] **'***objeto***'**  
 Tipo de objeto para el que se expone una operación. Los tipos válidos son **trabajo**, **SERVER**, y **programación**. *objeto* es **varchar(64)**, su valor predeterminado es **trabajo**.  
  
 [ **@job_id =**] *job_id*  
 Número de identificación del trabajo al que se aplica la operación. *job_id* es **uniqueidentifier**, no tiene ningún valor predeterminado. **0 x 00** indica todos los trabajos. Si *objeto* es **SERVER**, a continuación, *job_id*no es necesario.  
  
 [  **@specific_target_server =**] **'***target_server***'**  
 Nombre del servidor de destino al que se aplica la operación especificada. Si *job_id* se especifica, pero *target_server* no se especifica, las operaciones se exponen para todos los trabajos del trabajo de los servidores. *target_server* es **nvarchar (30)**, su valor predeterminado es null.  
  
 [  **@value =**] *valor*  
 Intervalo de sondeo, en segundos. *value* es de tipo **int**y su valor predeterminado es NULL. Especifique este parámetro solo si *operación* es **SET-POLL**.  
  
 [  **@schedule_uid=** ] *valor schedule_uid*  
 Identificador único de la programación a la que se aplica la operación. *valor schedule_uid* es **uniqueidentifier**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Notas  
 **sp_post_msx_operation** se debe ejecutar desde la **msdb** base de datos.  
  
 **sp_post_msx_operation** siempre se puede llamar sin ningún riesgo porque primero determina si el servidor actual es un agente de Microsoft SQL Server multiservidor y, si es así, si *objeto*es un trabajo multiservidor.  
  
 Una vez que se ha registrado una operación, aparece en el **sysdownloadlist** tabla. Después de crear y exponer un trabajo, también se deben comunicar los cambios siguientes de ese trabajo a los servidores de destino (TSX). Esto también se realiza mediante la lista de descarga.  
  
 Es muy recomendable administrar la lista de descarga con SQL Server Management Studio. Para obtener más información, consulte [ver o modificar trabajos](../../ssms/agent/view-or-modify-jobs.md).  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, los usuarios debe concederse el **sysadmin** rol fijo de servidor.  
  
## <a name="see-also"></a>Vea también  
 [sp_add_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
