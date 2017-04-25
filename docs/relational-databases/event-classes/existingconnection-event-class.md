---
title: Clase de eventos ExistingConnection | Microsoft Docs
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
- ExistingConnection event class
ms.assetid: 3eae548f-61af-4f91-ae6f-af5c8a152543
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d50c35d1e3f67d804cc80e6d7f442a12cb9942e5
ms.lasthandoff: 04/11/2017

---
# <a name="existingconnection-event-class"></a>ExistingConnection, clase de eventos
  La clase de eventos ExistingConnection indica las propiedades de las conexiones de usuario existentes al iniciar el seguimiento. El servidor genera un evento ExistingConnection para cada conexión de usuario existente.  
  
## <a name="existing-connection-event-class-data-columns"></a>Columnas de datos de la clase de eventos Existing Connection  
  
|Nombre de columna de datos|Tipo de datos|Descripción|Identificador de columna|Filtrable|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|Nombre de la aplicación cliente que ha creado la conexión a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|10|Sí|  
|BinaryData|**imagen**|Volcado binario de las marcas de opción, como la configuración del nivel de sesión, incluidos valores ANSI NULL, el relleno ANSI, el cierre del cursor al confirmar, la concatenación de valores NULL y los identificadores entre comillas.|2|Sí|  
|ClientProcessID|**int**|Identificador que el equipo host asigna al proceso en el que se ejecuta la aplicación cliente. Esta columna de datos se rellena si el cliente proporciona el identificador de proceso del cliente.|9|Sí|  
|DatabaseID|**int**|El Id. de la base de datos actual de la conexión de usuario. Identificador de la base de datos especificada mediante la instrucción USE *database* o la base de datos predeterminada si no se emite la instrucción USE *database* para una determinada instancia. Determina el valor de una base de datos mediante la función DB_ID.|3|Sí|  
|DatabaseName|**nvarchar**|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|35|Sí|  
|EventClass|**int**|Tipo de evento = 17.|27|No|  
|EventSequence|**int**|La secuencia de este evento dentro de este seguimiento.|51|No|  
|GroupID|**int**|Id. del grupo de carga de trabajo donde se activa el evento de Seguimiento de SQL.|66|Sí|  
|HostName|**nvarchar**|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host. Para determinar el nombre del host, utilice la función HOST_NAME.|8|Sí|  
|IntegerData|**int**|El tamaño de paquete de red que se utiliza para la conexión.|25|Sí|  
|IsSystem|**int**|Indica si el evento ha ocurrido en un proceso del sistema o en un proceso de usuario. 1 = sistema, NULL = usuario. Siempre es NULL para este evento.|60|Sí|  
|LoginName|**nvarchar**|Nombre del inicio de sesión del usuario (inicio de sesión de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o credenciales de inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con el formato DOMINIO\nombreDeUsuario).|11|Sí|  
|LoginSid|**imagen**|SID (número de identificación de seguridad) del usuario que ha iniciado la sesión. Puede buscar esta información en la vista de catálogo sys.server_principals. Cada SID es único para cada inicio de sesión en el servidor.|41|Sí|  
|NTDomainName|**nvarchar**|Dominio de Windows al que pertenece el usuario.|7|Sí|  
|NTUserName|**nvarchar**|Nombre del usuario de Windows.|6|Sí|  
|IdSolicitud|**int**|Id. de la solicitud que contiene la instrucción.|49|Sí|  
|ServerName|**nvarchar**|Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la que se realiza un seguimiento.|26|No|  
|SessionLoginName|**nvarchar**|Nombre de inicio de sesión del usuario que originó la sesión. Por ejemplo, si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando inicioDeSesión1 y ejecuta una instrucción como inicioDeSesión2, SessionLoginName muestra inicioDeSesión1 y LoginName muestra inicioDeSesión2. En esta columna se muestran los inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows.|64|Sí|  
|SPID|**int**|Identificador de la sesión en la que se produjo el evento.|12|Sí|  
|StartTime|**datetime**|Hora a la que el usuario ha abierto esta conexión (hora de inicio de sesión).|14|Sí|  
|TextData|**ntext**|Establece las opciones específicas para la conexión.|1|Sí|  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Audit Login (clase de eventos)](../../relational-databases/event-classes/audit-login-event-class.md)  
  
  
