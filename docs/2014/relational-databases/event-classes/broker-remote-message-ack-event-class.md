---
title: Clase de eventos Broker:Remote Message Ack | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
topic_type:
- apiref
helpviewer_keywords:
- Broker:Remote Message Ack event class
ms.assetid: 3d67efe1-74b4-4633-b029-c6e05b19f4dc
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7bd0cef1327e32dd5a773c3e422ec546014a0ef1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112295"
---
# <a name="brokerremote-message-ack-event-class"></a>Broker:Remote Message Ack, clase de eventos
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento **Broker:Remote Message Ack** cuando [!INCLUDE[ssSB](../../includes/sssb-md.md)] envía o recibe un reconocimiento de mensaje.  
  
## <a name="brokerremote-message-ack-event-class-data-columns"></a>Columnas de datos de la clase de eventos Broker:Remote Message Ack  
  
|Columna de datos|Tipo|Descripción|Número de columna|Filtrable|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación en lugar de con el nombre mostrado del programa.|10|Sí|  
|**BigintData1**|**bigint**|Número de secuencia del mensaje que contiene el reconocimiento.|52|no|  
|**BigintData2**|**bigint**|Número de secuencia del mensaje que se va a reconocer.|53|no|  
|**ClientProcessID**|**int**|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|**DatabaseID**|**int**|Id. de la base de datos especificada por la instrucción USE *database* . Si no se emitió ninguna instrucción USE *database* para una instancia determinada, el identificador de la base de datos predeterminada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**EventClass**|**int**|Tipo de clase de eventos capturado. Es siempre **149** para **Broker:Message Ack**.|27|no|  
|**EventSequence**|**int**|Número de secuencia de este evento.|51|no|  
|**EventSubClass**|**nvarchar**|Tipo de subclase de evento, que proporciona más información acerca de cada clase de eventos. Esta columna puede incluir los valores siguientes:<br /><br /> **Mensaje de confirmación enviada**<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] se ha enviado un reconocimiento como parte de un mensaje en secuencia normal.<br /><br /> **Enviada la confirmación**<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] se ha enviado un reconocimiento fuera de un mensaje en secuencia normal.<br /><br /> **Mensaje de confirmación recibida**<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] se ha recibido un reconocimiento como parte de un mensaje en secuencia normal.<br /><br /> **Recibidas una confirmación**<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] se ha recibido un reconocimiento fuera de un mensaje en secuencia normal.|21|Sí|  
|**GUID**|**uniqueidentifier**|Id. de conversación del diálogo. Este identificador se transmite como parte del mensaje y lo comparten ambas partes de la conversación.|54|no|  
|**HonorBrokerPriority**|**Int**|Valor actual de la opción HONOR_BROKER_PRIORITY de la base de datos: 0 = OFF, 1 = ON.|32|Sí|  
|**HostName**|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|**IntegerData**|**int**|Número de fragmento del mensaje que contiene el reconocimiento.|25|no|  
|**IntegerData2**|**int**|Número de fragmento del mensaje que se va a reconocer.|55|no|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario.<br /><br /> 0 = usuario<br /><br /> 1 = sistema|60|no|  
|**LoginSid**|**imagen**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**NTDomainName**|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|**NTUserName**|**nvarchar**|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|**Prioridad**|**int**|Nivel de prioridad de la conversación.|5|Sí|  
|**RoleName**|**nvarchar**|Rol de la instancia que reconoce el mensaje. Es **initiator** o **target**.|38|no|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo seguimiento se realiza.|26|no|  
|**SPID**|**int**|Identificador de proceso del servidor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna al proceso relacionado con el cliente.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**StarvationElevation**|**int**|El mensaje se envió con una prioridad más alta que la prioridad configurada para la conversación: 0 = false, 1 = true.|33|Sí|  
|**TransactionID**|**bigint**|Identificador de la transacción asignado por el sistema.|4|no|  
  
  