---
title: sp_MSchange_logreader_agent_properties (Transact-SQL) | Documentos de Microsoft
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
- sp_MSchange_logreader_agent_properties_TSQL
- sp_MSchange_logreader_agent_properties
helpviewer_keywords:
- sp_MSchange_logreader_agent_properties
ms.assetid: 925df9d3-a041-4046-8e17-c47f40edb86d
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0a9e1e011e762002a227db93146cc8350eea88ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spmschangelogreaderagentproperties-transact-sql"></a>sp_MSchange_logreader_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de un trabajo del agente de lector del registro que se ejecuta en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior distribuidor. Este procedimiento almacenado se utiliza para cambiar las propiedades cuando el publicador se ejecuta en una instancia de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_MSchange_logreader_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 Es el modo de seguridad que el agente utiliza al conectarse al publicador. *publisher_security_mode* es **smallint**, no tiene ningún valor predeterminado.  
  
 **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.  
  
 **1** especifica autenticación de Windows.  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 Es el inicio de sesión utilizado al conectar al publicador. *publisher_login* es **sysname**, no tiene ningún valor predeterminado. *publisher_login* debe especificarse cuando *publisher_security_mode* es **0**. Si *publisher_login* es NULL y *publisher_security_mode* es **1**, la cuenta de Windows especificada en *job_login* se utilizará Cuando se conecta al publicador.  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 Es la contraseña utilizada para conectarse al publicador. *publisher_password* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@job_login**=] **'***job_login***'**  
 Es el inicio de sesión de la cuenta de Windows en la que se ejecuta el agente. *job_login* es **nvarchar (257)**, no tiene ningún valor predeterminado. *Esto no se puede cambiar por un* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publisher.*  
  
 [ **@job_password**=] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows en la que se ejecuta el agente. *job_password* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_type**=] **'***publisher_type***'**  
 Especifica el tipo de publicador cuando el publicador no se ejecuta en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|Especifica un publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica un publicador estándar de Oracle.|  
|**PUERTA DE ENLACE DE ORACLE**|Especifica un publicador de puerta de enlace de Oracle.|  
  
 Para obtener más información acerca de las diferencias entre un publicador de Oracle y un publicador de puerta de enlace de Oracle, vea [Introducción a la publicación Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="remarks"></a>Comentarios  
 **sp_MSchange_logreader_agent_properties** se utiliza en la replicación transaccional.  
  
 Debe especificar todos los parámetros al ejecutar **sp_MSchange_logreader_agent_properties**. Ejecutar [sp_helplogreader_agent &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) para devolver las propiedades actuales del trabajo del agente de lector de registro.  
  
 Después de cambiar un inicio de sesión o una contraseña de agente, debe detener y reiniciar el agente para que el cambio surta efecto.  
  
 Cuando el publicador se ejecuta en una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, debe utilizar [sp_changelogreader_agent](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md) para cambiar las propiedades del agente de lector de registro.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor puede ejecutar **sp_MSchange_logreader_agent_properties**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
