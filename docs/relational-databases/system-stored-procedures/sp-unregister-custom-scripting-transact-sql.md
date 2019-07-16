---
title: sp_unregister_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe6bfe4c93ccabfaaec27739f7a1fd0e09348526
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017898"
---
# <a name="spunregistercustomscripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este procedimiento almacenado quita un procedimiento almacenado personalizado definido por el usuario o [!INCLUDE[tsql](../../includes/tsql-md.md)] archivo de script que se registró mediante la ejecución de [sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @type = ] 'type'` Se está quitando el tipo de procedimiento almacenado personalizado o el script. *tipo* es **varchar (16)** , no tiene ningún valor predeterminado y puede ser uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**insert**|El procedimiento almacenado personalizado registrado o el script se ejecuta cuando se replica una instrucción INSERT.|  
|**update**|El procedimiento almacenado personalizado registrado o el script se ejecuta cuando se replica una instrucción UPDATE.|  
|**delete**|El procedimiento almacenado personalizado registrado o el script se ejecuta cuando se replica una instrucción DELETE.|  
|**custom_script**|El procedimiento almacenado personalizado registrado o el script se ejecuta al final del desencadenador de lenguaje de definición de datos (DDL).|  
  
`[ @publication = ] 'publication'` Nombre de la publicación para que se está quitando el procedimiento almacenado personalizado o una secuencia de comandos. *publicación* es **sysname**, su valor predeterminado es null.  
  
`[ @article = ] 'article'` Nombre del artículo para el que se está quitando el procedimiento almacenado personalizado o una secuencia de comandos. *artículo* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_unregister_custom_scripting** se utiliza en la replicación de instantáneas y transaccional.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor el **db_owner** fijo de base de datos, o la **db_ddladmin** rol fijo de base de datos se puede ejecutar **sp_ unregister_custom_scripting**.  
  
## <a name="see-also"></a>Vea también  
 [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
