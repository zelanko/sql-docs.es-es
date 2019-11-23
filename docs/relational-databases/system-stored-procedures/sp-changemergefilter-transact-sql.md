---
title: sp_changemergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergefilter_TSQL
- sp_changemergefilter
helpviewer_keywords:
- sp_changemergefilter
ms.assetid: e08fdfdd-d242-4e85-817b-9f7a224fe567
author: stevestein
ms.author: sstein
ms.openlocfilehash: bfe3cd91150d1990acc410cb4a61af9485c61f4b
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304947"
---
# <a name="sp_changemergefilter-transact-sql"></a>sp_changemergefilter (Transact-SQL)
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
`[ @publication = ] 'publication'` es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'` es el nombre del artículo. *article* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @filtername = ] 'filtername'` es el nombre actual del filtro. *filtername* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @property = ] 'property'` es el nombre de la propiedad que se va a cambiar. *Property* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @value = ] 'value'` es el nuevo valor de la propiedad especificada. el *valor*es **nvarchar (1000)** y no tiene ningún valor predeterminado.  
  
 En esta tabla se describen las propiedades de los artículos y los valores de esas propiedades.  
  
|propiedad|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**filter_type**|**1**|Filtro de combinación.<br /><br /> Esta opción es necesaria para admitir los suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)].|  
||**2**|Relación de registros lógicos.|  
||**3**|El filtro de combinación también es una relación de registros lógicos.|  
|**filtername**||Nombre del filtro.|  
|**join_articlename**||Nombre del artículo de combinación.|  
|**join_filterclause**||Cláusula de filtro.|  
|**join_unique_key**|**true**|La combinación se hace sobre una clave exclusiva.|  
||**False**|La combinación no se hace sobre una clave exclusiva.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bit**, con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios en el artículo de mezcla no hacen que la instantánea no sea válida. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** significa que los cambios en el artículo de mezcla pueden hacer que la instantánea no sea válida y, si hay suscripciones existentes que requieran una nueva instantánea, concede permiso para que la instantánea existente se marque como obsoleta y se genere una nueva instantánea.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` confirma que la acción realizada por este procedimiento almacenado puede requerir que se reinicialicen las suscripciones existentes. *force_reinit_subscription* es un **bit** con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios en el artículo de mezcla no harán que se reinicialice la suscripción. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de las suscripciones existentes, se producirá un error y no se realizarán cambios.  
  
 **1** significa que los cambios en el artículo de mezcla harán que se reinicialicen las suscripciones existentes y concede permiso para que se produzca la reinicialización de la suscripción.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Remarks  
 **sp_changemergefilter** se utiliza en la replicación de mezcla.  
  
 Para cambiar el filtro de un artículo de mezcla es preciso recrear la instantánea, si ya existe. Esto se realiza estableciendo el **\@force_invalidate_snapshot** en **1**. Asimismo, si hay suscripciones para este artículo, es necesario reinicializarlas. Esto se hace estableciendo el **force_reinit_subscription de\@** en **1**.  
  
 Para utilizar registros lógicos, la publicación y los artículos deben satisfacer una serie de requisitos. Para obtener más información, vea [Group Changes to Related Rows with Logical Records](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md) (Agrupar cambios en filas relacionadas con registros lógicos).  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_changemergefilter**.  
  
## <a name="see-also"></a>Vea también  
 [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
