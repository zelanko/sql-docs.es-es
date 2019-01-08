---
title: sp_adjustpublisheridentityrange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adjustpublisheridentityrange_TSQL
- sp_adjustpublisheridentityrange
helpviewer_keywords:
- sp_adjustpublisheridentityrange
ms.assetid: 64f111fd-fb7d-4459-93f7-65f0f8dd7efe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 508eaa25657393dba0d84e0bda6eb0582b3f90fb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822079"
---
# <a name="spadjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ajusta el intervalo de identidad de una publicación y reasigna nuevos intervalos según el valor de umbral de la publicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Es el nombre de la publicación en la que reasignan nuevos rangos de identidad. *publicación* es **sysname**, su valor predeterminado es null.  
  
 [  **@table_name=**] **'***table_name***'**  
 Es el nombre de la tabla en la que reasignan nuevos rangos de identidad. *table_name* es **sysname**, su valor predeterminado es null.  
  
 [  **@table_owner=**] **'***table_owner***'**  
 Es el propietario de la tabla en el publicador. *TABLE_OWNER* es **sysname**, su valor predeterminado es null. Si *table_owner* no se especifica, se usa el nombre del usuario actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_adjustpublisheridentityrange** se utiliza en todos los tipos de replicación.  
  
 En una publicación que tiene habilitado el intervalo de identidad automático, el Agente de distribución o el Agente de mezcla es responsable de ajustar automáticamente el intervalo de identidad en una publicación según su valor de umbral. Sin embargo, si por alguna razón el agente de distribución o el agente de mezcla no se ha ejecutado durante un período de tiempo y el recurso de intervalo de identidad se ha consumido hasta el punto del umbral, los usuarios pueden llamar **sp_adjustpublisheridentityrange** Para asignar un nuevo intervalo de valores para un publicador.  
  
 Al ejecutar **sp_adjustpublisheridentityrange**, ya sea *publicación* o *table_name* debe especificarse. Si se especifican ambos o ninguno, se devolverá un error.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_adjustpublisheridentityrange**.  
  
## <a name="see-also"></a>Vea también  
 [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
