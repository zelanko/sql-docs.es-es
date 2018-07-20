---
title: sp_helpdistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4eed56a7e9356ac7f42c5f1bf2a5d55e85111523
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082417"
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
 Es el publicador cuyas propiedades se van a devolver. *publicador* es **sysname**, su valor predeterminado es **%**.  
  
 [  **@check_user=** ] *check_user*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del publicador.|  
|**distribution_db**|**sysname**|Base de datos de distribución del publicador especificado.|  
|**security_mode**|**int**|Modo de seguridad empleado por los agentes de replicación para conectar al publicador para suscripciones de actualización en cola, o con un publicador que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows|  
|**inicio de sesión**|**sysname**|Nombre de inicio de sesión empleado por los agentes de replicación para conectar al publicador para suscripciones de actualización en cola, o con un publicador que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**password**|**nvarchar (524)**|Contraseña devuelta (en forma de cifrado sencillo). Contraseña es NULL para los usuarios no sean **sysadmin**.|  
|**Active**|**bit**|Indica si un publicador remoto utiliza el servidor local como distribuidor:<br /><br /> **0** = No<br /><br /> **1** = Sí|  
|**working_directory**|**nvarchar(255)**|Nombre del directorio de trabajo.|  
|**confianza**|**bit**|Si se necesita la contraseña cuando un publicador se conecta con el distribuidor. Para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, esto debe devolver siempre **0**, lo que significa que la contraseña es obligatoria.|  
|**thirdparty_flag**|**bit**|Indica si la publicación está habilitada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o por una aplicación de terceros:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], oracle o el publicador de puerta de enlace de Oracle.<br /><br /> **1** = publisher se ha integrado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una aplicación de terceros.|  
|**publisher_type**|**sysname**|Tipo de publicador; puede ser uno de los siguientes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **PUERTA DE ENLACE DE ORACLE**|  
|**publisher_data_source**|**nvarchar(4000)**|Nombre del origen de datos OLE DB en el publicador.|  
|**storage_connection_string**|**nvarchar(4000)**|Clave de acceso de almacenamiento para el directorio de trabajo al distribuidor ni publicador en Azure SQL Database.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_helpdistpublisher** se utiliza en todos los tipos de replicación.  
  
 **sp_helpdistpublisher** no mostrará el inicio de sesión del publicador o con contraseña en el resultado se establece para que no sean de**sysadmin** inicios de sesión.  
  
## <a name="permissions"></a>Permisos  
 Los miembros de la **sysadmin** puede ejecutar el rol fijo de servidor **sp_helpdistpublisher** para los publicadores que utilicen el servidor local como distribuidor. Los miembros de la **db_owner** rol fijo de base de datos o el **replmonitor** en una base de datos de distribución pueden ejecutar **sp_helpdistpublisher** para los publicadores que utilicen que base de datos de distribución. Lista de usuarios en el acceso a la publicación para una publicación en el índice especificado *publisher* pueden ejecutar **sp_helpdistpublisher**. Si *publisher* no se especifica, se devolverá información para todos los publicadores que el usuario tiene derechos de acceso.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
