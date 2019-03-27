---
title: sp_addpublication_snapshot (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 35b18161e9d0022e0f7df29498a94c40646a5055
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493986"
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Crea el Agente de instantáneas en la publicación especificada. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  Al configurar un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
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
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @frequency_type = ] frequency_type` Es la frecuencia con que se ejecuta el agente de instantáneas. *frequency_type* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Vez.|  
|**4** (valor predeterminado)|Diariamente|  
|**8**|Semanalmente|  
|**16**|Mensualmente|  
|**32**|Mensualmente, según el intervalo de frecuencia|  
|**64**|Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciar el agente.|  
|**128**|Cuando el equipo esté inactivo|  
  
`[ @frequency_interval = ] frequency_interval` Es el valor que se aplican a la frecuencia establecida por *frequency_type*. *frequency_interval* es **int**, y puede tener uno de los siguientes valores.  
  
|Valor de frequency_type|Efecto en frequency_interval|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval* no se utiliza.|  
|**4** (valor predeterminado)|Cada *frequency_interval* días, con un valor predeterminado de diariamente.|  
|**8**|*frequency_interval* es uno o varios de los siguientes (combinados con un [ &#124; (OR bit a bit)](../../t-sql/language-elements/bitwise-or-transact-sql.md) operador lógico):<br /><br /> **1** = el domingo&#124;<br /><br /> **2** = el lunes&#124;<br /><br /> **4** = el martes&#124;<br /><br /> **8** = Wednesday &#124;<br /><br /> **16** = el jueves&#124;<br /><br /> **32** = Friday &#124;<br /><br /> **64** = el sábado|  
|**16**|En el *frequency_interval* día del mes.|  
|**32**|*frequency_interval* es uno de los siguientes:<br /><br /> **1** = el domingo&#124;<br /><br /> **2** = el lunes&#124;<br /><br /> **3** = el martes&#124;<br /><br /> **4** = Wednesday &#124;<br /><br /> **5** = el jueves&#124;<br /><br /> **6** = Friday &#124;<br /><br /> **7** = el sábado&#124;<br /><br /> **8** = día&#124;<br /><br /> **9** = día de la semana&#124;<br /><br /> **10** = día del fin de semana|  
|**64**|*frequency_interval* no se utiliza.|  
|**128**|*frequency_interval* no se utiliza.|  
  
`[ @frequency_subday = ] frequency_subday` Es la unidad para *freq_subday_interval*. *frequency_subday* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Una vez|  
|**2**|Second|  
|**4** (valor predeterminado)|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` Es el intervalo de *frequency_subday*. *frequency_subday_interval* es **int**, su valor predeterminado de 5, lo que significa cada 5 minutos.  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` Es la fecha en que se ejecuta el agente de instantáneas. *frequency_relative_interval* es **int**, su valor predeterminado es 1.  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` Es el factor de periodicidad utilizado por *frequency_type*. *frequency_recurrence_factor* es **int**, su valor predeterminado es 0.  
  
`[ @active_start_date = ] active_start_date` Es la fecha en el agente de instantáneas programada, con el formato AAAAMMDD. *active_start_date* es **int**, su valor predeterminado es 0.  
  
`[ @active_end_date = ] active_end_date` Es la fecha en el agente de instantáneas deja de estar programado, con el formato AAAAMMDD. *active_end_date* es **int**, su valor predeterminado es 99991231, que significa 31 de diciembre de 9999.  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` Es la hora del día, cuando el agente de instantáneas es el primero programada, con el formato HHMMSS. *active_start_time_of_day* es **int**, su valor predeterminado es 0.  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` Es la hora del día en que el agente de instantáneas deja de estar programado, con el formato HHMMSS. *active_end_time_of_day* es **int**, su valor predeterminado es 235959, lo que significa 11:59:59 P.M. como en un reloj de 24 horas.  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'` Es el nombre de un trabajo del agente de instantáneas existente si se usa un trabajo existente. *snapshot_agent_name* es **nvarchar (100)** con un valor predeterminado es null. Este parámetro es solo para uso interno y no se puede especificar al crear una publicación nueva. Si *snapshot_agent_name* se especifica, a continuación, *job_login* y *job_password* debe ser NULL.  
  
`[ @publisher_security_mode = ] publisher_security_mode` Es el modo de seguridad utilizado por el agente al conectarse al publicador. *publisher_security_mode* es **smallint**, su valor predeterminado es 1. **0** especifica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación, y **1** especifica autenticación de Windows. Un valor de **0** debe especificarse para que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` Se usa el inicio de sesión al conectarse al publicador. *publisher_login* es **sysname**, su valor predeterminado es null. *publisher_login* debe especificarse cuando *publisher_security_mode* es **0**. Si *publisher_login* es NULL y *publisher_security_mode* es **1**, la cuenta especificada en *job_login* se usará cuando para conectarse al publicador.  
  
`[ @publisher_password = ] 'publisher_password'` Es la contraseña utilizada al conectarse al publicador. *publisher_password* es **sysname**, su valor predeterminado es null.  
  
> [!IMPORTANT]  
>  No almacene información de autenticación en archivos de script. Para ayudar a mejorar la seguridad, se recomienda proporcionar nombres de inicio de sesión y contraseñas en tiempo de ejecución.  
  
`[ @job_login = ] 'job_login'` Es el inicio de sesión para la cuenta bajo la que se ejecuta el agente. En Azure SQL Database Managed Instance, utilice una cuenta de SQL Server. *job_login* es **nvarchar (257)**, su valor predeterminado es null. Esta cuenta siempre se utiliza para las conexiones del agente al distribuidor. Es preciso proporcionar este parámetro al crear un nuevo trabajo del Agente de instantáneas.  
  
> [!NOTE]
>  Para que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, debe ser el mismo inicio de sesión especificado en [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md).  
  
`[ @job_password = ] 'job_password'` Es la contraseña de la cuenta de Windows que se ejecuta el agente. *job_password* es **sysname**, no tiene ningún valor predeterminado. Es preciso proporcionar este parámetro al crear un nuevo trabajo del Agente de instantáneas.  
  
> [!IMPORTANT]  
>  No almacene información de autenticación en archivos de script. Para ayudar a mejorar la seguridad, se recomienda proporcionar nombres de inicio de sesión y contraseñas en tiempo de ejecución.  
  
`[ @publisher = ] 'publisher'` Especifica que no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *publicador* es **sysname**, su valor predeterminado es null.  
  
> [!NOTE]  
>  *publicador* no debe usarse al crear un agente de instantáneas en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_addpublication_snapshot** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_addpublication_snapshot**.  
  
## <a name="see-also"></a>Vea también  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Crear y aplicar una instantánea](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [sp_addpublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
