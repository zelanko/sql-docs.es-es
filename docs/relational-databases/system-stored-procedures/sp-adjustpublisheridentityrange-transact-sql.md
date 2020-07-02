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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1f58c1a212c722873f66d940de691c89d13d08f5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716304"
---
# <a name="sp_adjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Ajusta el intervalo de identidad de una publicación y reasigna nuevos intervalos según el valor de umbral de la publicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`Es el nombre de la publicación en la que se reasignan los nuevos intervalos de identidad. *Publication* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @table_name = ] 'table_name'`Es el nombre de la tabla en la que se reasignan los nuevos intervalos de identidad. *TABLE_NAME* es de **tipo sysname y su**valor predeterminado es NULL.  
  
`[ @table_owner = ] 'table_owner'`Es el propietario de la tabla en el publicador. *table_owner* es de **tipo sysname y su**valor predeterminado es NULL. Si no se especifica *table_owner* , se usa el nombre del usuario actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_adjustpublisheridentityrange** se utiliza en todos los tipos de replicación.  
  
 En una publicación que tiene habilitado el intervalo de identidad automático, el Agente de distribución o el Agente de mezcla es responsable de ajustar automáticamente el intervalo de identidad en una publicación según su valor de umbral. Sin embargo, si por alguna razón el Agente de distribución o Agente de mezcla no se ha ejecutado durante un período de tiempo, y el recurso de intervalo de identidad se ha consumido en gran medida hasta el punto de umbral, los usuarios pueden llamar a **sp_adjustpublisheridentityrange** para asignar un nuevo intervalo de valores para un publicador.  
  
 Al ejecutar **sp_adjustpublisheridentityrange**, se debe especificar cualquier *publicación* o *TABLE_NAME* . Si se especifican ambos o ninguno, se devolverá un error.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **db_owner** pueden ejecutar **sp_adjustpublisheridentityrange**.  
  
## <a name="see-also"></a>Consulte también  
 [Replicar columnas de identidad](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
