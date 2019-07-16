---
title: sp_articlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: stevestein
ms.author: sstein
ms.openlocfilehash: acbbd043080b107a5d545408fabe271d62015e54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105081"
---
# <a name="sparticlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza para especificar las columnas incluidas en el artículo para filtrar verticalmente los datos de una tabla publicada. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_articlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column' ]  
    [ , [ @operation = ] 'operation' ]  
    [ , [ @refresh_synctran_procs = ] refresh_synctran_procs ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @change_active = ] change_actve ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @internal = ] 'internal' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación que contiene este artículo. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'` Es el nombre del artículo. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @column = ] 'column'` Es el nombre de la columna que se va a agregar o quitar. *columna* es **sysname**, su valor predeterminado es null. Si es NULL, se publican todas las columnas.  
  
`[ @operation = ] 'operation'` Especifica si se agregan o quitan columnas en un artículo. *operación* es **nvarchar (5)** , con el valor predeterminado es add. **agregar** marca la columna para la replicación. **quitar** anula la selección de la columna.  
  
`[ @refresh_synctran_procs = ] refresh_synctran_procs` Especifica si se vuelven a generar los procedimientos almacenados que admiten suscripciones de actualización inmediata para que coincida con el número de columnas replicadas. *refresh_synctran_procs* es **bit**, su valor predeterminado es **1**. Si **1**, se vuelven a generar los procedimientos almacenados.  
  
`[ @ignore_distributor = ] ignore_distributor` Indica si este procedimiento almacenado se ejecuta sin conectarse al distribuidor. *ignore_distributor* es **bit**, su valor predeterminado es **0**. Si **0**, la base de datos debe estar habilitado para la publicación y la caché de artículos debe actualizarse para reflejar las nuevas columnas replicadas en el artículo. Si **1**, permite quitar los artículos que residen en una base de datos no publicada; deben usarse solo en situaciones de recuperación de las columnas de artículo.  
  
`[ @change_active = ] change_active` Permite modificar las columnas en las publicaciones que tienen suscripciones. *change_active* es un **int** con un valor predeterminado de **0**. Si **0**, no se modifican columnas. Si **1**, las columnas se pueden agregar o quitar de los artículos activos que tienen suscripciones.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bit**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo no invalidarán la instantánea no es válido. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo pueden invalidar la instantánea no es válido y si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para marcar como obsoleta la instantánea existente y una nueva instantánea generada.  
  
 [ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que la acción realizada por este procedimiento almacenado puede requerir la reinicialización de las suscripciones existentes. *force_reinit_subscription* es un **bit**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo no invalidarán la suscripción para reinicializarla. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de suscripciones, se producirá un error y no se realizarán cambios. **1** especifica que los cambios en el artículo que se reinicialicen las suscripciones existentes y concede permiso para que se produzca la reinicialización de suscripción.  
  
`[ @publisher = ] 'publisher'` Especifica que no es [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
`[ @internal = ] 'internal'` Solo para uso interno.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_articlecolumn** se utiliza en la replicación de instantáneas y transaccional.  
  
 Solo un artículo sin suscripciones se puede filtrar usando **sp_articlecolumn**.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_articlecolumn**.  
  
## <a name="see-also"></a>Vea también  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir y modificar un filtro de columna](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
