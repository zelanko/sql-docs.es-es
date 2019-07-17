---
title: sp_replshowcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replshowcmds
- sp_replshowcmds_TSQL
helpviewer_keywords:
- sp_replshowcmds
ms.assetid: 199f5a74-e08e-4d02-a33c-b8ab0db20f44
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7769c4e648cf3ed3898409cbdc3f0787dcb6d837
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113122"
---
# <a name="spreplshowcmds-transact-sql"></a>sp_replshowcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve los comandos de las transacciones marcadas para replicación en un formato legible. **sp_replshowcmds** solo cuando las conexiones de cliente (incluida la conexión actual) no leen transacciones replicadas del registro se puede ejecutar. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replshowcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @maxtrans = ] maxtrans` Es el número de transacciones que se va a devolver información. *maxtrans* es **int**, su valor predeterminado es **1**, que especifica el número máximo de transacciones pendientes de replicación para el que **sp_replshowcmds** Devuelve información.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_replshowcmds** es un procedimiento de diagnóstico que devuelve información acerca de la base de datos de publicación desde la que se ejecuta.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**xact_seqno**|**binary(10)**|Número de secuencia del comando.|  
|**originator_id**|**int**|Id. de originador del comando, siempre **0**.|  
|**publisher_database_id**|**int**|Id. de la base de datos de publicador, siempre **0**.|  
|**article_id**|**int**|ID. del artículo.|  
|**type**|**int**|Tipo de comando.|  
|**command**|**nvarchar(1024)**|Comando [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="remarks"></a>Comentarios  
 **sp_replshowcmds** se utiliza en la replicación transaccional.  
  
 Uso de **sp_replshowcmds**, puede ver las transacciones que están actualmente no distribuyan (aquellas transacciones restantes en el registro de transacciones que no se han enviado al distribuidor).  
  
 Los clientes que ejecutan **sp_replshowcmds** y **sp_replcmds** dentro de la misma base de datos reciben el error 18752.  
  
 Para evitar este error, debe desconectar el primer cliente o el rol de cliente como el registro del log debe liberarse mediante la ejecución de **sp_replflush**. Una vez que han desconectado todos los clientes de registro del log, **sp_replshowcmds** se puede ejecutar correctamente.  
  
> [!NOTE]  
>  **sp_replshowcmds** se debe ejecutar solo para solucionar problemas de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_replshowcmds**.  
  
## <a name="see-also"></a>Vea también  
 [Mensajes de error](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
