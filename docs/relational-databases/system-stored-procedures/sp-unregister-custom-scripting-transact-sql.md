---
title: sp_unregister_custom_scripting (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
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
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1d2d1e9e081984645fcad82d59d6229f30225502
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
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
 [ **@type** =] **'***tipo***'**  
 Es el tipo de procedimiento almacenado personalizado o el script que se está quitando. *tipo de* es **varchar (16)**, no tiene ningún valor predeterminado y puede ser uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**insert**|El procedimiento almacenado personalizado registrado o el script se ejecuta cuando se replica una instrucción INSERT.|  
|**Actualización**|El procedimiento almacenado personalizado registrado o el script se ejecuta cuando se replica una instrucción UPDATE.|  
|**delete**|El procedimiento almacenado personalizado registrado o el script se ejecuta cuando se replica una instrucción DELETE.|  
|**custom_script**|El procedimiento almacenado personalizado registrado o el script se ejecuta al final del desencadenador de lenguaje de definición de datos (DDL).|  
  
 [ **@publication** =] **'***publicación***'**  
 Nombre de la publicación para la que se está quitando el procedimiento almacenado personalizado o el script. *publicación* es **sysname**, su valor predeterminado es null.  
  
 [ **@article** =] **'***artículo***'**  
 Nombre del artículo para el que se está quitando el procedimiento almacenado personalizado o el script. *artículo* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_unregister_custom_scripting** se utiliza en la replicación de instantáneas y transaccional.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor el **db_owner** función fija de base de datos, o el **db_ddladmin** rol fijo de base de datos puede ejecutar **sp_ unregister_custom_scripting**.  
  
## <a name="see-also"></a>Vea también  
 [sp_register_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
