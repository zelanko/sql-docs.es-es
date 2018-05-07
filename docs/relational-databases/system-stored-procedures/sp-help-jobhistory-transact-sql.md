---
title: sp_help_jobhistory (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_jobhistory_TSQL
- sp_help_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobhistory
ms.assetid: a944d44e-411b-4735-8ce4-73888d4262d7
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e001e9e0ea0dd7dfdbe64a788db465125b04e414
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpjobhistory-transact-sql"></a>sp_help_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información acerca de los trabajos en los servidores de un dominio de administración multiservidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_jobhistory [ [ @job_id = ] job_id ]   
     [ , [ @job_name = ] 'job_name' ]   
     [ , [ @step_id = ] step_id ]   
     [ , [ @sql_message_id = ] sql_message_id ]   
     [ , [ @sql_severity = ] sql_severity ]   
     [ , [ @start_run_date = ] start_run_date ]   
     [ , [ @end_run_date = ] end_run_date ]   
     [ , [ @start_run_time = ] start_run_time ]   
     [ , [ @end_run_time = ] end_run_time ]   
     [ , [ @minimum_run_duration = ] minimum_run_duration ]   
     [ , [ @run_status = ] run_status ]   
     [ , [ @minimum_retries = ] minimum_retries ]   
     [ , [ @oldest_first = ] oldest_first ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @mode = ] 'mode' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@job_id=** ] *job_id*  
 El número de identificación del trabajo. *job_id* es **uniqueidentifier**, su valor predeterminado es null.  
  
 [  **@job_name=** ] **'***job_name***'**  
 Nombre del trabajo. *job_name* es **sysname**, su valor predeterminado es null.  
  
 [  **@step_id=** ] *step_id*  
 El número de identificación del paso. *step_id* es **int**, su valor predeterminado es null.  
  
 [  **@sql_message_id=** ] *sql_message_id*  
 Número de identificación del mensaje de error devuelto por Microsoft SQL Server cuando se ejecuta el trabajo. *sql_message_id* es **int**, su valor predeterminado es null.  
  
 [  **@sql_severity=** ] *sql_severity*  
 Nivel de gravedad del mensaje de error devuelto por SQL Server cuando se ejecuta el trabajo. *sql_severity* es **int**, su valor predeterminado es null.  
  
 [  **@start_run_date=** ] *start_run_date*  
 Fecha en que se inició el trabajo. *start_run_date*es **int**, su valor predeterminado es null. *start_run_date* se debe escribir con el formato AAAAMMDD, donde AAAA es un año con cuatro cifras, MM es un nombre de mes con dos cifras y DD es el día con dos cifras.  
  
 [  **@end_run_date=** ] *end_run_date*  
 Fecha en que se completó el trabajo. *end_run_date* es **int**, su valor predeterminado es null. *end_run_date*se debe escribir con el formato AAAAMMDD, donde AAAA es un año con cuatro cifras, MM es un nombre de mes con dos cifras y DD es el día con dos cifras.  
  
 [  **@start_run_time=** ] *start_run_time*  
 Hora a la que comenzó el trabajo. *start_run_time* es **int**, su valor predeterminado es null. *start_run_time*se debe escribir con el formato HHMMSS, donde HH es la hora del día, MM son los minutos del día dos cifras y SS son los segundos dos caracteres del día.  
  
 [  **@end_run_time=** ] *end_run_time*  
 Hora a la que se completó la ejecución del trabajo. *end_run_time* es **int**, su valor predeterminado es null. *end_run_time*se debe escribir con el formato HHMMSS, donde HH es la hora del día, MM son los minutos del día dos cifras y SS son los segundos dos caracteres del día.  
  
 [  **@minimum_run_duration=** ] *minimum_run_duration*  
 Duración mínima de la realización del trabajo. *minimum_run_duration* es **int**, su valor predeterminado es null. *minimum_run_duration*se debe escribir con el formato HHMMSS, donde HH es la hora del día, MM son los minutos del día dos cifras y SS son los segundos dos caracteres del día.  
  
 [  **@run_status=** ] *run_status*  
 Estado de ejecución del trabajo. *run_status* es **int**, su valor predeterminado es null y puede tener uno de estos valores.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**0**|Error|  
|**1**|Se realizó correctamente|  
|**2**|Reintento (solo pasos)|  
|**3**|Canceled|  
|**4**|Mensaje en curso|  
|**5**|Desconocido|  
  
 [  **@minimum_retries=** ] *minimum_retries*  
 Número mínimo de veces que se debe volver a intentar la ejecución de un trabajo. *minimum_retries* es **int**, su valor predeterminado es null.  
  
 [  **@oldest_first=** ] *oldest_first*  
 Indica si la salida se debe presentar con los trabajos más antiguos en primer lugar. *oldest_first* es **int**, su valor predeterminado es **0**, que presenta los trabajos más recientes en primer lugar. **1** presenta los trabajos más antiguos en primer lugar.  
  
 [  **@server=** ] **'***server***'**  
 Nombre del servidor en el que se realizó el trabajo. *servidor* es **nvarchar (30)**, su valor predeterminado es null.  
  
 [  **@mode=** ] **'***modo***'**  
 Indica si SQL Server imprime todas las columnas del conjunto de resultados (**completa**) o un resumen de las columnas. *modo* es **varchar(7)**, su valor predeterminado es **resumen**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 La lista de columnas depende del valor de *modo*. El conjunto de columnas más completo se muestra a continuación y se devuelve cuando *modo* es FULL.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**valor de instance_id**|**int**|Número de identificación de la entrada en el historial.|  
|**job_id**|**uniqueidentifier**|Número de identificación del trabajo.|  
|**job_name**|**sysname**|Nombre del trabajo.|  
|**step_id**|**int**|Número de identificación de paso (será **0** para un historial de trabajos).|  
|**Step_name**|**sysname**|Nombre de paso (será NULL para un historial de trabajos).|  
|**sql_message_id**|**int**|Para pasos [!INCLUDE[tsql](../../includes/tsql-md.md)], número de error de [!INCLUDE[tsql](../../includes/tsql-md.md)] más reciente encontrado en la ejecución del comando.|  
|**sql_severity**|**int**|Para pasos [!INCLUDE[tsql](../../includes/tsql-md.md)], nivel de gravedad más alto de los errores de [!INCLUDE[tsql](../../includes/tsql-md.md)] encontrado en la ejecución del comando.|  
|**message**|**nvarchar(1024)**|Mensaje del historial de trabajos o pasos.|  
|**run_status**|**int**|Resultado del trabajo o del paso.|  
|**run_date**|**int**|Fecha en que empezó la ejecución del trabajo o del paso.|  
|**run_time**|**int**|Hora en que empezó la ejecución del trabajo o del paso.|  
|**run_duration**|**int**|Tiempo transcurrido en la ejecución del trabajo o paso en formato HHMMSS.|  
|**operator_emailed**|**nvarchar (20)**|Operador que recibió mensajes de correo electrónico relativos a este trabajo (es NULL para el historial de pasos).|  
|**operator_netsent**|**nvarchar (20)**|Operador que recibió mensajes de red relativos a este trabajo (es NULL para el historial de pasos).|  
|**operator_paged**|**nvarchar (20)**|Operador que recibió mensajes de localizador relativos a este trabajo (es NULL para el historial de pasos).|  
|**retries_attempted**|**int**|Número de veces que se ha vuelto a intentar el paso (siempre es 0 para un historial de trabajos).|  
|**servidor**|**nvarchar(30)**|Servidor en el que se ejecuta el paso o el trabajo. Siempre es (**local**).|  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_jobhistory** devuelve un informe con el historial de los trabajos programados especificados. Si no se especifican parámetros, el informe contiene el historial de todos los trabajos programados.  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento almacenado. Al resto de usuarios se les debe conceder uno de los siguientes roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para detalles sobre los permisos de estos roles, consulte [Roles fijos de base de datos del Agente SQL Server](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
 Los miembros de la **SQLAgentUserRole** rol de base de datos solo puede ver el historial de trabajos que les pertenecen.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-listing-all-job-information-for-a-job"></a>A. Mostrar toda la información de un trabajo  
 En el siguiente ejemplo se muestra toda la información del trabajo `NightlyBackups`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobhistory   
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-that-match-certain-conditions"></a>B. Mostrar información de trabajos que cumplen determinadas condiciones  
 En el siguiente ejemplo se imprimen todas las columnas y toda la información de los trabajos o pasos de trabajo que no progresaron y devolvieron el mensaje de error `50100` (mensaje de error definido por el usuario) y una gravedad de `20`.  
  
```  
USE msdb  
GO  
  
EXEC dbo.sp_help_jobhistory  
    @sql_message_id = 50100,  
    @sql_severity = 20,  
    @run_status = 0,  
    @mode = N'FULL' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
