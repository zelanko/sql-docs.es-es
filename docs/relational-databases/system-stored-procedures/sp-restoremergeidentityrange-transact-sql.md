---
description: sp_restoremergeidentityrange (Transact-SQL)
title: sp_restoremergeidentityrange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_restoremergeidentityrange_TSQL
- sp_restoremergeidentityrange
helpviewer_keywords:
- sp_restoremergeidentityrange
ms.assetid: 7923e422-2748-40c0-b5a8-6410c48d5b70
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ce2166f3179097c44fb8d725fb6125ae8b2b5d06
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551271"
---
# <a name="sp_restoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Este procedimiento almacenado se utiliza para actualizar las asignaciones de intervalos de identidad. Garantiza que la administración automática del intervalo de identidad funciona adecuadamente después de restaurar un publicador a partir de una copia de seguridad. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *Publication* es de **tipo sysname y su**valor predeterminado es **All**. Cuando se especifica, solo se restauran los intervalos de identidad de esa publicación.  
  
`[ @article = ] 'article'` Es el nombre del artículo. *article* es de **tipo sysname y su**valor predeterminado es **All**. Cuando se especifica, solo se restauran los intervalos de identidad de ese artículo.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_restoremergeidentityrange** se utiliza con la replicación de mezcla.  
  
 **sp_restoremergeidentityrange** obtiene la información de asignación de intervalo de identidad máxima del distribuidor y actualiza los valores de la columna **max_used** de [MSmerge_identity_range_allocations &#40;&#41;de Transact-SQL ](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md) para los artículos que usan la administración automática del intervalo de identidad.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_restoremergeidentityrange**.  
  
## <a name="see-also"></a>Consulte también  
 [sp_addmergearticle &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
