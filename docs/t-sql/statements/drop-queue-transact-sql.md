---
title: DROP QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 297ef4c06b88d02e3c1a28829c7223d49c8ecee6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65503712"
---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una cola existente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Nombre de la base de datos que contiene la cola que se va a quitar. Si no se proporciona *database_name*, el valor predeterminado es la base de datos actual.  
  
 *schema_name (object)*  
 Nombre del esquema propietario de la cola que se va a quitar. Si no se proporciona *schema_name*, se usa el esquema predeterminado del usuario actual.  
  
 *queue_name*  
 Nombre de la cola que se va a quitar.  
  
## <a name="remarks"></a>Notas  
 No se puede quitar una cola si hay servicios que hacen referencia a ella.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, se concede permiso para quitar una cola al propietario de esta, a los miembros de los roles fijos de base de datos **db_ddladmin** o **db_owner** y a los miembros del rol fijo de servidor **sysadmin**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se quita la cola **ExpenseQueue** de la base de datos actual.  
  
```  
DROP QUEUE ExpenseQueue ;  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
