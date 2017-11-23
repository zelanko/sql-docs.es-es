---
title: sp_helpdistpublisher (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords: sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e01aca1558894f52f575aba642cd4079c22f21f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve las propiedades de los publicadores que utilizan un distribuidor. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=** ] **'***publisher***'**  
 Es el publicador cuyas propiedades se van a devolver. *Publisher* es **sysname**, su valor predeterminado es  **%** .  
  
 [  **@check_user=** ] *check_user*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del publicador.|  
|**distribution_db**|**sysname**|Base de datos de distribución del publicador especificado.|  
|**security_mode**|**int**|Modo de seguridad empleado por los agentes de replicación para conectar al publicador para suscripciones de actualización en cola, o con un publicador que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows|  
|**inicio de sesión**|**sysname**|Nombre de inicio de sesión empleado por los agentes de replicación para conectar al publicador para suscripciones de actualización en cola, o con un publicador que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**contraseña**|**nvarchar (524)**|Contraseña devuelta (en forma de cifrado sencillo). Contraseña es distinto de NULL para los usuarios **sysadmin**.|  
|**Active**|**bit**|Indica si un publicador remoto utiliza el servidor local como distribuidor:<br /><br /> **0** = No<br /><br /> **1** = yes|  
|**working_directory**|**nvarchar(255)**|Nombre del directorio de trabajo.|  
|**de confianza**|**bit**|Si se necesita la contraseña cuando un publicador se conecta con el distribuidor. Para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, se debe devolver siempre **0**, lo que significa que la contraseña es obligatoria.|  
|**thirdparty_flag**|**bit**|Indica si la publicación está habilitada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o por una aplicación de terceros:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], oracle o el publicador de puerta de enlace de Oracle.<br /><br /> **1** = publisher se ha integrado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una aplicación de terceros.|  
|**publisher_type**|**sysname**|Tipo de publicador; puede ser uno de los siguientes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **PUERTA DE ENLACE DE ORACLE**|  
|**publisher_data_source**|**nvarchar(4000)**|Nombre del origen de datos OLE DB en el publicador.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdistpublisher** se utiliza en todos los tipos de replicación.  
  
 **sp_helpdistpublisher** no mostrará el inicio de sesión del publicador o se especifica para la contraseña en el resultado no es**sysadmin** inicios de sesión.  
  
## <a name="permissions"></a>Permissions  
 Los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_helpdistpublisher** para los publicadores que utilicen el servidor local como distribuidor. Los miembros de la **db_owner** rol fijo de base de datos o la **replmonitor** en una base de datos de distribución pueden ejecutar **sp_helpdistpublisher** para los publicadores que utilicen que base de datos de distribución. Lista de los usuarios en el acceso a la publicación para una publicación en el índice especificado *publisher* puede ejecutarse **sp_helpdistpublisher**. Si *publisher* no se especifica, se devuelve información para todos los publicadores que el usuario tiene derechos de acceso.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
