---
title: sp_mergearticlecolumn (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 083d6d27d9417a76f9cafc1c3726e3f7c10df6d7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spmergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea particiones verticales en una publicación de combinación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_mergearticlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column'  
    [ , [ @operation = ] 'operation'   
    [ , [ @schema_replication = ] 'schema_replication' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =**] **'***publicación***'**  
 Es el nombre de la publicación. *Publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article =**] **'***artículo***'**  
 Es el nombre del artículo de la publicación. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@column =**] **'***columna***'**  
 Identifica las columnas donde se va a crear la partición vertical. *columna* es **sysname**, su valor predeterminado es null. Si es NULL y `@operation = N'add'`, de manera predeterminada se agregan al artículo todas las columnas de la tabla de origen. *columna* no puede ser NULL cuando *operación* está establecido en **quitar**. Para excluir las columnas de un artículo, ejecute **sp_mergearticlecolumn** y especifique *columna* y `@operation = N'drop'` para cada columna que desee quitar del elemento especificado *artículo*.  
  
 [  **@operation =**] **'***operación***'**  
 Es el estado de replicación. *operación* es **nvarchar (4)**, con un valor predeterminado es ADD. **agregar** marca la columna para la replicación. **quitar** borra la columna.  
  
 [  **@schema_replication=**] **'***el argumento schema_replication***'**  
 Especifica que un cambio en el esquema se propagará al ejecutar el agente de mezcla. *el argumento schema_replication* es **nvarchar (5)**, con un valor predeterminado es FALSE.  
  
> [!NOTE]  
>  Solo **FALSE** es compatible con *el argumento schema_replication*.  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Habilita o deshabilita la capacidad de que se invalide una instantánea. *force_invalidate_snapshot* es un **bits**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios realizados en el artículo de mezcla no invalidarán la instantánea no es válida.  
  
 **1** especifica que los cambios realizados en el artículo de mezcla pueden invalidar la instantánea no es válida, y si ese es el caso, un valor de **1** concede permiso para la nueva instantánea para que se produzca.  
  
 [  **@force_reinit_subscription =]***force_reinit_subscription*  
 Habilita o deshabilita la capacidad de reinicializar la suscripción. *force_reinit_subscription* es un poco con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios realizados en el artículo de mezcla no hará que se reinicialice la suscripción.  
  
 **1** especifica que los cambios realizados en el artículo de mezcla pueden causar la suscripción para reinicializarla, y si ese es el caso, un valor de **1** concede permiso para que se lleve a cabo la reinicialización.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_mergearticlecolumn** se utiliza en la replicación de mezcla.  
  
 No es posible quitar una columna de identidad del artículo si se está utilizando la administración automática del intervalo de identidad. Para más información, vea [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 Si una aplicación establece una nueva partición vertical después de crear la instantánea inicial, es necesario generar una instantánea nueva y volverla a aplicar a cada suscripción. Las instantáneas se aplican al ejecutar el siguiente Agente de instantáneas, distribución o mezcla programado.  
  
 Si se utiliza el seguimiento por fila en la detección de conflictos (valor predeterminado), la tabla base puede incluir un máximo de 1024 columnas, pero en el artículo deben filtrarse las columnas de forma que se publique un máximo de 246 columnas. Si se utiliza el seguimiento por columna, la tabla base puede incluir 246 columnas como máximo.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_mergearticlecolumn**.  
  
## <a name="see-also"></a>Vea también  
 [Definir y modificar un filtro de combinación entre artículos de mezcla](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Definir y modificar un filtro de fila con parámetros para un artículo de mezcla](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Filtrar datos publicados](../../relational-databases/replication/publish/filter-published-data.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
