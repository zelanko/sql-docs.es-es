---
title: sp_enumeratependingschemachanges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a3f0fa918d0247f5fd6dbe11c4a91a2376c52dd
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530817"
---
# <a name="spenumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista de todos los cambios de esquema pendientes. Este procedimiento almacenado puede utilizarse con [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md), lo que permite que un administrador omita cambios de esquema pendientes seleccionados para que no se replican. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @starting_schemaversion = ] starting_schemaversion` Es el cambio de esquema de número más bajo para incluir en el conjunto de resultados.  
  
## <a name="result-set"></a>Tipo de cursor  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|Nombre del artículo al que se aplica el cambio de esquema, o **toda la publicación** los cambios de esquema que se aplican a toda la publicación.|  
|**schemaversion**|**int**|Número del cambio de esquema pendiente.|  
|**schematype**|**sysname**|Valor de texto que representa el tipo de cambio de esquema.|  
|**schematext**|**nvarchar(max)**|[!INCLUDE[tsql](../../includes/tsql-md.md)] que describe el cambio de esquema.|  
|**schemastatus**|**nvarchar(10)**|Indica si hay un cambio de esquema pendiente para el artículo, que puede tener los valores siguientes:<br /><br /> **Active** = cambio de esquema está pendiente<br /><br /> **inactivo** = cambio de esquema está inactivo<br /><br /> **omitir** = no se replica el cambio de esquema|  
|**schemaguid**|**uniqueidentifier**|Identifica el cambio de esquema.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_enumeratependingschemachanges** se utiliza en la replicación de mezcla.  
  
 **sp_enumeratependingschemachanges**, que se usa con [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md), está pensado para la compatibilidad de la replicación de mezcla y debe usarse solo cuando otras acciones correctivas, como reinicialización, no se han podido corregir la situación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_enumeratependingschemachanges**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
