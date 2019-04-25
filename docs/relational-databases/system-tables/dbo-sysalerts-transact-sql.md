---
title: dbo.sysalerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysalerts
- sysalerts_TSQL
- dbo.sysalerts_TSQL
- sysalerts
dev_langs:
- TSQL
helpviewer_keywords:
- sysalerts system table
ms.assetid: a2c2f50d-61f3-4951-996a-add5ad092cc2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7bad6fbd9229547318a060f08eeb102b21cda9bb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62470893"
---
# <a name="dbosysalerts-transact-sql"></a>dbo.sysalerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada alerta. Una alerta es un mensaje enviado como respuesta a un evento. Una alerta puede reenviar mensajes fuera del entorno de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y puede consistir en un mensaje enviado por correo electrónico o a un buscapersonas. Una alerta también puede generar una tarea.  Esta tabla se almacena en el **msdb** base de datos.
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. de la alerta.|  
|**Nombre**|**sysname**|Nombre de la alerta.|  
|**event_source**|**nvarchar(100)**|Origen del evento: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**event_category_id**|**int**|Reservado para uso futuro.|  
|**event_id**|**int**|Reservado para uso futuro.|  
|**message_id**|**int**|Definido por el usuario Id. de mensaje o una referencia a **sysmessages** mensaje que desencadena esta alerta.|  
|**severity**|**int**|Gravedad que desencadena esta alerta.|  
|**enabled**|**tinyint**|Estado de la alerta:<br /><br /> **0** = disabled.<br /><br /> **1** = habilitado.|  
|**delay_between_responses**|**int**|Intervalo de espera, en segundos, entre las notificaciones de esta alerta.|  
|**last_occurrence_date**|**int**|Última repetición (fecha) de la alerta.|  
|**last_occurrence_time**|**int**|Última repeticiónn (hora) de la alerta.|  
|**last_response_date**|**int**|Última notificación (fecha) de la alerta.|  
|**last_response_time**|**int**|Última notificación (hora) de la alerta.|  
|**notification_message**|**nvarchar(512)**|Información adicional enviada con la alerta.|  
|**include_event_description**|**tinyint**|Máscara de bits que representa si la descripción del evento se envía por correo electrónico, buscapersonas o Net send. Consulte el gráfico siguiente para los valores.|  
|**database_name**|**nvarchar(512)**|Base de datos en la que se debe producir el evento para que se desencadene esta alerta.|  
|**event_description_keyword**|**nvarchar(100)**|Patrón al que se debe ajustar el error para que se desencadene la alerta.|  
|**occurrence_count**|**int**|Número de repeticiones de esta alerta.|  
|**count_reset_date**|**int**|Número de días (fecha) se restablecerá a **0**.|  
|**count_reset_time**|**int**|Número de horas se restablecerá a **0**.|  
|**job_id**|**uniqueidentifier**|Id. de la tarea ejecutada cuando se produce esta alerta.|  
|**has_notification**|**int**|Número de operadores que reciben notificación por correo electrónico cuando se produce la alerta.|  
|**flags**|**int**|Reservado.|  
|**performance_condition**|**nvarchar(512)**|Reservado.|  
|**category_id**|**int**|Reservado.|  
  
 ## <a name="remarks"></a>Comentarios

En la tabla siguiente se muestra los valores para la máscara de bits include_event_description. Dbo.sysalerts devuelve el valor decimal. 

|Decimal | binary | Significado |
|------|------|------|
|0 |0000 |ningún mensaje |
|1 |0001 |Correo electrónico |
|2 |0010 |buscapersonas |
|3 |0011 |elemento de paginación y el correo electrónico |
|4 |0100 |Net send |
|5 |0101 |Correo electrónico y net send |
|6 |0110 |Buscapersonas y net send |
|7 |0111 |Correo electrónico, buscapersonas y net send |
  
