---
title: sp_changemergefilter (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
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
- sp_changemergefilter_TSQL
- sp_changemergefilter
helpviewer_keywords:
- sp_changemergefilter
ms.assetid: e08fdfdd-d242-4e85-817b-9f7a224fe567
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 152fa21dbcbac8fbefd2dcae4b0f5bacf78eb5b2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spchangemergefilter-transact-sql"></a>sp_changemergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia algunas propiedades del filtro de mezcla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changemergefilter [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
        , [ @filtername= ] 'filtername'  
        , [ @property= ] 'property'  
        , [ @value= ] 'value'  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@article=** ] **'***artículo***'**  
 Es el nombre del artículo. *artículo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@filtername=** ] **'***filtername***'**  
 Es el nombre actual del filtro. *filtername* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@property=** ] **'***propiedad***'**  
 Es el nombre de la propiedad que se va a cambiar. *propiedad* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@value=**] **'***valor***'**  
 Es el nuevo valor para la propiedad especificada. *valor*es **nvarchar (1000)**, no tiene ningún valor predeterminado.  
  
 En esta tabla se describen las propiedades de los artículos y los valores de esas propiedades.  
  
|Propiedad|Value|Description|  
|--------------|-----------|-----------------|  
|**filter_type**|**1**|Filtro de combinación.<br /><br /> Esta opción es necesaria para admitir los suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)].|  
||**2**|Relación de registros lógicos.|  
||**3**|El filtro de combinación también es una relación de registros lógicos.|  
|**filtername**||Nombre del filtro.|  
|**join_articlename**||Nombre del artículo de combinación.|  
|**join_filterclause**||Cláusula de filtro.|  
|**join_unique_key**|**true**|La combinación se hace sobre una clave exclusiva.|  
||**False**|La combinación no se hace sobre una clave exclusiva.|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bits**, su valor predeterminado es **0**.  
  
 **0** especifica que los cambios en el artículo de mezcla no invalidarán la instantánea no es válida. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** significa que los cambios en el artículo de mezcla pueden invalidar la instantánea no es válida y si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para marcar como obsoleta la instantánea existente y generado una nueva.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que la acción realizada por este procedimiento almacenado puede requerir que se reinicialicen las suscripciones existentes. *force_reinit_subscription* es un **bits** con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios realizados en el artículo de mezcla hacen que la suscripción para reinicializarla. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de las suscripciones existentes, se producirá un error y no se realizarán cambios.  
  
 **1** significa que los cambios en el artículo de mezcla provocará que se reinicialicen las suscripciones existentes y concede permiso para que se lleve a cabo la reinicialización.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changemergefilter** se utiliza en la replicación de mezcla.  
  
 Para cambiar el filtro de un artículo de mezcla es preciso recrear la instantánea, si ya existe. Esto se realiza estableciendo la **@force_invalidate_snapshot** a **1**. Asimismo, si hay suscripciones para este artículo, es necesario reinicializarlas. Esto se hace estableciendo el **@force_reinit_subscription** a **1**.  
  
 Para utilizar registros lógicos, la publicación y los artículos deben satisfacer una serie de requisitos. Para más información, vea [Agrupar cambios en filas relacionadas con registros lógicos](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_changemergefilter**.  
  
## <a name="see-also"></a>Vea también  
 [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
