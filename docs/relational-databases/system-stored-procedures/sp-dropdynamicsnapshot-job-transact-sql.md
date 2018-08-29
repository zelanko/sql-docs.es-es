---
title: sp_dropdynamicsnapshot_job (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_dropdynamicsnapshot_job_TSQL
- sp_dropdynamicsnapshot_job
helpviewer_keywords:
- sp_dropdynamicsnapshot_job
ms.assetid: 128e428a-01b3-4062-8c6e-d22d5fa268a9
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 89de049ad17ac51f6b166da59269b41b1101d258
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028735"
---
# <a name="spdropdynamicsnapshotjob-transact-sql"></a>sp_dropdynamicsnapshot_job (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un trabajo de instantáneas de datos filtrados para una publicación con filtros de fila con parámetros. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación. Cuando se elimina el trabajo, todos los datos relacionados se eliminan desde el [MSdynamicsnapshotjobs](../../relational-databases/system-tables/msdynamicsnapshotjobs-transact-sql.md) tabla del sistema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropdynamicsnapshot_job [ @publication = ] 'publication'   
    [ , [ @dynamic_snapshot_jobname = ] 'dynamic_snapshot_jobname' ]   
    [ , [ @dynamic_snapshot_jobid = ] 'dynamic_snapshot_jobid' ]   
    [ , [ @ignore_distributor =] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación de la que se quita el trabajo de instantáneas de datos filtrados. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@dynamic_snapshot_jobname**=] **'***dynamic_snapshot_jobname***'**  
 Es el nombre del trabajo de instantáneas de datos filtrados que se va a quitar. *dynamic_snapshot_jobname*es de tipo sysname y si no está proporcionado los valores predeterminados para cualquier trabajo nombre está asociado con *dynamic_snapshot_jobid*.  
  
 [ **@dynamic_snapshot_jobid**=] **'***dynamic_snapshot_jobid***'**  
 Es un identificador del trabajo de instantáneas de datos filtrados que se va a quitar. *dynamic_snapshot_jobid*es **uniqueidentifier**, no tiene valor predeterminado es null.  
  
> [!IMPORTANT]  
>  Solo *dynamic_snapshot_jobid*o *dynamic_snapshot_jobname* se puede especificar. Si no se proporcionaron valores para cualquier *dynamic_snapshot_jobid*o *dynamic_snapshot_jobname*, se quitan todos los trabajos de instantáneas dinámicas para la publicación.  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 *ignore_distributor* es **bit**, su valor predeterminado es **0**. Este parámetro se puede utilizar para quitar un trabajo de instantáneas dinámicas sin tener que realizar tareas de limpieza en el distribuidor.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_dropdynamicsnapshot** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_dropdynamicsnapshot**.  
  
## <a name="see-also"></a>Vea también  
 [sp_adddynamicsnapshot_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddynamicsnapshot-job-transact-sql.md)  
  
  
