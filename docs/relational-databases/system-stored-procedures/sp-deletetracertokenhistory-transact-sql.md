---
title: sp_deletetracertokenhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_deletetracertokenhistory
- sp_deletetracertokenhistory_TSQL
helpviewer_keywords:
- sp_deletetracertokenhistory
ms.assetid: 9ae1be14-0d2f-40b1-9d6e-22d79726abf4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f84cd1cbb9a49f0c13a93fdff721f430983088ca
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955976"
---
# <a name="spdeletetracertokenhistory-transact-sql"></a>sp_deletetracertokenhistory (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Quita los registros desde el [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) y [MStracer_history &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-history-transact-sql.md) las tablas del sistema. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el distribuidor de la base de datos de distribución.

![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="syntax"></a>Sintaxis

```
sp_deletetracertokenhistory [ @publication = ] 'publication'
    [ , [ @tracer_id = ] tracer_id ]
    [ , [ @cutoff_date = ] cutoff_date ]
    [ , [ @publisher = ] 'publisher' ]
    [ , [ @publisher_db = ] 'publisher_db' ]
```

## <a name="arguments"></a>Argumentos

`@publication= 'publication'`  
Es el nombre de la publicación en la que se ha insertado el token de seguimiento. El tipo de datos es **sysname**. Este parámetro es obligatorio.

`[ @tracer_id= ] tracer_id`  
Es el identificador del token de seguimiento que se va a eliminar. El tipo de datos es **int**. El valor predeterminado es *null*. Si *null*, se eliminan todos los testigos de seguimiento que pertenecen a la publicación.

`[ @cutoff_date= ] cutoff_date`  
Testigos de seguimiento insertados en la publicación antes de esta fecha se eliminan. El tipo de datos es **datetime**. El valor predeterminado es *null*.

`[ @publisher= ] 'publisher'`  
Es el nombre del publicador. El tipo de datos es **sysname**. El valor predeterminado es *null*.

> [!NOTE]
> Este parámetro solo debe especificarse para que no sean de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores o cuando se ejecuta el procedimiento almacenado desde el distribuidor.

`[ @publisher_db= ] 'publisher_db'`  
Es el nombre de la base de datos de publicación. El tipo de datos es **sysname**. El valor predeterminado es NULL. Si el procedimiento almacenado se ejecuta en el publicador, se omite este parámetro.

> [!NOTE]
> Este parámetro debe especificarse cuando se ejecuta el procedimiento almacenado desde el distribuidor.

## <a name="return-code-values"></a>Valores de código de retorno

**0** (correcto) o **1** (error)

## <a name="remarks"></a>Comentarios

**sp_deletetracertokenhistory** se utiliza en la replicación transaccional.  

Se produce un error si se especifican ambos parámetros *tracer_id* y *cutoff_date*.

Si no se ejecutan **sp_deletetracertokenhistory** para eliminar los metadatos de token de seguimiento, la información se eliminará cuando se produce la limpieza de historial programada regularmente.

Id. de token de seguimiento se puede determinar mediante la ejecución de [sp_helptracertokens &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql.md) o consultando el [MStracer_tokens &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/mstracer-tokens-transact-sql.md) tabla del sistema.

## <a name="permissions"></a>Permisos

Solo el personal siguiente tiene autoridad para ejecutar **sp_deletetracertokenhistory**:

- Los miembros de la **replmonitor** roles, en la base de datos de distribución
- Los miembros de la **sysadmin** rol fijo de servidor.
- Los miembros de la **db_owner** rol fijo de base de datos, en la base de datos de publicación.
- El **db_owner** de la base de datos fija.

## <a name="see-also"></a>Vea también

[Medir la latencia y validar las conexiones de la replicación transaccional](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)

[sp_helptracertokenhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql.md)
