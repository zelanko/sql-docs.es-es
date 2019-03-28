---
title: sp_dropdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropdistpublisher
- sp_dropdistpublisher_TSQL
helpviewer_keywords:
- sp_dropdistpublisher
ms.assetid: c0bdd3de-3be0-455c-898a-98d4660e7ce3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8acc73e057ff8b91987406e74a28563fecfc9278
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58526457"
---
# <a name="spdropdistpublisher-transact-sql"></a>sp_dropdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un publicador de distribución. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropdistpublisher [ @publisher = ] 'publisher'  
    [ , [ @no_checks = ] no_checks ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el publicador que se va a quitar. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @no_checks = ] no_checks` Especifica si **sp_dropdistpublisher** comprueba que el publicador ha desinstalado el servidor como distribuidor. *no_checks* es **bit**, su valor predeterminado es **0**.  
  
 Si **0**, la replicación comprueba que el publicador remoto ha desinstalado el servidor local como distribuidor. Si el publicador de distribución es local, la replicación comprueba que no quedan objetos de publicación o distribución en el servidor local.  
  
 Si **1**, se quitan todos los objetos de replicación asociados con el publicador de distribución incluso si no se puede alcanzar un publicador remoto. Una vez hecho esto, el publicador remoto debe desinstalar la replicación mediante [sp_dropdistributor](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md) con **@ignore_distributor**  =  **1**.  
  
`[ @ignore_distributor = ] ignore_distributor` Especifica si los objetos de distribución se dejan en el distribuidor cuando se quita el publicador. *ignore_distributor* es **bit** y puede tener uno de estos valores:  
  
 **1** = los objetos de distribución que pertenecen a la *publisher* permanecen en el distribuidor.  
  
 **0** = los objetos de distribución para el *publisher* se limpian en el distribuidor.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropdistpublisher** se utiliza en todos los tipos de replicación.  
  
 Cuando se quita un publicador de Oracle, si no se puede quitar el publicador **sp_dropdistpublisher** devuelve un error y los objetos del distribuidor para el publicador se quitan.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_DropDistPub](../../relational-databases/replication/codesnippet/tsql/sp-dropdistpublisher-tra_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_dropdistpublisher**.  
  
## <a name="see-also"></a>Vea también  
 [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md)  (Deshabilitar la publicación y la distribución)  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
