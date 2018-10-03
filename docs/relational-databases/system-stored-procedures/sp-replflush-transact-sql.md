---
title: sp_replflush (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replflush
- sp_replflush_TSQL
helpviewer_keywords:
- sp_replflush
ms.assetid: 20809f5f-941d-427f-8f0c-de7a6c487584
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2f4919103db6881a99a65572e7c8492147a50b23
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638335"
---
# <a name="spreplflush-transact-sql"></a>sp_replflush (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Vacía la caché de artículos. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  No debería ser necesario ejecutar este procedimiento manualmente. **sp_replflush** solo debe usarse para solucionar problemas de replicación y está dirigido por un profesional de soporte técnico experto en replicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replflush  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replflush** se utiliza en la replicación transaccional.  
  
 Las definiciones de los artículos se almacenan en caché para mejorar la eficacia. **sp_replflush** lo utilizan otros procedimientos almacenados de replicación siempre que se modifica o quita la definición de un artículo.  
  
 Solamente una conexión de cliente puede tener acceso al registro del LOG de una base de datos determinada. Si un cliente tiene acceso a una base de datos de registro del log, ejecutar **sp_replflush** hace que el cliente libere su acceso. Otros clientes, a continuación, pueden examinar el registro de transacciones con **sp_replcmds** o **sp_replshowcmds**.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_replflush**.  
  
## <a name="see-also"></a>Vea también  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
