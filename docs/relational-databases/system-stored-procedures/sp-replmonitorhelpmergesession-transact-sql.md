---
title: sp_replmonitorhelpmergesession (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
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
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords: sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 111c25448a3c9699451b22e1513e217988b475f6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spreplmonitorhelpmergesession-transact-sql"></a>sp_replmonitorhelpmergesession (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información acerca de sesiones pasadas de un Agente de mezcla de replicación concreto, con una fila por cada sesión que coincida con el criterio de filtrado. Este procedimiento almacenado, que se utiliza para supervisar la replicación de mezcla, se ejecuta en el distribuidor de la base de datos de distribución o en el suscriptor de la base de datos de suscripciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replmonitorhelpmergesession [ [ @agent_name = ] 'agent_name' ]  
    [ , [ @hours = ] hours ]  
    [ , [ @session_type = ] session_type ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
    [ , [ @publication = ] 'publication' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@agent_name**  =] **'***agent_name***'**  
 Es el nombre del agente. *agent_name* es **nvarchar (100)** no tiene ningún valor predeterminado.  
  
 [  **@hours**  =] *horas*  
 Es el intervalo de tiempo en horas sobre el que se devuelve información de historial de las sesiones del agente. *horas* es **int**, que puede ser uno de los siguientes intervalos.  
  
|Valor|Description|  
|-----------|-----------------|  
|< **0**|Devuelve información sobre las ejecuciones pasadas del agente, hasta un máximo de 100.|  
|**0** (valor predeterminado)|Devuelve información sobre todas las ejecuciones pasadas del agente.|  
|> **0**|Devuelve información sobre agente ejecuciones que se ha producido en los últimos *horas* número de horas.|  
  
 [  **@session_type**  =] *session_type*  
 Filtra el conjunto de resultados según el resultado del fin de la sesión. *session_type* es **int**, y puede tener uno de estos valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**1** (predeterminado)|Sesiones del agente con un reintento o un resultado correcto.|  
|**0**|Sesiones del agente con un resultado erróneo.|  
  
 [  **@publisher**  =] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, su valor predeterminado es null. Este parámetro se usa al ejecutar **sp_replmonitorhelpmergesession** en el suscriptor.  
  
 [  **@publisher_db**  =] **'***publisher_db***'**  
 Es el nombre de la base de datos de publicación. *publisher_db* es **sysname**, su valor predeterminado es null. Este parámetro se usa al ejecutar **sp_replmonitorhelpmergesession** en el suscriptor.  
  
 [  **@publication=** ] **'***publicación***'**  
 Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es null. Este parámetro se usa al ejecutar **sp_replmonitorhelpmergesession** en el suscriptor.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Session_id**|**int**|Identificador de la sesión de trabajo del agente.|  
|**Estado**|**int**|Estado de la ejecución del agente:<br /><br /> **1** = inicio<br /><br /> **2** = correctamente<br /><br /> **3** = en curso<br /><br /> **4** = inactivo<br /><br /> **5** = reintento<br /><br /> **6** = error|  
|**StartTime**|**datetime**|Hora en que se inició la sesión de trabajo de agente.|  
|**EndTime**|**datetime**|Hora en que finalizó la sesión de trabajo de agente.|  
|**Duración**|**int**|Duración acumulada, en segundos, de esta sesión de trabajo.|  
|**UploadedCommands**|**int**|Número de comandos cargados durante la sesión del agente.|  
|**DownloadedCommands**|**int**|Número de comandos descargados durante la sesión del agente.|  
|**ErrorMessages**|**int**|Número de mensajes de error generados durante la sesión del agente.|  
|**Identificador del error**|**int**|Id. del error producido.|  
|**PercentageDone**|**decimal**|Porcentaje estimado de los cambios totales que ya se han entregado en una sesión activa.|  
|**TimeRemaining**|**int**|Número estimado de segundos que restan en una sesión activa.|  
|**CurrentPhase**|**int**|Es la fase actual de una sesión activa y puede ser una de las siguientes.<br /><br /> **1** = carga<br /><br /> **2** = descarga|  
|**LastMessage**|**nvarchar (500)**|Es el último mensaje registrado por el Agente de mezcla durante la sesión.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replmonitorhelpmergesession** se usa para supervisar la replicación de mezcla.  
  
 Cuando se ejecuta en el suscriptor, **sp_replmonitorhelpmergesession** solamente devuelve información sobre las últimas cinco sesiones del agente de mezcla.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **db_owner** o **replmonitor** fijo de base de datos en la base de datos de distribución en el distribuidor o en la base de datos de suscripción en el suscriptor pueden ejecutar **sp_ replmonitorhelpmergesession**.  
  
## <a name="see-also"></a>Vea también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
