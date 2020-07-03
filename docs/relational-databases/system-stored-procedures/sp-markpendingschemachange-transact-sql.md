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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cea2f7c8f9ce6040f4335428e2c5e97b52a3e591
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899351"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @schemaversion = ] schemaversion`Identifica un cambio de esquema pendiente. *schemaversion* es de **tipo int**y su valor predeterminado es **0**. Use [sp_enumeratependingschemachanges &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) para mostrar los cambios de esquema pendientes de la publicación.  
  
`[ @status = ] 'status'`Indica si se omitirá un cambio de esquema pendiente. *status* es de tipo **nvarchar (10)** y su valor predeterminado es **Active**. Si se **omite**el valor de *status* , no se replicará el cambio de esquema seleccionado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_markpendingschemachange** se utiliza con la replicación de mezcla.  
  
 **sp_markpendingschemachange** es un procedimiento almacenado diseñado para la compatibilidad con la replicación de mezcla y solo debe usarse cuando otras acciones correctivas, como la reinicialización, no han podido corregir la situación o son demasiado costosas en términos de rendimiento.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_markpendingschemachange**.  
  
## <a name="see-also"></a>Consulte también  
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
