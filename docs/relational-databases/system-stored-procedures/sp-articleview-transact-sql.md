---
title: sp_articleview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords:
- sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b06d348358a141771816230179ca7deae4e4353a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132866"
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea la vista que define el artículo publicado cuando una tabla se filtra horizontal o verticalmente. Esta vista se utiliza como el origen filtrado del esquema y los datos de las tablas de destino. Con este procedimiento almacenado solamente pueden modificarse artículos sin suscripciones. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_articleview [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @view_name = ] 'view_name']  
    [ , [ @filter_clause = ] 'filter_clause']  
    [ , [ @change_active = ] change_active ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @refreshsynctranprocs = ] refreshsynctranprocs ]  
    [ , [ @internal = ] internal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'**_publicación_**'**  
 Es el nombre de la publicación que contiene el artículo. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=**] **'**_artículo_**'**  
 Es el nombre del artículo. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@view_name=**] **'**_view_name_**'**  
 Es el nombre de la vista que define el artículo publicado. *view_name* es **nvarchar (386)**, su valor predeterminado es null.  
  
 [  **@filter_clause=**] **'**_filter_clause_**'**  
 Es una cláusula de restricción (WHERE) que define un filtro horizontal. Cuando escriba la cláusula de restricción, omita la palabra clave WHERE. *filter_clause* es **ntext**, su valor predeterminado es null.  
  
 [  **@change_active =** ] *change_active*  
 Permite modificar las columnas en publicaciones con suscripciones. *change_active* es un **int**, su valor predeterminado es **0**. Si **0**, no se cambian las columnas. Si **1**, las vistas se pueden crear o volver a crear en los artículos activos que tienen suscripciones.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bit**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo no invalidarán la instantánea no es válido. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo pueden invalidar la instantánea no es válido y si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para marcar como obsoleta la instantánea existente y una nueva instantánea generada.  
  
 [  **@force_reinit_subscription =]** _force_reinit_subscription_  
 Confirma que la acción realizada por este procedimiento almacenado puede requerir la reinicialización de las suscripciones existentes. *force_reinit_subscription* es un **bit** con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios en el artículo no invalidarán la suscripción para reinicializarla. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de suscripciones, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo hace que la suscripción existente para reinicializarla y concede permiso para que se produzca la reinicialización de suscripción.  
  
 [ **@publisher**=] **'**_publisher_**'**  
 Especifica que no es [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no se debe usar al publicar desde un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
 [ **@refreshsynctranprocs** =] *refreshsynctranprocs*  
 Indica si los procedimientos almacenados utilizados para sincronizar la replicación se vuelven a crear automáticamente. *refreshsynctranprocs* es **bit**, su valor predeterminado es 1.  
  
 **1** significa que los procedimientos almacenados se vuelven a creados.  
  
 **0** significa que los procedimientos almacenados no se vuelven a creados.  
  
 [ **@internal**=] *interno*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_articleview** crea la vista que define el artículo publicado e inserta el Id. de esta vista en el **sync_objid** columna de la [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabla e inserta el texto de la cláusula de restricción en la **filter_clause** columna. Si se replican todas las columnas y no hay ningún **filter_clause**, el **sync_objid** en el [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabla está establecida en el identificador de la tabla base y el uso de **sp_articleview** no es necesario.  
  
 Para publicar una tabla filtrada verticalmente (es decir, para filtrar columnas) ejecuta por primera vez **sp_addarticle** no *sync_object* parámetro, ejecute [sp_articlecolumn &#40;&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) una vez para cada columna replicar (definiendo el filtro vertical) y, a continuación, ejecute **sp_articleview** para crear la vista que define el artículo publicado.  
  
 Para publicar una tabla filtrada horizontalmente (es decir, para filtrar filas), ejecute [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) no *filtro* parámetro. Ejecute [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md), con todos los parámetros, incluido *filter_clause*. A continuación, ejecute **sp_articleview**, con todos los parámetros, incluido el idénticos *filter_clause*.  
  
 Para publicar una tabla filtrada vertical y horizontalmente, ejecute [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) no *sync_object* o *filtro* parámetros. Ejecute [sp_articlecolumn &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md) una vez para cada columna que se va a replicarse y luego ejecute [sp_articlefilter &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) y **sp_ articleview**.  
  
 Si el artículo ya tiene una vista que define el artículo publicado, **sp_articleview** quita la vista existente y crea automáticamente una nueva. Si la vista se creó manualmente (**tipo** en [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) es **5**), no se quita la vista existente.  
  
 Si crea un procedimiento almacenado de filtro personalizado y una vista que define el artículo publicado de forma manual, no ejecute **sp_articleview**. En su lugar, proporciónelos como el *filtro* y *sync_object* parámetros [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), junto con el adecuado*tipo* valor.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_articleview**.  
  
## <a name="see-also"></a>Vea también  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir y modificar un filtro de fila estático](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
