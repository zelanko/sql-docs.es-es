---
title: sp_getqueuedrows (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getqueuedrows_TSQL
- sp_getqueuedrows
helpviewer_keywords:
- sp_getqueuedrows
ms.assetid: 139e834f-1988-4b4d-ac81-db1f89ea90e8
author: stevestein
ms.author: sstein
ms.openlocfilehash: ad7521eed3cd25d067e3ea253ff2a4362350c889
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68123939"
---
# <a name="spgetqueuedrows-transact-sql"></a>sp_getqueuedrows (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera filas en el suscriptor que tienen actualizaciones pendientes en la cola. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tablename = ] 'tablename'` Es el nombre de la tabla. *TableName* es **sysname**, no tiene ningún valor predeterminado. La tabla debe formar parte de una suscripción en cola.  
  
`[ @owner = ] 'owner'` Es el propietario de la suscripción. *propietario* es **sysname**, su valor predeterminado es null.  
  
`[ @tranid = ] 'transaction_id'` Permite la salida ser filtradas por el identificador de transacción. *transaction_id* es **nvarchar (70)** , su valor predeterminado es null. Si se especifica, se muestra el Id. de la transacción asociado con el comando en cola. Si es NULL, se muestran todos los comandos de la cola.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Muestra todas las filas que tienen actualmente al menos una transacción en cola para la tabla suscrita.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Acción**|**nvarchar(10)**|Tipo de acción que se llevará a cabo cuando tenga lugar la sincronización.<br /><br /> INS= insertar<br /><br /> DEL = eliminar<br /><br /> UPD = actualizar|  
|**transacción**|**nvarchar(70)**|Id. de transacción con el que se ejecutó el comando.|  
|**tabla column1... n**||El valor para cada columna de la tabla especificada en *tablename*.|  
|**msrepl_tran_version**|**uniqueidentifier**|Esta columna se utiliza para realizar un seguimiento de los cambios de datos replicados y para llevar a cabo la detección de conflictos en el publicador. Esta columna se agrega a la tabla automáticamente.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_getqueuedrows** se utiliza en los suscriptores que participan en la actualización en cola.  
  
 **sp_getqueuedrows** busca filas de una tabla determinada en una suscripción de la base de datos que han participado en una actualización en cola, pero actualmente no se han resuelto por el agente de lector de cola.  
  
## <a name="permissions"></a>Permisos  
 **sp_getqueuedrows** requiere permisos SELECT en la tabla especificada en *tablename*.  
  
## <a name="see-also"></a>Vea también  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Detección y resolución de conflictos de actualización en cola](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
