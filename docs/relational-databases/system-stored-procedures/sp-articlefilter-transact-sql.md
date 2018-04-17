---
title: sp_articlefilter (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ca25ec698e928ef247148be55d65c3ea37f59be8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sparticlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Filtra los datos que se publican en función de un artículo de tabla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_articlefilter [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @filter_name = ] 'filter_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación que contiene el artículo. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=**] **'***artículo***'**  
 Es el nombre del artículo. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@filter_name=**] **'***filter_name***'**  
 Es el nombre del procedimiento almacenado de filtro que se creen los *filter_name*. *filter_name* es **nvarchar (386)**, su valor predeterminado es null. Debe especificar un nombre único para el filtro de artículo.  
  
 [  **@filter_clause=**] **'***filter_clause***'**  
 Es una cláusula de restricción (WHERE) que define un filtro horizontal. Al especificar la cláusula de restricción, omita la palabra clave WHERE. *filter_clause* es **ntext**, su valor predeterminado es null.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bits**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo no invalidarán la instantánea no es válida. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo pueden invalidar la instantánea no es válida y si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para marcar como obsoleta la instantánea existente y generar una nueva.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que la acción realizada por este procedimiento almacenado puede requerir que se reinicialicen las suscripciones existentes. *force_reinit_subscription* es un **bits**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo hacen que una necesidad de que se reinicialicen las suscripciones. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de suscripciones, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo hace que se reinicialicen las suscripciones existentes y concede permiso para que se lleve a cabo la reinicialización.  
  
 [  **@publisher=** ] **'***publisher***'**  
 Especifica un no[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse con un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_articlefilter** se utiliza en la replicación de instantáneas y transaccional.  
  
 Ejecutar **sp_articlefilter** para un artículo con las suscripciones existentes que requiere que las suscripciones para reinicialización.  
  
 **sp_articlefilter** crea el filtro, inserta el Id. del procedimiento almacenado de filtro en el **filtro** columna de la [sysarticles &#40;Transact-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md) tabla y, a continuación, Inserta el texto de la cláusula de restricción en la **filter_clause** columna.  
  
 Para crear un artículo con un filtro horizontal, ejecute [sp_addarticle &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) y no tienen ninguna *filtro* parámetro. Ejecutar **sp_articlefilter**, con todos los parámetros, incluido *filter_clause*y, a continuación, ejecute [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md), con todos los parámetros, incluido el mismo parámetro *filter_clause*. Si el filtro ya existe y si la **tipo** en **sysarticles** es **1** (artículo basado en registro), se elimina el filtro anterior y se crea un nuevo filtro.  
  
 Si *filter_name* y *filter_clause* son no siempre, se elimina el filtro anterior y el Id. del filtro se establece en **0**.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_articlefilter**.  
  
## <a name="see-also"></a>Vea también  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir y modificar un filtro de fila estático](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
