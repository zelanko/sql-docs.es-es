---
title: sp_replmonitorhelpmergesession (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorhelpmergesession_TSQL
- sp_replmonitorhelpmergesession
helpviewer_keywords:
- sp_replmonitorhelpmergesession
ms.assetid: a0400ba8-9609-4901-917e-925e119103a1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e31f785d1b1fa205a9498889f814a0a0bc32e9a8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834349"
---
# <a name="sp_replmonitorhelpmergesession-transact-sql"></a>sp_replmonitorhelpmergesession (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @agent_name = ] 'agent_name'`Es el nombre del agente. *agent_name* es de tipo **nvarchar (100)** y no tiene ningún valor predeterminado.  
  
`[ @hours = ] hours`Es el intervalo de tiempo, en horas, para el que se devuelve información histórica de la sesión del agente. *hours* es **int**, que puede ser uno de los siguientes intervalos.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|< **0,1**|Devuelve información sobre las ejecuciones pasadas del agente, hasta un máximo de 100.|  
|**0** (valor predeterminado)|Devuelve información sobre todas las ejecuciones pasadas del agente.|  
|> **0,1**|Devuelve información sobre las ejecuciones del agente que se produjeron en *el último número de horas.*|  
  
`[ @session_type = ] session_type`Filtra el conjunto de resultados según el resultado final de la sesión. *session_type* es de **tipo int**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1** (predeterminado)|Sesiones del agente con un reintento o un resultado correcto.|  
|**0**|Sesiones del agente con un resultado erróneo.|  
  
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *Publisher* es de **tipo sysname y su**valor predeterminado es NULL. Este parámetro se utiliza al ejecutar **sp_replmonitorhelpmergesession** en el suscriptor.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos de publicación. *publisher_db* es de **tipo sysname y su**valor predeterminado es NULL. Este parámetro se utiliza al ejecutar **sp_replmonitorhelpmergesession** en el suscriptor.  
  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *Publication* es de **tipo sysname y su**valor predeterminado es NULL. Este parámetro se utiliza al ejecutar **sp_replmonitorhelpmergesession** en el suscriptor.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Session_id**|**int**|Identificador de la sesión de trabajo del agente.|  
|**Estado**|**int**|Estado de la ejecución del agente:<br /><br /> **1** = Inicio<br /><br /> **2** = correcto<br /><br /> **3** = en curso<br /><br /> **4** = inactivo<br /><br /> **5** = reintento<br /><br /> **6** = error|  
|**StartTime**|**datetime**|Hora en que se inició la sesión de trabajo de agente.|  
|**EndTime**|**datetime**|Hora en que finalizó la sesión de trabajo de agente.|  
|**Duración**|**int**|Duración acumulada, en segundos, de esta sesión de trabajo.|  
|**UploadedCommands**|**int**|Número de comandos cargados durante la sesión del agente.|  
|**DownloadedCommands**|**int**|Número de comandos descargados durante la sesión del agente.|  
|**ErrorMessages**|**int**|Número de mensajes de error generados durante la sesión del agente.|  
|**ErrorID**|**int**|Id. del error producido.|  
|**PercentageDone**|**decimal**|Porcentaje estimado de los cambios totales que ya se han entregado en una sesión activa.|  
|**TimeRemaining**|**int**|Número estimado de segundos que restan en una sesión activa.|  
|**CurrentPhase**|**int**|Es la fase actual de una sesión activa y puede ser una de las siguientes.<br /><br /> **1** = carga<br /><br /> **2** = descargar|  
|**LastMessage**|**nvarchar (500)**|Es el último mensaje registrado por el Agente de mezcla durante la sesión.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_replmonitorhelpmergesession** se utiliza para supervisar la replicación de mezcla.  
  
 Cuando se ejecuta en el suscriptor, **sp_replmonitorhelpmergesession** solo devuelve información sobre las últimas cinco sesiones agente de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de base de datos **db_owner** o **replmonitor** en la base de datos de distribución en el distribuidor o en la base de datos de suscripciones del suscriptor pueden ejecutar **sp_replmonitorhelpmergesession**.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar la replicación mediante programación](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
