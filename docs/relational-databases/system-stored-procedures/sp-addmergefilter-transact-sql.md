---
title: sp_addmergefilter (Transact-SQL) | Documentos de Microsoft
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
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords:
- sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bae5cbac50c347247bba5b0488a7fb70ad8e71a3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spaddmergefilter-transact-sql"></a>sp_addmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega un nuevo filtro de mezcla para crear una partición basada en una combinación con otra tabla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addmergefilter [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @filtername = ] 'filtername'   
        , [ @join_articlename = ] 'join_articlename'   
        , [ @join_filterclause = ] join_filterclause  
    [ , [ @join_unique_key = ] join_unique_key ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @filter_type = ] filter_type ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación en la que se agrega el filtro de mezcla. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=** ] **'***artículo***'**  
 Es el nombre del artículo en el que se agrega el filtro de mezcla. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@filtername=** ] **'***filtername***'**  
 Es el nombre del filtro. *filtername* es un parámetro necesario. *filtername*es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@join_articlename=** ] **'***join_articlename***'**  
 Es el artículo primario al que el artículo secundario, especificado por *artículo*, debe combinarse con la cláusula de combinación especificada por *join_filterclause*, para determinar las filas del artículo secundario que cumplen el criterio de filtro del filtro de combinación. *join_articlename* es **sysname**, no tiene ningún valor predeterminado. El artículo debe encontrarse en la publicación dada por *publicación*.  
  
 [  **@join_filterclause=** ] *join_filterclause*  
 Es la cláusula de combinación que se debe usar para combinar el artículo secundario especificado por *artículo*y el artículo primario especificado por *join_article*, para determinar las filas que cumplen criterios del filtro de mezcla. *join_filterclause* es **nvarchar (1000)**.  
  
 [  **@join_unique_key=** ] *join_unique_key*  
 Especifica si la combinación entre el artículo secundario *artículo*y el artículo primario *join_article*es uno a varios, uno a uno, varios a uno o varios a varios. *join_unique_key* es **int**, con un valor predeterminado es 0. **0** indica una combinación de varios a uno o varios a varios. **1** indica una combinación uno a uno o uno a varios. Este valor es **1** cuando las columnas de combinación forman una clave única en *join_article*, o si *join_filterclause* entre una clave externa en *artículo* y una clave principal en *join_article*.  
  
> [!CAUTION]  
>  Solo se establece este parámetro en **1** si tiene una restricción en la columna de combinación en la tabla subyacente para el artículo primario que garantiza la exclusividad. Si *join_unique_key* está establecido en **1** incorrectamente, puede producirse la no convergencia de los datos.  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bits**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios realizados en el artículo de mezcla no invalidarán la instantánea no es válida. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizará ningún cambio.  
  
 **1** especifica que los cambios en el artículo de mezcla pueden invalidar la instantánea no es válida y si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para marcar como obsoleta la instantánea existente y una nueva instantánea genera.  
  
 [  **@force_reinit_subscription=** ] *force_reinit_subscription*  
 Confirma que la acción realizada por este procedimiento almacenado puede requerir que se reinicialicen las suscripciones existentes. *force_reinit_subscription* es un **bits**, con un valor predeterminado es 0.  
  
 **0** especifica que los cambios realizados en el artículo de mezcla no hará que se reinicialice la suscripción. Si el procedimiento almacenado detecta que el cambio requiere que se reinicialicen las suscripciones, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que los cambios en el artículo de mezcla darán lugar a que se reinicialicen las suscripciones existentes y concede permiso para que se lleve a cabo la reinicialización.  
  
 [  **@filter_type=** ] *filter_type*  
 Especifica el tipo de filtro que se agrega. *filter_type* es **tinyint**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Solo filtro de combinación. Debe admitir [!INCLUDE[ssEW](../../includes/ssew-md.md)] los suscriptores.|  
|**2**|Solo relación de registros lógicos.|  
|**3**|Filtro de combinación y relación de registros lógicos.|  
  
 Para más información, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addmergefilter** se utiliza en la replicación de mezcla.  
  
 **sp_addmergefilter** sólo puede utilizarse con artículos de la tabla. No se admiten los artículos de vista ni de vista indizada.  
  
 Este procedimiento se puede utilizar también para agregar una relación lógica entre dos artículos que pueden tener o no un filtro de combinación entre ellos. *filter_type* se utiliza para especificar si el filtro de mezcla que se va a agregar es un filtro de combinación, una relación lógica o ambas cosas.  
  
 Para utilizar registros lógicos, la publicación y los artículos deben satisfacer una serie de requisitos. Para más información, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
 Esta opción se usa normalmente para un artículo que tiene una referencia de clave externa a una tabla de clave principal publicada y la tabla de clave principal tiene un filtro definido en su artículo. El subconjunto de filas de clave principal se usa para determinar las filas de clave externa que se replican en el suscriptor.  
  
 No se puede agregar un filtro de combinación entre dos artículos publicados cuando las tablas de origen de ambos artículos comparten el mismo nombre de objeto de tabla. En tal caso, aunque ambas tablas sean propiedad de esquemas diferentes y tengan nombres de artículo únicos, se producirá un error en la creación del filtro de combinación.  
  
 Cuando se utilizan un filtro de combinación y un filtro de fila con parámetros en un artículo de tabla, la replicación determina si una fila pertenece a una partición de suscriptor. Lo hace mediante la evaluación de la función de filtrado o el filtro de combinación (mediante el [OR](../../t-sql/language-elements/or-transact-sql.md) operador), en lugar de evaluar la intersección de las dos condiciones (mediante el [AND](../../t-sql/language-elements/and-transact-sql.md) operador).  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_addmergefilter**.  
  
## <a name="see-also"></a>Vea también  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Definir y modificar un filtro de combinación entre artículos de mezcla](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
