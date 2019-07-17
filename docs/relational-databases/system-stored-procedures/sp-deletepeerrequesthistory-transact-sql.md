---
title: sp_deletepeerrequesthistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletepeerrequesthistory
- sp_deletepeerrequesthistory_TSQL
helpviewer_keywords:
- sp_deletepeerrequesthistory
ms.assetid: 63a4ec6e-ce79-4bf1-9d37-5ac88f8d6beb
author: stevestein
ms.author: sstein
ms.openlocfilehash: e1af3aad1f66f3de7dd2fce44990718980018d3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111942"
---
# <a name="spdeletepeerrequesthistory-transact-sql"></a>sp_deletepeerrequesthistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina el historial de una solicitud de estado de publicación, que incluye el historial de solicitudes ([MSpeer_request &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-request-transact-sql.md)), así como el historial de respuestas ([MSpeer_response &#40; Transact-SQL&#41;](../../relational-databases/system-tables/mspeer-response-transact-sql.md)). Este procedimiento almacenado se ejecuta en la base de datos de publicación en un publicador que participa en una topología de replicación punto a punto. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_deletepeerrequesthistory [ @publication = ] 'publication'  
    [ , [ @request_id = ] request_id ]  
    [ , [ @cutoff_date = ] cutoff_date ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Nombre de la publicación para el que se realizó la solicitud de estado. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @request_id = ] request_id` Especifica una solicitud de estado individual para que se eliminarán todas las respuestas a esta solicitud. *request_id* es **int**, su valor predeterminado es null.  
  
`[ @cutoff_date = ] cutoff_date` Especifica una fecha límite, antes de que se eliminan todos los registros de repuestas. *cutoff_date* es **datetime**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_deletepeerrequesthistory** se utiliza en una topología de replicación transaccional punto a punto. Para obtener más información, consulte [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 Al ejecutar **sp_deletepeerrequesthistory**, ya sea *request_id* o *cutoff_date* debe especificarse.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_deletepeerrequesthistory**.  
  
## <a name="see-also"></a>Vea también  
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)   
 [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md)  
  
  
