---
title: Clase de eventos Broker:Message Classify | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4398085227952f30e4df7d54ac78c1aef1355173
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62664054"
---
# <a name="brokermessage-classify-event-class"></a>Broker:Message Classify, clase de eventos
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento **Broker:Message Classify** cuando Service Broker determina el enrutamiento para un mensaje.  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Columnas de datos de la clase de evento Broker:Message Classify  
  
|Columna de datos|Tipo de datos|Descripción|Número de columna|Filtrable|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|**ClientProcessID**|**int**|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|**DatabaseID**|**int**|Identificador de la base de datos especificada mediante la instrucción USE *baseDeDatos* o identificador de la base de datos predeterminada si no se emite la instrucción USE *baseDeDatos* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**EventClass**|**int**|Tipo de clase de eventos capturado. Es siempre **141** para **Broker:Message Classify**.|27|Sin|  
|**EventSequence**|**int**|Número de secuencia de este evento.|51|Sin|  
|**EventSubClass**|**nvarchar**|Tipo de subclase de evento que proporciona más información acerca de cada clase de evento. Esta columna puede incluir los valores siguientes:<br /><br /> **Local**: la ruta elegida tiene la dirección LOCAL.<br /><br /> **Remote**: la ruta elegida tiene una dirección diferente a LOCAL.<br /><br /> **Delayed**: el mensaje tiene demora porque el reenvío está deshabilitado o porque no hay ninguna ruta que coincida.|21|Sí|  
|**FileName**|**nvarchar**|Nombre del servicio al que se dirige el mensaje.|36|Sin|  
|**GUID**|**uniqueidentifier**|Id. de conversación del diálogo. Este identificador se transmite como parte del mensaje y lo comparten ambas partes de la conversación.|54|Sin|  
|**HostName**|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|No|  
|**LoginSid**|**image**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**NTDomainName**|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|**NTUserName**|**nvarchar**|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|**OwnerName**|**nvarchar**|Identificador de agente al que se dirige el mensaje.|37|Sin|  
|**RoleName**|**nvarchar**|Indica si el mensaje se recibió desde la red o si se originó en esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|38|No|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|Sin|  
|**SPID**|**int**|Identificador de proceso del servidor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna al proceso asociado al cliente.|12|Sí|  
|**Start Time**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**TargetUserName**|**nvarchar**|Dirección de red del siguiente agente de saltos.|39|Sin|  
|**TransactionID**|**bigint**|Identificador de la transacción asignado por el sistema.|4|Sin|  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
