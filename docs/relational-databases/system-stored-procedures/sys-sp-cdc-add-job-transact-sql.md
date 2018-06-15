---
title: Sys.sp_cdc_add_job (Transact-SQL) | Documentos de Microsoft
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
- sp_cdc_add_job_TSQL
- sys.sp_cdc_add_job
- sys.sp_cdc_add_job_TSQL
- sp_cdc_add_job
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cdc_add_job
ms.assetid: c4458738-ed25-40a6-8294-a26ca5a05bd9
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7c42d2150a148f1a288c1fa447f4bb1d9020fe09
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33261964"
---
# <a name="sysspcdcaddjob-transact-sql"></a>sys.sp_cdc_add_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una limpieza de captura datos de cambios o un trabajo de captura en la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_add_job [ @job_type = ] 'job_type'  
    [ , [ @start_job = ] start_job ]   
    [ , [ @maxtrans = ] max_trans ]   
    [ , [ @maxscans = ] max_scans ]   
    [ , [ @continuous = ] continuous ]   
    [ , [ @pollinginterval = ] polling_interval ]   
    [ , [ @retention ] = retention ]   
    [ , [ @threshold ] = 'delete_threshold' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_type=** ] **'***job_type***'**  
 Tipo de trabajo que se agrega. *job_type* es **nvarchar (20)** y no puede ser NULL. Las entradas válidas son **'capture'** y **'cleanup'**.  
  
 [  **@start_job=** ] *start_job*  
 Marca que indica si se debería iniciar el trabajo inmediatamente una vez agregado. *start_job* es **bits** con un valor predeterminado es 1.  
  
 [ **@maxtrans** ] = *max_trans*  
 Número máximo de transacciones para procesar en cada ciclo de recorrido. *max_trans* es **int** con un valor predeterminado de 500. Si se especifica, el valor debe ser un entero positivo.  
  
 *max_trans* es válida únicamente para los trabajos de captura.  
  
 [ **@maxscans** ] **= *** max_scans*  
 Número máximo de ciclos de recorrido que se ejecutarán para extraer todas las filas del registro. *max_scans* es **int** su valor predeterminado es 10.  
  
 *max_scan* es válida únicamente para los trabajos de captura.  
  
 [ **@continuous** ] **= *** continua*  
 Indica si el trabajo de captura se ejecutará continuamente (1), o solo una vez (0). *continuo* es **bits** con un valor predeterminado es 1.  
  
 Cuando *continua* = 1, el [sp_cdc_scan](../../relational-databases/system-stored-procedures/sys-sp-cdc-scan-transact-sql.md) trabajo examina el registro y procesa hasta (*max_trans* \* *max_scans*) transacciones. A continuación, espera el número de segundos especificado en *polling_interval* antes de comenzar el recorrido del registro siguiente.  
  
 Cuando *continua* = 0, el **sp_cdc_scan** hasta se ejecuta el trabajo *max_scans* recorridos del registro, procesando hasta *max_trans* transacciones durante cada recorrido y, a continuación, se cierra.  
  
 *continuo* es válida únicamente para los trabajos de captura.  
  
 [ **@pollinginterval** ] **= *** polling_interval*  
 Número de segundos entre los ciclos de recorrido del registro. *polling_interval* es **bigint** con un valor predeterminado es 5.  
  
 *polling_interval* es válida sólo para la captura de los trabajos al *continua* está establecido en 1. Si se especifica, el valor no puede ser negativo y no puede superar 24 horas. Si se especifica el valor 0, no hay ninguna espera entre los exámenes del registro.  
  
 [ **@retention** ] **= *** retención*  
 Número de minutos que las filas de datos de cambio se retendrán en tablas de cambio. *retención* es **bigint** con un valor predeterminado de 4320 (72 horas). El valor máximo es 52494800 (100 años). Si se especifica, el valor debe ser un entero positivo.  
  
 *retención* es válida únicamente para los trabajos de limpieza.  
  
 [  **@threshold =** ] **'***delete_threshold***'**  
 Número máximo de entradas correspondientes a operaciones de eliminación que se pueden eliminar mediante una única instrucción durante el proceso de limpieza. *delete_threshold* es **bigint** con un valor predeterminado es 5000.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Un trabajo de limpieza se crea utilizando los valores predeterminados cuando la primera tabla de la base de datos se habilita para la captura de datos de cambio. Un trabajo de cambio se crea usando los valores predeterminados cuando la primera tabla de la base de datos se habilita para la captura de datos de cambio y no existe ninguna publicación transaccional para la base de datos. Si existe una publicación transaccional, se usará el lector del registro transaccional para controlar el mecanismo de captura, y no se permitirá ni se necesitará realizar otro trabajo de captura.  
  
 Dado que los trabajos de captura y limpieza se crean de forma predeterminada, este procedimiento almacenado solo es necesario cuando un trabajo se ha eliminado y se ha vuelto a crear explícitamente.  
  
 El nombre del trabajo es **cdc. ***< database_name >***_cleanup** o **cdc. ***< database_name >***_capture**, donde *< database_name >* es el nombre de la base de datos actual. Si ya existe un trabajo con el mismo nombre, el nombre se anexa con un período (**.**) seguido por un identificador único, por ejemplo: **cdc. AdventureWorks_capture. A1ACBDED-13FC-428C-8302-10100EF74F52**.  
  
 Para ver la configuración actual de un trabajo de captura o limpieza, use [sp_cdc_help_jobs](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md). Para cambiar la configuración de un trabajo, use [sp_cdc_change_job](../../relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **db_owner** rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-capture-job"></a>A. Crear un trabajo de captura  
 En este ejemplo se crea un trabajo de captura. Este ejemplo supone que el trabajo de limpieza existente se eliminó y se debe volver a crear explícitamente. El trabajo se crea utilizando los valores predeterminados.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job @job_type = N'capture';  
GO  
```  
  
### <a name="b-creating-a-cleanup-job"></a>B. Crear un trabajo de limpieza  
 En el siguiente ejemplo se crea un trabajo de limpieza en la base de datos de [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. El parámetro `@start_job` está establecido en 0 y `@retention` está establecido en 5760 minutos (96 horas). Este ejemplo supone que el trabajo de limpieza existente se eliminó y se debe volver a crear explícitamente.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_add_job  
     @job_type = N'cleanup'  
    ,@start_job = 0  
    ,@retention = 5760;  
```  
  
## <a name="see-also"></a>Vea también  
 [dbo.cdc_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
