---
title: sys.sp_cdc_change_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_change_job_TSQL
- sys.sp_cdc_change_job
- sp_cdc_change_job_TSQL
- sp_cdc_change_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_change_job
ms.assetid: ea918888-0fc5-4cc1-b301-26b2a9fbb20d
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c2c39363ca1b0824b27645df8c8501931b674a2
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056765"
---
# <a name="syssp_cdc_change_job-transact-sql"></a>sys.sp_cdc_change_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica la configuración de un trabajo de captura o de limpieza de captura de datos de cambio en la base de datos actual. Para ver la configuración actual de un trabajo, consulte la tabla [dbo. cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) o utilice [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_change_job [ [ @job_type = ] 'job_type' ]  
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ @threshold = ] 'delete threshold'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @job_type = ] 'job_type'` tipo de trabajo que se va a modificar. *job_type* es de tipo **nvarchar (20)** y su valor predeterminado es ' Capture '. Las entradas válidas son 'capture' y 'cleanup'.  
  
`[ @maxtrans ] = max_trans_` número máximo de transacciones para procesar en cada ciclo de examen. *max_trans* es de **tipo int** y su valor predeterminado es null, lo que indica que no hay ningún cambio para este parámetro. Si se especifica, el valor debe ser un entero positivo.  
  
 *max_trans* solo es válido para los trabajos de captura.  
  
`[ @maxscans ] = max_scans_` número máximo de ciclos de recorrido que se ejecutarán para extraer todas las filas del registro. *max_scans* es de **tipo int** y su valor predeterminado es null, lo que indica que no hay ningún cambio para este parámetro.  
  
 *max_scan* solo es válido para los trabajos de captura.  
  
`[ @continuous ] = continuous_` indica si el trabajo de captura debe ejecutarse continuamente (1) o solo una vez (0). *Continuous* es de **bit** con un valor predeterminado de NULL, que indica que no hay ningún cambio para este parámetro.  
  
 Cuando *Continuous* = 1, el trabajo de [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) examina el registro y procesa hasta (*max_trans* \* *max_scans*) transacciones. Después, espera el número de segundos especificado en *polling_interval* antes de comenzar el siguiente examen del registro.  
  
 Cuando es *Continuous* = 0, el trabajo de **sp_cdc_scan** se ejecuta hasta *max_scans* exámenes del registro, procesando hasta *max_trans* transacciones durante cada análisis y, a continuación, se cierra.  
  
 Si **\@Continuous** se cambia de 1 a 0, **\@PollingInterval** se establece automáticamente en 0. Se omite un valor especificado para **\@PollingInterval** distinto de 0.  
  
 Si se omite **\@Continuous** o se establece explícitamente en NULL y **\@PollingInterval** se establece explícitamente en un valor mayor que 0, **\@Continuous** se establece automáticamente en 1.  
  
 *Continuous* solo es válido para los trabajos de captura.  
  
`[ @pollinginterval ] = polling_interval_` número de segundos entre los ciclos de recorrido del registro. *polling_interval* es de tipo **BIGINT** y su valor predeterminado es null, lo que indica que no hay ningún cambio para este parámetro.  
  
 *polling_interval* solo es válido para los trabajos de captura cuando *Continuous* está establecido en 1.  
  
`[ @retention ] = retention_` número de minutos que las filas de cambio se conservarán en las tablas de cambios. la *retención* es **BIGINT** con un valor predeterminado de NULL, que indica que no hay ningún cambio para este parámetro. El valor máximo es 52494800 (100 años). Si se especifica, el valor debe ser un entero positivo.  
  
 la *retención* solo es válida para los trabajos de limpieza.  
  
`[ @threshold = ] 'delete threshold'` número máximo de entradas de eliminación que se pueden eliminar mediante una única instrucción en la limpieza. el *umbral de eliminación* es **BIGINT** y su valor predeterminado es null, lo que indica que no hay ningún cambio para este parámetro. el *umbral de eliminación* solo es válido para los trabajos de limpieza.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Remarks  
 Si se omite un parámetro, no se actualiza el valor asociado en la tabla [dbo. cdc_jobs](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md) . Un parámetro establecido explícitamente en NULL se trata como si se omitiese el parámetro.  
  
 Si se especifica un parámetro que no es válido para el tipo de trabajo, la instrucción generará un error.  
  
 Los cambios en un trabajo no surtirán efecto hasta que el trabajo se detenga mediante [sp_cdc_stop_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-stop-job-transact-sql.md) y se reinicie con [sp_cdc_start_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-start-job-transact-sql.md).  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de base de datos **db_owner** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-a-capture-job"></a>A. Cambiar un trabajo de captura  
 En el ejemplo siguiente se actualizan los parámetros `@job_type`, `@maxscans` y `@maxtrans` de un trabajo de captura en la base de datos `AdventureWorks2012`. El resto de parámetros válidos para un trabajo captura, `@continuous` y `@pollinginterval`, se omiten; sus valores no se modifican.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'capture',  
    @maxscans = 1000,  
    @maxtrans = 15;  
GO  
```  
  
### <a name="b-changing-a-cleanup-job"></a>b. Cambiar un trabajo de limpieza  
 En el siguiente ejemplo se actualiza un trabajo de limpieza en la base de datos `AdventureWorks2012`. Se especifican todos los parámetros válidos para este tipo de trabajo, excepto **\@umbral**. El valor de **\@umbral** no se modifica.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_change_job   
    @job_type = N'cleanup',  
    @retention = 2880;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [dbo.cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
