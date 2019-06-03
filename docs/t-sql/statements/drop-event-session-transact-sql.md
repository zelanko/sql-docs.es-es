---
title: DROP EVENT SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_EVENT_SESSION_TSQL
- DROP EVENT SESSION
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- DROP EVENT SESSION statement
ms.assetid: 92eabe4b-24e2-43b1-978c-31a199964b90
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6ae8c9e09e62cee4b9234a3dd9f1867b9142d4db
ms.sourcegitcommit: 9388dcccd6b89826dde47b4c05db71274cfb439a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/28/2019
ms.locfileid: "66270179"
---
# <a name="drop-event-session-transact-sql"></a>DROP EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita una sesión de eventos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```    
DROP EVENT SESSION event_session_name  
ON SERVER  
```  
  
## <a name="arguments"></a>Argumentos  
 *event_session_name*  
 El nombre de una sesión de eventos existente.  
  
## <a name="remarks"></a>Notas  
 Al quitar una sesión de eventos, se quita completamente toda la información de configuración, como destinos y parámetros de sesión.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso `ALTER ANY EVENT SESSION`.  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se muestra cómo quitar una sesión de eventos.  
  
```sql  
DROP EVENT SESSION evt_spin_lock_diagnosis ON SERVER;
GO
```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)  
  
  
