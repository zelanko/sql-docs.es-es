---
title: sysmail_help_queue_sp (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e83aba8601f4329a496229eca329035a95b283c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailhelpqueuesp-transact-sql"></a>sysmail_help_queue_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El Correo electrónico de base de datos tiene dos colas: la de correo y la de estado. En la cola de correo se almacenan los elementos de correo que están a la espera de ser enviados. En la de estado se almacena el estado de los elementos ya enviados. Este procedimiento almacenado permite ver el estado de las colas de correo o estado. Si el parámetro  **@queue_type**  no se especifica, el procedimiento almacenado devuelve una fila para cada una de las colas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@queue_type** = ] **'***queue_type***'**  
 Argumento opcional elimina los mensajes de correo electrónico del tipo especificado como el *queue_type*. *queue_type* es **nvarchar(6)** no tiene ningún valor predeterminado. Las entradas válidas son **correo** y **estado**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-set"></a>Conjunto de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar(6)**|Tipo de cola. Los valores posibles son **correo** y **estado**.|  
|**length**|**int**|Número de elementos de correo de la cola especificada.|  
|**state**|**nvarchar(64)**|Estado del monitor. Los valores posibles son **inactivo** (cola está inactiva), **NOTIFIED** (cola ha sido una notificación de confirmación de que se produzca), y **RECEIVES_OCCURRING** (cola está recibiendo).|  
|**last_empty_rowset_time**|**FECHA Y HORA**|Fecha y hora en que la cola estuvo vacía por última vez. En formato de hora militar y zona horaria GMT.|  
|**last_activated_time**|**FECHA Y HORA**|Fecha y hora en que la cola se activó por última vez. En formato de hora militar y zona horaria GMT.|  
  
## <a name="remarks"></a>Comentarios  
 Al solucionar problemas de correo electrónico de base de datos, utilice **sysmail_help_queue_sp** para ver cuántos elementos se encuentran en la cola, el estado de la cola, y cuando por última activado.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, solo los miembros de la **sysadmin** rol fijo de servidor puede tener acceso a este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve las colas de correo y estado.  
  
```  
EXECUTE msdb.dbo.sysmail_help_queue_sp ;  
GO  
```  
  
 Se trata de un conjunto de resultados de ejemplo cuya longitud se ha modificado.  
  
```  
queue_type length      state              last_empty_rowset_time  last_activated_time  
---------- -------- ------------------ ----------------------- -----------------------  
mail       0        RECEIVES_OCCURRING 2005-10-07 21:14:47.010 2005-10-10 20:52:51.517  
status     0        INACTIVE           2005-10-07 21:04:47.003 2005-10-10 21:04:47.003  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)  
  
  
