---
title: Sys.sp_cdc_help_jobs (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cdc_help_jobs
- sys.sp_cdc_help_jobs_TSQL
- sp_cdc_help_jobs_TSQL
- sys.sp_cdc_help_jobs
dev_langs: TSQL
helpviewer_keywords: sp_cdc_help_jobs
ms.assetid: 9399b4bc-8293-408f-b3cb-f904e0657fb5
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4382b14729daf79809e8501f191657b11d4f311e
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sysspcdchelpjobs-transact-sql"></a>sys.sp_cdc_help_jobs (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea informe que incluyen información sobre todos los trabajos de captura o de limpieza de captura de datos de cambio en la base de datos actual.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_help_jobs  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|Id. del trabajo.|  
|**job_type**|**nvarchar (20)**|Tipo de trabajo.|  
|**maxtrans**|**int**|El número máximo de transacciones que se va a procesar en cada ciclo de examen.<br /><br /> **maxtrans** es válida únicamente para los trabajos de captura.|  
|**maxscans**|**int**|El número máximo de ciclos de recorrido para ejecutar en orden y extraer todas las filas del registro.<br /><br /> **maxscans** es válida únicamente para los trabajos de captura.|  
|**continuo**|**bit**|Una marca que indica si el trabajo de captura debe ejecutarse continuamente (1) o solo una vez (0). Para obtener más información, consulte [sys.sp_cdc_add_job &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md).<br /><br /> **continuo** es válida únicamente para los trabajos de captura.|  
|**pollingInterval**|**bigint**|El número de segundos entre los ciclos del recorrido del registro.<br /><br /> **pollingInterval** es válida únicamente para los trabajos de captura.|  
|**retención**|**bigint**|El número de minutos que se conservan las filas de cambios en las tablas de cambios.<br /><br /> **retención** es válida únicamente para los trabajos de limpieza.|  
|**umbral**|**bigint**|El número máximo de entradas correspondientes a operaciones de eliminación que se pueden eliminar mediante una única instrucción durante el proceso de limpieza.|  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **db_owner** rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 Este ejemplo devuelve información acerca de los trabajos de captura y limpieza definidos para la base de datos `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_help_jobs;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [dbo.cdc_jobs &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)   
 [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md)  
  
  
