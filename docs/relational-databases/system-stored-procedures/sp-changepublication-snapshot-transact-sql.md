---
title: sp_changepublication_snapshot (Transact-SQL) | Documentos de Microsoft
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
- sp_changepublication_snapshot_TSQL
- sp_changepublication_snapshot
helpviewer_keywords: sp_changepublication_snapshot
ms.assetid: 518a4618-3592-4edc-8425-cbc33cdff891
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a0a7c888c4851a9bcb671823d0bd46309a00300
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spchangepublicationsnapshot-transact-sql"></a>sp_changepublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades del Agente de instantáneas para la publicación especificada. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changepublication_snapshot [ @publication= ] 'publication'  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication =**] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@frequency_type =**] *frequency_type*  
 Es la frecuencia con que se programa el agente. *frequency_type* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|A petición|  
|**4**|Cada día|  
|**8**|Programación semanal|  
|**16**|Programación mensual|  
|**32**|Mensualmente relativa|  
|**64**|Iniciar automáticamente|  
|**128**|Periódica|  
|NULL (predeterminado)||  
  
 [  **@frequency_interval =**] *frequency_interval*  
 Especifica los días en los que se ejecuta el agente. *frequency_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Domingo|  
|**2**|Lunes|  
|**3**|Martes|  
|**4**|Miércoles|  
|**5**|Jueves|  
|**6**|Viernes|  
|**7**|Sábado|  
|**8**|Day|  
|**9**|Días de la semana|  
|**10**|Días del fin de semana|  
|NULL (predeterminado)||  
  
 [  **@frequency_subday =**] *frequency_subday*  
 Son las unidades para *freq_subday_interval*. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4**|Minute|  
|**8**|Hour|  
|NULL (predeterminado)||  
  
 [  **@frequency_subday_interval =**] *frequency_subday_interval*  
 Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_relative_interval =**] *frequency_relative_interval*  
 Es la fecha en que se ejecuta el agente de instantáneas. *frequency_relative_interval* es **int**, su valor predeterminado es null.  
  
 [  **@frequency_recurrence_factor =**] *frequency_recurrence_factor*  
 Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_date =**] *active_start_date*  
 Es la fecha en que el agente de instantáneas se programa por primera vez, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_date =**] *active_end_date*  
 Es la fecha en la que el agente de instantáneas deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es null.  
  
 [  **@active_start_time_of_day =**] *active_start_time_of_day*  
 Es la hora del día en que el agente de instantáneas se programa por primera vez, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@active_end_time_of_day =**] *active_end_time_of_day*  
 Es la hora del día en que el agente de instantáneas deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es null.  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name***'**  
 Es el nombre de un trabajo del agente de instantáneas existente, si se está utilizando un trabajo existente. *snapshot_agent_name* es **nvarchar (100)** con un valor predeterminado es NULL.  
  
 [  **@publisher_security_mode =** ] *publisher_security_mode*  
 Es el modo de seguridad que el agente utiliza al conectarse al publicador. *publisher_security_mode* es **smallint**, su valor predeterminado es null. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, y **1** especifica autenticación de Windows. Un valor de **0** debe especificarse para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login =** ] **'***publisher_login***'**  
 Es el inicio de sesión utilizado al conectar al publicador. *publisher_login* es **sysname**, su valor predeterminado es null. *publisher_login* debe especificarse cuando *publisher_security_mode* es **0**. Si *publisher_login* es NULL y *publisher_security_mode* es **1**, la cuenta de Windows especificada en *job_login* se utiliza cuando conectarse al publicador.  
  
 [  **@publisher_password =** ] **'***publisher_password***'**  
 Es la contraseña utilizada para conectarse al publicador. *publisher_password* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  No utilice una contraseña en blanco. Utilice una contraseña segura. Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@job_login**  =] **'***job_login***'**  
 Es el inicio de sesión de la cuenta de Windows en la que se ejecuta el agente. *job_login* es **nvarchar (257)**, su valor predeterminado es null. Esta cuenta de Windows siempre se utiliza para conexiones del agente con el distribuidor. Es preciso proporcionar este parámetro al crear un nuevo trabajo del Agente de instantáneas. No es posible cambiar por un publicador que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [  **@job_password =** ] **'***job_password***'**  
 Es la contraseña de la cuenta de Windows en la que se ejecuta el agente. *job_password* es **sysname**, su valor predeterminado es null. Es preciso proporcionar este parámetro al crear un nuevo trabajo del Agente de instantáneas.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [  **@publisher =** ] **'***publisher***'**  
 Especifica un no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publisher. *Publisher* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *Publisher* no debe usarse al crear un agente de instantáneas en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changepublication_snapshot** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos puede ejecutar **sp_changepublication_snapshot**.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication_snapshot &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
