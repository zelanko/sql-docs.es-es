---
title: Sys.sp_mscdc_capture_job (Transact-SQL) | Documentos de Microsoft
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
- sys.sp_cdc_scan_TSQL
- sp_cdc_scan
- sys.sp_cdc_scan
- sp_cdc_scan_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_cdc_scan
ms.assetid: 46e4294c-97b8-47d6-9ed9-b436a9929353
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cbde9d47ae848ed52a9feeb81329f68456330c79
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysspcdcscan-transact-sql"></a>sys.sp_cdc_scan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ejecuta la operación de recorrido del registro de captura de datos modificados.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_scan [ [ @maxtrans = ] max_trans ]   
     [ , [ @maxscans = ] max_scans ]   
     [ , [ @continuous = ] continuous ]   
     [ , [ @pollinginterval = ] polling_interval ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@maxtrans=** ] *max_trans*  
 Número máximo de transacciones para procesar en cada ciclo de recorrido. *max_trans* es **int** con un valor predeterminado de 500.  
  
 [  **@maxscans=** ] *max_scans*  
 Número máximo de ciclos de recorrido que se ejecutarán para extraer todas las filas del registro. *max_scans* es **int** su valor predeterminado es 10.  
  
 [  **@continuous=** ] *continua*  
 Indica si el procedimiento almacenado debe finalizar después de ejecutar un ciclo de examen (0) o se ejecuta continuamente, deteniéndose el tiempo especificado por *polling_interval* antes de volver a ejecutar el ciclo de examen (1). *continuo* es **tinyint** con un valor predeterminado es 0.  
  
 [  **@pollinginterval=** ] *polling_interval*  
 Número de segundos entre los ciclos de recorrido del registro. *polling_interval* es **bigint** con un valor predeterminado es 0.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 sys.sp_MScdc_capture_job llama internamente a sys.sp_cdc_scan si la captura de datos modificados utiliza el trabajo de captura del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El procedimiento no se puede ejecutar explícitamente cuando una operación de examen del registro de captura de datos modificados ya está activa, o cuando la base de datos está habilitada para la replicación transaccional. Este procedimiento almacenado debe usarse por los administradores que deseen personalizar el comportamiento del trabajo de captura que se configura automáticamente.  
  
## <a name="permissions"></a>Permissions  
 Requiere pertenencia al rol fijo de base de datos db_owner.  
  
## <a name="see-also"></a>Vea también  
 [dbo.cdc_jobs &#40; Transact-SQL &#41;](../../relational-databases/system-tables/dbo-cdc-jobs-transact-sql.md)  
  
  
