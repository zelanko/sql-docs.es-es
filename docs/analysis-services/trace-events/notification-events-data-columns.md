---
title: Columnas de datos de eventos de notificación | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Notification Events event category
ms.assetid: 0ecf06da-1586-415a-9da8-60d4c634f030
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8d825bcc7fcdc548275cb46632229791855c275e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="notification-events-data-columns"></a>Columnas de datos de eventos de notificación
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Los eventos de notificación son aquéllos no provocados directamente por los usuarios de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Por ejemplo, las notificaciones tienen lugar porque los usuarios actualizan tablas subyacentes para el almacenamiento automático en la caché.  
  
 La categoría de eventos Eventos de notificación tiene la siguiente clase de eventos:  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|39|Notification|Evento de notificación.|  
|40|User Defined|Evento definido por el usuario.|  
  
 En la siguiente tabla se enumeran las columnas de datos de la clase de eventos.  
  
## <a name="notification"></a>Notification  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> Se definen los siguientes pares **Sub Class Id**:<br />                      **Sub Class Name** :<br /><br /> 0: Proactive Caching Begin<br /><br /> 1: Proactive Caching End<br /><br /> 2: Flight Recorder Started<br /><br /> 3: Flight Recorder Stopped<br /><br /> 4: Configuration Properties Updated<br /><br /> 5: SQL Trace<br /><br /> 6: Object Created<br /><br /> 7: Object Deleted<br /><br /> 8: Object Altered<br /><br /> 9: Proactive Caching Polling Begin<br /><br /> 10: Proactive Caching Polling End<br /><br /> 11: Flight Recorder Snapshot Begin<br /><br /> 12: Flight Recorder Snapshot End<br /><br /> 13: Proactive Caching: notifiable object updated<br /><br /> 14: Lazy Processing: start processing<br /><br /> 15: Lazy Processing: processing complete<br /><br /> 16: SessionOpened Event Begin<br /><br /> 17: SessionOpened Event End<br /><br /> 18: SessionClosing Event Begin<br /><br /> 19: SessionClosing Event End<br /><br /> 20: CubeOpened Event Begin<br /><br /> 21: CubeOpened Event End<br /><br /> 22: CubeClosing Event Begin<br /><br /> 23: CubeClosing Event End<br /><br /> 24: Transaction abort requested|  
|CurrentTime|2|5|Contiene la hora actual del evento de notificación, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Contiene la hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Contiene el tiempo (en milisegundos) que duró el evento.|  
|IntegerData|10|1|Contiene los datos enteros asociados al evento de notificación. Cuando la columna EventSubclass es 8, los valores son:<br /><br /> 1 = Creado<br /><br /> 2 = Eliminado<br /><br /> 3 = Propiedades del objeto cambiadas<br /><br /> 4 = Propiedades cambiadas de los elementos secundarios del objeto<br /><br /> 6 = Elementos secundarios agregados<br /><br /> 7 = Elementos secundarios eliminados<br /><br /> 8 = Objeto totalmente procesado<br /><br /> 9 = Objeto parcialmente procesado<br /><br /> 10 = Objeto no procesado<br /><br /> 11 = Objeto totalmente optimizado<br /><br /> 12 = Objeto parcialmente optimizado<br /><br /> 13 = Objeto no optimizado|  
|ObjectID|11|8|Contiene el identificador de objeto (valor de cadena) para el cual se ha emitido esta notificación.|  
|ObjectType|12|1|Contiene el tipo de objeto asociado al evento de notificación.|  
|ObjectName|13|8|Contiene el nombre de objeto asociado al evento de notificación.|  
|ObjectPath|14|8|Contiene la ruta de objeto asociada al evento de notificación. La ruta de acceso es una lista separada por comas de elementos primarios que empieza por el elemento primario del objeto.|  
|ObjectReference|15|8|Contiene la referencia de objeto del evento final del informe de progreso. La referencia de objeto está codificada como XML por todos los elementos primarios mediante etiquetas para describir el objeto.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de notificación.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que se ha producido el evento de notificación.|  
|NTUserName|32|8|Contiene el nombre de usuario de Windows asociado al evento de notificación.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento de notificación.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento de notificación. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica unívocamente la sesión de usuario asociada al evento de notificación. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados al evento de notificación.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de notificación.|  
|RequestProperties|45|9|Contiene las propiedades de las solicitudes de XMLA.|  
  
## <a name="user-defined"></a>User Defined  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|Subclase de evento específica del usuario que proporciona información adicional sobre cada clase de eventos.|  
|CurrentTime|2|5|Contiene la hora actual del evento de notificación, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|IntegerData|10|1|Información sobre el evento específica del usuario.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de notificación.|  
|DatabaseName|28|8|Contiene el nombre de la base de datos en la que se ha producido el evento de notificación.|  
|NTUserName|32|8|Contiene el nombre de usuario de Windows asociado al evento de notificación.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento de notificación.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento de notificación. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica unívocamente la sesión de usuario asociada al evento de notificación. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados al evento de notificación.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de notificación.|  
  
## <a name="see-also"></a>Vea también  
 [Categoría de eventos de eventos de notificación](../../analysis-services/trace-events/notification-events-event-category.md)  
  
  
