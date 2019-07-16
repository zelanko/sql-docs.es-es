---
title: sp_register_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: c10451148c6f9b2fda231691b770bca3928517f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075751"
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La replicación permite que los procedimientos almacenados personalizados definidos por el usuario sustituyan a uno o más de los procedimientos predeterminados utilizados en la replicación transaccional. Cuando se realiza un cambio en el esquema en una tabla replicada, estos procedimientos almacenados se vuelven a crear. **sp_register_custom_scripting** registra un procedimiento almacenado o [!INCLUDE[tsql](../../includes/tsql-md.md)] archivo de script que se ejecuta cuando se produce un cambio de esquema en el script la definición de un nuevo definido por el usuario procedimiento almacenado personalizado. Este nuevo procedimiento almacenado personalizado definido por el usuario debe reflejar el nuevo esquema de la tabla. **sp_register_custom_scripting** se ejecuta en el publicador de la base de datos de publicación, y el archivo de script registrado o un procedimiento almacenado se ejecuta en el suscriptor cuando se produce un cambio de esquema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @type = ] 'type'` Se está registrando el tipo de procedimiento almacenado personalizado o el script. *tipo* es **varchar (16)** , no tiene ningún valor predeterminado y puede ser uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**insert**|El procedimiento almacenado personalizado registrado se ejecuta cuando se replica una instrucción INSERT.|  
|**update**|El procedimiento almacenado personalizado registrado se ejecuta cuando se replica una instrucción UPDATE.|  
|**delete**|El procedimiento almacenado personalizado registrado se ejecuta cuando se replica una instrucción DELETE.|  
|**custom_script**|El script se ejecuta al final del desencadenador de lenguaje de definición de datos (DDL).|  
  
`[ @value = ] 'value'` Nombre de un procedimiento almacenado o el nombre y la ruta de acceso completa a la [!INCLUDE[tsql](../../includes/tsql-md.md)] archivo de script que se va a registrar. *valor* es **nvarchar (1024)** , no tiene ningún valor predeterminado.  
  
> [!NOTE]  
>  Si se especifica NULL *valor*anulará un script registrado con anterioridad, que es igual que ejecutar el parámetro [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md).  
  
 Cuando el valor de *tipo* es **custom_script**, el nombre y ruta de acceso completa de un [!INCLUDE[tsql](../../includes/tsql-md.md)] se espera que el archivo de script. En caso contrario, *valor* debe ser el nombre de un procedimiento almacenado registrado.  
  
`[ @publication = ] 'publication'` Nombre de la publicación para el que se está registrando el procedimiento almacenado personalizado o una secuencia de comandos. *publicación* es **sysname**, su valor predeterminado es **NULL**.  
  
`[ @article = ] 'article'` Nombre del artículo para el que se está registrando el procedimiento almacenado personalizado o una secuencia de comandos. *artículo* es **sysname**, su valor predeterminado es **NULL**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_register_custom_scripting** se utiliza en la replicación de instantáneas y transaccional.  
  
 Se debe ejecutar este procedimiento almacenado antes de realizar un cambio en el esquema en una tabla replicada. Para obtener más información sobre el uso de este procedimiento almacenado, vea [procedimientos transaccionales de Custom regenerar para reflejar los cambios de esquema](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor el **db_owner** fijo de base de datos, o la **db_ddladmin** rol fijo de base de datos se puede ejecutar **sp_ register_custom_scripting**.  
  
## <a name="see-also"></a>Vea también  
 [sp_unregister_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
