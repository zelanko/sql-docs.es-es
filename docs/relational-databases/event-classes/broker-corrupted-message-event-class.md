---
title: Clase de eventos Broker:Corrupted Message | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Broker:Corrupted Message event class
ms.assetid: 084bf198-2138-438e-bdc7-4ff1e04300f7
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4e27bdd5ad90a537ea6562bfc730e4439b4a7616
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="brokercorrupted-message-event-class"></a>Broker:Corrupted Message, clase de eventos
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un evento **Broker:Corrupted Message** cuando Service Broker recibe un mensaje dañado.  
  
## <a name="brokercorrupted-message-event-class-data-columns"></a>Columnas de datos de la clase de eventos Broker:Corrupted Message  
  
|Columna de datos|Tipo|Descripción|Número de columna|Filtrable|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|**BigintData1**|**bigint**|Número de secuencia de este mensaje.|52|No|  
|**BinaryData**|**imagen**|Cuerpo del mensaje.|2|Sí|  
|**ClientProcessID**|**int**|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|**DatabaseID**|**int**|Identificador de la base de datos especificada mediante la instrucción USE *baseDeDatos* o identificador de la base de datos predeterminada si no se emite la instrucción USE *baseDeDatos* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**Error**|**int**|Número de id. del mensaje en **sys.messages** para el texto del evento.|31|No|  
|**EventClass**|**int**|Tipo de clase de eventos capturado. Es siempre **161** para **Broker:Corrupted Message**.|27|No|  
|**EventSequence**|**int**|Número de secuencia de este evento.|51|No|  
|**FileName**|**nvarchar**|Dirección de red del extremo remoto.|36|No|  
|**GUID**|**uniqueidentifier**|Id. de conversación que corresponde a la conversación a la que pertenece el mensaje dañado. Este identificador se transmite como parte del mensaje y lo comparten ambas partes de la conversación.|54|No|  
|**Host Name**|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|**IntegerData**|**int**|Número de fragmento de este mensaje.|25|Sí|  
|**IsSystem**|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|No|  
|**LoginSid**|**imagen**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**NTDomainName**|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|**NTUserName**|**nvarchar**|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|**ObjectName**|**nvarchar**|Nombre de servicio del otro lado de la conversación y cadena de conexión que la base de datos remota ha utilizado para conectarse a esta base de datos.|34|No|  
|**RoleName**|**nvarchar**|Rol del extremo que recibe este mensaje. Uno de los valores siguientes.<br /><br /> **iniciador**: el punto de conexión receptor es el iniciador de la conversación.<br /><br /> **destino**: el punto de conexión receptor es el destino de la conversación.|38|No|  
|**ServerName**|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|**Severity**|**int**|Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha quitado el mensaje debido a un error, gravedad de este error.|29|No|  
|**SPID**|**int**|Identificador de proceso del servidor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna al proceso asociado al cliente.|12|Sí|  
|**StartTime**|**datetime**|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**State**|**int**|Indica la ubicación en el código fuente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que produjo el evento. Cada lugar en el que se puede producir este evento tiene un código de estado diferente. Un ingeniero de soporte técnico de Microsoft puede utilizar este código de estado para buscar el lugar en que se produjo el evento.|30|No|  
|**TextData**|**ntext**|Descripción del daño detectado.|1|Sí|  
|**Transaction ID**|**bigint**|Identificador de la transacción asignado por el sistema.|4|No|  
  
 La columna **TextData** de este evento contiene texto que describe el problema con el mensaje.  
  
  
