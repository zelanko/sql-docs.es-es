---
title: sp_helpmergepartition (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords:
- sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4c320af039ba5ea94282c853bc34edbbde7901aa
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpmergepartition-transact-sql"></a>sp_helpmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información de partición para la publicación de combinación especificada. Este procedimiento almacenado se ejecuta en el publicador de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@suser_sname=** ] **'***suser_sname***'**  
 Es el valor de SUSER_SNAME utilizado para definir una partición. *SUSER_SNAME* es **sysname**, su valor predeterminado es null. Proporcione este parámetro para limitar el conjunto de resultados tan solo a las particiones en que SUSER_SNAME se resuelve en el valor suministrado.  
  
> [!NOTE]  
>  Cuando *suser_sname* se proporciona, *host_name* debe ser NULL  
  
 [  **@host_name=** ] **'***host_name***'**  
 Es el valor de HOST_NAME utilizado para definir una partición. *HOST_NAME* es **sysname**, su valor predeterminado es null. Proporcione este parámetro para limitar el conjunto de resultados tan solo a las particiones en que HOST_NAME se resuelve en el valor suministrado.  
  
> [!NOTE]  
>  Cuando *suser_sname* se proporciona, *host_name* debe ser NULL  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Partición**|**int**|Identifica la partición del suscriptor.|  
|**HOST_NAME**|**sysname**|Valor utilizado al crear la partición para una suscripción que está filtrada por el valor de la [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) función en el suscriptor.|  
|**SUSER_SNAME**|**sysname**|Valor utilizado al crear la partición para una suscripción que está filtrada por el valor de la [SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md) función en el suscriptor.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Ubicación de la instantánea de datos filtrados para la partición del suscriptor.|  
|**date_refreshed**|**datetime**|Última fecha en que el trabajo de instantáneas se ha ejecutado para generar la instantánea de datos filtrados para la partición.|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|Identifica el trabajo que crea la instantánea de datos filtrados para una partición.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpmergepartition** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor y el **db_owner** rol fijo de base de datos puede ejecutar **sp_helpmergepartition**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_dropmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
