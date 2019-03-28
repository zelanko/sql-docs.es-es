---
title: sp_droparticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droparticle_TSQL
- sp_droparticle
helpviewer_keywords:
- sp_droparticle
ms.assetid: 09fec594-53f4-48a5-8edb-c50731c7adb2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cbfeeaa70544c5e2bb19251dfbbccc2e40c22af9
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535747"
---
# <a name="spdroparticle-transact-sql"></a>sp_droparticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un artículo de una publicación de instantáneas o transaccional. No se puede quitar un artículo si hay una o más suscripciones del mismo. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_droparticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @from_drop_publication = ] from_drop_publication ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación que contiene el artículo que se va a quitar. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'` Es el nombre del artículo que se va a quitar. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bit**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo no invalidarán la instantánea no es válido. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo pueden invalidar la instantánea no es válido y si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para marcar como obsoleta la instantánea existente y una nueva instantánea generada.  
  
`[ @publisher = ] 'publisher'` Especifica que no es [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse cuando se cambia las propiedades del artículo en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
`[ @from_drop_publication = ] from_drop_publication` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_droparticle** se utiliza en la replicación de instantáneas y transaccional.  
  
 Artículos filtrados horizontalmente, **sp_droparticle** comprueba la **tipo** columna del artículo en el [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) la tabla a determinar si una vista o filtro también se debe quitar. Si se ha generado automáticamente una vista o un filtro, también se quita con el artículo. Si se creó de forma manual, la vista o filtro no se quita.  
  
 Ejecutar **sp_droparticle** quitar un artículo de una publicación no quita el objeto de la base de datos de publicación o el objeto correspondiente de la base de datos de suscripción. Use `DROP <object>` para quitar manualmente estos objetos, si es necesario.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_droparticle](../../relational-databases/replication/codesnippet/tsql/sp-droparticle-transact-_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_droparticle**.  
  
## <a name="see-also"></a>Vea también  
 [Eliminar un artículo](../../relational-databases/replication/publish/delete-an-article.md)   
 [Agregar y quitar artículos de publicaciones existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
