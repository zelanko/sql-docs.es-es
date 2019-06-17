---
title: Clase de eventos Broker:Message Undeliverable | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Message Drop event class
- Broker:Message Undeliverable event class
ms.assetid: f532b7c9-ca34-4bac-8dc3-53f9895fd6af
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1aadd84d42f797026323023b0cf5be27d01d693
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62663975"
---
# <a name="brokermessage-undeliverable-event-class"></a>Clase de eventos Broker:Message Undeliverable
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera un evento **Broker:Message Undeliverable** cuando Service Broker no puede retener un mensaje recibido que debería haberse entregado a un servicio en esta instancia. Para saber qué mensajes se deberían haber reenviado, vea [Broker:Forwarded Message Dropped (clase de eventos)](broker-forwarded-message-dropped-event-class.md).  
  
## <a name="brokermessage-undeliverable-event-class-data-columns"></a>Columnas de datos de la clase de eventos Broker:Message Undeliverable  
  
|Columna de datos|Tipo|Descripción|Número de columna|Filtrable|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**Application Name**|`nvarchar`|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|**BigintData1**|`bigint`|El número de secuencia del mensaje no apto para entrega.|52|No|  
|**BigintData2**|`bigint`|Número de secuencia del último mensaje que se confirmó correctamente.|53|Sin|  
|**ClientProcessID**|`int`|Id. que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona su identificador de proceso.|9|Sí|  
|**DatabaseID**|`int`|Identificador de la base de datos especificada mediante la instrucción USE *baseDeDatos* o identificador de la base de datos predeterminada si no se emite la instrucción USE *baseDeDatos* para una instancia determinada. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] muestra el nombre de la base de datos si se captura la columna de datos **ServerName** en el seguimiento y el servidor está disponible. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|**Error**|`int`|Número de id. del mensaje en **sys.messages** para el texto del evento.|31|Sin|  
|**EventClass**|`int`|Tipo de clase de eventos capturado. Siempre es **160** para **Broker:MessageUndeliverable**.|27|Sin|  
|**EventSequence**|`int`|Número de secuencia de este evento.|51|Sin|  
|**EventSubClass**|`nvarchar`|Indica si el mensaje no apto para entrega era un mensaje en secuencia. Uno de dos valores:<br /><br /> **Mensaje en secuencia**. El mensaje no apto para entrega era un mensaje en secuencia.<br /><br /> **Mensaje sin secuencia**. El mensaje no apto para entrega no era un mensaje en secuencia.|21|Sí|  
|**GUID**|`uniqueidentifier`|El Id. de la conversación a la que pertenece el mensaje no apto para entrega. Este identificador se transmite como parte del mensaje y lo comparten ambas partes de la conversación.|54|Sin|  
|**HostName**|`nvarchar`|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|**IntegerData**|`int`|El número de fragmento del mensaje no apto para entrega.|25|No|  
|**IntegerData2**|`int`|El número de fragmento del mensaje que reconoció el mensaje no apto para entrega.|55|No|  
|**IsSystem**|`int`|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, 0 = usuario.|60|Sin|  
|**LoginName**|`nvarchar`|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de Windows en formato DOMINIO\nombreDeUsuario).|11|Sin|  
|**LoginSid**|`image`|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|**NTDomainName**|`nvarchar`|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|**NTUserName**|`nvarchar`|Nombre del usuario al que pertenece la conexión que generó este evento.|6|Sí|  
|**ObjectName**|`nvarchar`|Identificador de conversación del diálogo.|34|Sin|  
|**RoleName**|`nvarchar`|Rol del identificador de conversación. Es **initiator** o **target**.|38|Sin|  
|**ServerName**|`nvarchar`|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|**Severity**|`int`|Número de nivel de gravedad para el texto del evento.|29|Sin|  
|**SPID**|`int`|Identificador de proceso del servidor que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asigna al proceso asociado al cliente.|12|Sí|  
|**StartTime**|`datetime`|Hora a la que se inició el evento, si está disponible.|14|Sí|  
|**Estado**|`int`|Indica la ubicación en el código fuente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que produjo el evento. Cada lugar en el que se puede producir este evento tiene un código de estado diferente. Un ingeniero de soporte técnico de Microsoft puede utilizar este código de estado para localizar la ubicación en la que se generó el evento.|30|Sin|  
|**TextData**|`ntext`|La razón por la que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pudo entregar el mensaje.|1|Sí|  
|**TransactionID**|`bigint`|Identificador de la transacción asignado por el sistema.|4|No|  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
