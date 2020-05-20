---
title: sp_dropdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0c9f33c4f50f77ed8ded47b6d7f69a2476f49227
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830172"
---
# <a name="sp_dropdynamicsnapshot_job-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un trabajo de instantáneas de datos filtrados para una publicación con filtros de fila con parámetros. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. Cuando se elimina el trabajo, todos los datos relacionados se eliminan de la tabla del sistema [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación de la que se quita el trabajo de instantáneas de datos filtrados. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname'`Es el nombre del trabajo de instantánea de datos filtrados que se va a quitar. *dynamic_snapshot_jobname*es de tipo sysname y, si no se proporciona, el valor predeterminado es cualquier nombre de trabajo asociado a *dynamic_snapshot_jobid*.  
  
`[ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid'`Es un identificador para el trabajo de instantáneas de datos filtrados que se va a quitar. *dynamic_snapshot_jobid*es de tipo **uniqueidentifier**y su valor predeterminado es NULL.  
  
> [!IMPORTANT]  
>  Solo se pueden especificar *dynamic_snapshot_jobid*o *dynamic_snapshot_jobname* . Si no se proporcionan valores para *dynamic_snapshot_jobid*o *dynamic_snapshot_jobname*, se quitan todos los trabajos de instantáneas dinámicas de la publicación.  
  
`[ @ignore_distributor = ] ignore_distributor`*ignore_distributor* es de **bit**y su valor predeterminado es **0**. Este parámetro se puede utilizar para quitar un trabajo de instantáneas dinámicas sin tener que realizar tareas de limpieza en el distribuidor.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_dropdynamicsnapshot** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_dropdynamicsnapshot**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_adddynamicsnapshot_job &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
