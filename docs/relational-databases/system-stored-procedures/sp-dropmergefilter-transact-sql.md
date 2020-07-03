---
title: sp_dropmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergefilter_TSQL
- sp_dropmergefilter
helpviewer_keywords:
- sp_dropmergefilter
ms.assetid: 798586d7-05f3-4a5e-bea8-a34b7b52d0fd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2de7b17ff172c5945c7bfb83cae6a8a11325e6d0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881816"
---
# <a name="sp_dropmergefilter-transact-sql"></a>sp_dropmergefilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Quita un filtro de mezcla. **sp_dropmergefilter** quita todas las columnas de filtro de mezcla definidas en el filtro de mezcla que se va a quitar. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropmergefilter [ @publication= ] 'publication', [ @article= ] 'article'     , [ @filtername= ] 'filtername'  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @article = ] 'article'`Es el nombre del artículo. *article* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @filtername = ] 'filtername'`Es el nombre del filtro que se va a quitar. *filtername* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`Habilita o deshabilita la posibilidad de invalidar una instantánea. *force_invalidate_snapshot* es un **bit**, con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios en el artículo de mezcla no hacen que la instantánea no sea válida.  
  
 **1** significa que los cambios en el artículo de mezcla pueden hacer que la instantánea no sea válida. En ese caso, el valor **1** concede permiso para que se produzca la nueva instantánea.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`Habilita o deshabilita la capacidad de marcar una suscripción como no válida. *force_reinit_subscription* es un **bit**, con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios en el filtro de artículo de mezcla no hacen que las suscripciones no sean válidas.  
  
 **1** significa que los cambios en el filtro de artículo de mezcla hacen que las suscripciones no sean válidas.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropmergefilter** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_dropmergefilter**.  
  
## <a name="see-also"></a>Consulte también  
 [Cambiar las propiedades de la publicación y del artículo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergefilter &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
