---
title: sp_markpendingschemachange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords:
- sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67377f638459a37f25fbc78b9acff395192a2f3f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537337"
---
# <a name="spmarkpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Se utiliza para la compatibilidad de las publicaciones de combinación lo que permite al administrador omitir cambios de esquema pendientes seleccionados para que así no se repliquen. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!CAUTION]  
>  Este procedimiento almacenado puede hacer que los cambios en el esquema no se repliquen. Solo se debe utilizar para resolver problemas después de haber intentando otros métodos, como la reinicialización, o métodos que son demasiado costosos en términos de rendimiento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @schemaversion = ] schemaversion` Identifica un cambio de esquema pendiente. *schemaVersion* es **int**, con un valor predeterminado de **0**. Use [sp_enumeratependingschemachanges &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) para enumerar los cambios de esquema pendiente para la publicación.  
  
`[ @status = ] 'status'` Es si se omitirá un cambio de esquema pendiente. *estado* es **nvarchar (10)** con un valor predeterminado de **active**. Si el valor de *estado* es **omitido**, a continuación, el cambio de esquema seleccionado no se replicarán.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_markpendingschemachange** se usa con la replicación de mezcla.  
  
 **sp_markpendingschemachange** es un procedimiento almacenado pensado para la compatibilidad de la replicación de mezcla y debe usarse solo cuando otras acciones correctivas, como la reinicialización, no se han podido corregir la situación o son demasiado costosas en términos de rendimiento.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Vea también  
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
