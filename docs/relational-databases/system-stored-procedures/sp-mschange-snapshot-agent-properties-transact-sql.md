---
title: sp_MSchange_snapshot_agent_properties (Transact-SQL) | Microsoft Docs
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
- sp_MSchange_snapshot_agent_properties_TSQL
- sp_MSchange_snapshot_agent_properties
helpviewer_keywords:
- sp_MSchange_snapshot_agent_properties
ms.assetid: 7947a788-3fd7-469f-84db-b03ba89a153c
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67bd8a178ba3e7759257567fdb46af6ddd79daa4
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43019684"
---
# <a name="spmschangesnapshotagentproperties-transact-sql"></a>sp_MSchange_snapshot_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de un trabajo del agente de instantáneas que se ejecuta en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o versión posterior de distribuidor. Este procedimiento almacenado se utiliza para cambiar las propiedades cuando el publicador se ejecuta en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos de distribución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_MSchange_snapshot_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @frequency_type= ] frequency_type  
        , [ @frequency_interval= ] frequency_interval  
        , [ @frequency_subday= ] frequency_subday  
        , [ @frequency_subday_interval= ] frequency_subday_interval  
        , [ @frequency_relative_interval= ] frequency_relative_interval  
        , [ @frequency_recurrence_factor= ] frequency_recurrence_factor  
        , [ @active_start_date= ] active_start_date  
        , [ @active_end_date= ] active_end_date  
        , [ @active_start_time_of_day= ] active_start_time_of_day  
        , [ @active_end_time_of_day= ] active_end_time_of_day  
        , [ @snapshot_job_name = ] 'snapshot_agent_name'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publisher** =] **'***publisher***'**  
 Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publisher_db=** ] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@publication =** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@frequency_type =** ] *frequency_type*  
 Es la frecuencia con que se ejecuta el agente de instantáneas. *frequency_type* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**10**|Programación mensual|  
|**20**|Mensualmente, dependiendo del intervalo de frecuencia|  
|**40**|Cuando se inicia el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 Es el valor que se aplican a la frecuencia establecida por *frequency_type*. *frequency_interval* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 Son las unidades para *freq_subday_interval*. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 Es la fecha en que se ejecuta el agente de instantáneas. *frequency_relative_interval* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, no tiene ningún valor predeterminado.  
  
 [ **@active_start_date =** ] *active_start_date*  
 Es la fecha en que el agente de instantáneas se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, no tiene ningún valor predeterminado.  
  
 [ **@active_end_date =** ] *active_end_date*  
 Es la fecha en la que el agente de instantáneas deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 Es la hora del día en que el agente de instantáneas se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 Es la hora del día en que el agente de instantáneas deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, no tiene ningún valor predeterminado.  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name***'**  
 Es el nombre de un trabajo del agente de instantáneas existente, si se está utilizando un trabajo existente. *snapshot_agent_name* es **nvarchar (100)**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 Es el modo de seguridad que el agente utiliza al conectarse al publicador. *publisher_security_mode* es **int**, no tiene ningún valor predeterminado. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, y **1** especifica autenticación de Windows. Un valor de **0** debe especificarse para que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'***publisher_login***'**  
 Es el inicio de sesión utilizado al conectar al publicador. *publisher_login* es **sysname**, no tiene ningún valor predeterminado. *publisher_login* debe especificarse cuando *publisher_security_mode* es **0**. Si *publisher_login* es NULL y el publicador *_ ** security_mode* es **1**, la cuenta de Windows especificada en *job_login* será se usa al conectarse al publicador.  
  
 [ **@publisher_password**=] **'***publisher_password***'**  
 Es la contraseña utilizada para conectarse al publicador. *publisher_password* es **nvarchar (524)**, no tiene ningún valor predeterminado.  
  
> [!IMPORTANT]  
>  No almacene información de autenticación en archivos de script. Para ayudar a mejorar la seguridad, se recomienda proporcionar nombres de inicio de sesión y contraseñas en tiempo de ejecución.  
  
 [ **@job_login**=] **'***job_login***'**  
 Es el inicio de sesión de la cuenta de Windows en la que se ejecuta el agente. *job_login* es **nvarchar (257)**, no tiene ningún valor predeterminado. Esta cuenta de Windows siempre se utiliza para conexiones del agente con el distribuidor. Es preciso proporcionar este parámetro al crear un nuevo trabajo del Agente de instantáneas. *No se puede cambiar para que no es* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *Publisher.*  
  
 [ **@job_password**=] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows en la que se ejecuta el agente. *job_password* es **sysname**, no tiene ningún valor predeterminado. Es preciso proporcionar este parámetro al crear un nuevo trabajo del Agente de instantáneas.  
  
> [!IMPORTANT]  
>  No almacene información de autenticación en archivos de script. Para ayudar a mejorar la seguridad, se recomienda proporcionar nombres de inicio de sesión y contraseñas en tiempo de ejecución.  
  
 [ **@publisher_type**=] **'***publisher_type***'**  
 Especifica el tipo de publicador cuando el publicador no se ejecuta en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**MSSQLSERVER**|Especifica un publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica un publicador estándar de Oracle.|  
|**PUERTA DE ENLACE DE ORACLE**|Especifica un publicador de puerta de enlace de Oracle.|  
  
 Para obtener más información sobre las diferencias entre un publicador de Oracle y un publicador de puerta de enlace de Oracle, vea [Introducción a la publicación Oracle](../../relational-databases/replication/non-sql/oracle-publishing-overview.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_MSchange_snapshot_agent_properties** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
 Debe especificar todos los parámetros al ejecutar **sp_MSchange_snapshot_agent_properties**. Ejecutar [sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md) para devolver las propiedades actuales del trabajo del agente de instantáneas.  
  
 Cuando el publicador se ejecuta en una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, debe utilizar [sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) para cambiar las propiedades de un trabajo del agente de instantáneas.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor puede ejecutar **sp_MSchange_snapshot_agent_properties**.  
  
## <a name="see-also"></a>Vea también  
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
