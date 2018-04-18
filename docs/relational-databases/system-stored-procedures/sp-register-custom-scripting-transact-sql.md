---
title: sp_register_custom_scripting (Transact-SQL) | Documentos de Microsoft
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
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b0f249f4c70ec6892ca6cb576dad0d70c60527b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La replicación permite que los procedimientos almacenados personalizados definidos por el usuario sustituyan a uno o más de los procedimientos predeterminados utilizados en la replicación transaccional. Cuando se realiza un cambio en el esquema en una tabla replicada, estos procedimientos almacenados se vuelven a crear. **sp_register_custom_scripting** registra un procedimiento almacenado o [!INCLUDE[tsql](../../includes/tsql-md.md)] archivo de script que se ejecuta cuando se produce un cambio de esquema al script de la definición de un nuevo definido por el usuario procedimiento almacenado personalizado. Este nuevo procedimiento almacenado personalizado definido por el usuario debe reflejar el nuevo esquema de la tabla. **sp_register_custom_scripting** se ejecuta en el publicador de la base de datos de publicación y el archivo de script registrado o un procedimiento almacenado se ejecuta en el suscriptor cuando se produce un cambio de esquema.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@type** =] **'***tipo***'**  
 Es el tipo de procedimiento almacenado personalizado o el script que se registra. *tipo de* es **varchar (16)**, no tiene ningún valor predeterminado y puede ser uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**insert**|El procedimiento almacenado personalizado registrado se ejecuta cuando se replica una instrucción INSERT.|  
|**Actualización**|El procedimiento almacenado personalizado registrado se ejecuta cuando se replica una instrucción UPDATE.|  
|**delete**|El procedimiento almacenado personalizado registrado se ejecuta cuando se replica una instrucción DELETE.|  
|**custom_script**|El script se ejecuta al final del desencadenador de lenguaje de definición de datos (DDL).|  
  
 [ **@value**=] **'***valor***'**  
 Nombre de un procedimiento almacenado o nombre y ruta de acceso completa al archivo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se está registrando. *valor* es **nvarchar (1024)**, no tiene ningún valor predeterminado.  
  
> [!NOTE]  
>  Si se especifica NULL *valor*parámetro anulará el registro un script registrado con anterioridad, que es igual que ejecutar [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md).  
  
 Cuando el valor de *tipo* es **custom_script**, el nombre y la ruta de acceso completa de un [!INCLUDE[tsql](../../includes/tsql-md.md)] se espera que el archivo de script. En caso contrario, *valor* debe ser el nombre de un procedimiento almacenado registrado.  
  
 [ **@publication**=] **'***publicación***'**  
 Nombre de la publicación para la que se está registrando el procedimiento almacenado personalizado o el script. *publicación* es **sysname**, su valor predeterminado es **NULL**.  
  
 [ **@article**=] **'***artículo***'**  
 Nombre del artículo para el que se está registrando el procedimiento almacenado personalizado o el script. *artículo* es **sysname**, su valor predeterminado es **NULL**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_register_custom_scripting** se utiliza en la replicación de instantáneas y transaccional.  
  
 Se debe ejecutar este procedimiento almacenado antes de realizar un cambio en el esquema en una tabla replicada. Para obtener más información sobre el uso de este procedimiento almacenado, vea [regenerar personalizado transaccional procedimientos para reflejar los cambios de esquema](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor el **db_owner** función fija de base de datos, o el **db_ddladmin** rol fijo de base de datos puede ejecutar **sp_ register_custom_scripting**.  
  
## <a name="see-also"></a>Vea también  
 [sp_unregister_custom_scripting &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
