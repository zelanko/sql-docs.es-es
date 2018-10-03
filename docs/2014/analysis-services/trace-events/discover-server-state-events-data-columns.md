---
title: Columnas de datos de eventos de estado del servidor de detección | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Discover Server State event category
ms.assetid: fbacb187-a4d1-4aa4-be3b-3ddd175f9e19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7076a131acf9c3237c653e32ad238df20bca896
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104605"
---
# <a name="discover-server-state-events-data-columns"></a>Columnas de datos de eventos de detección de estado del servidor
  La categoría de eventos Detección de estado del servidor tiene las clases de eventos siguientes:  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|33|Server State Discover Begin|Inicio de la detección del estado del servidor.|  
|34|Server State Discover Data|Contenido de la respuesta de detección del estado del servidor.|  
|35|Server State Discover End|Fin de la detección del estado del servidor.|  
  
 En las siguientes tablas se muestran las columnas de datos de cada una de estas clases de eventos.  
  
## <a name="server-state-discover-begin-classdata-columns"></a>Columnas de datos de la clase Server State Discover Begin  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|Contiene la hora actual del evento de detección de estado del servidor, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de detección de estado del servidor.|  
|NTUserName|32|8|Contiene la cuenta de usuario de Windows asociada al evento de detección de estado del servidor.|  
|NTDomainName|33|8|Contiene la cuenta de usuario de dominio de Windows asociada al evento de detección de estado del servidor.|  
|ClientProcessID|36|1|Contiene el identificador de proceso de la aplicación cliente que ha creado la conexión con el servidor.|  
|ApplicationName|37|8|Contiene el nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento de detección de estado del servidor.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento de detección de estado del servidor. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica de forma única la sesión de usuario asociada al evento de detección de estado del servidor. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados al evento.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de detección de estado del servidor.|  
|RequestProperties|45|9|Contiene las propiedades de la solicitud de XMLA actual.|  
  
## <a name="server-state-discover-data-classdata-columns"></a>Columnas de datos de la clase Server State Discover Data  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|Contiene la hora actual del evento de detección de estado del servidor, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de detección de estado del servidor.|  
|SessionID|39|8|Contiene el identificador de sesión asociado al evento de detección de estado del servidor.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica de forma única la sesión de usuario asociada al evento de detección de estado del servidor. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados a la respuesta del servidor con respecto a la solicitud de detección.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de detección de estado del servidor.|  
  
## <a name="server-state-discover-end-classdata-columns"></a>Columnas de datos de la clase Server State Discover End  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: **DISCOVER_CONNECTIONS**<br /><br /> 2: **DISCOVER_SESSIONS**<br /><br /> 3: **DISCOVER_TRANSACTIONS**<br /><br /> 6: **DISCOVER_DB_CONNECTIONS**<br /><br /> 7: **DISCOVER_JOBS**<br /><br /> 8: **DISCOVER_LOCKS**<br /><br /> 12: **DISCOVER_PERFORMANCE_COUNTERS**<br /><br /> 13: **DISCOVER_MEMORYUSAGE**<br /><br /> 14: **DISCOVER_JOB_PROGRESS**<br /><br /> 15: **DISCOVER_MEMORYGRANT**|  
|CurrentTime|2|5|Contiene la hora actual del evento de detección de estado del servidor, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Contiene la hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Contiene la hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duration|5|2|Contiene el tiempo (en milisegundos) que duró el evento.|  
|CPUTime|6|2|Contiene el intervalo de tiempo de CPU (en milisegundos) utilizado por el evento de detección de estado del servidor.|  
|ConnectionID|25|1|Contiene el identificador único de conexión asociado al evento de detección de estado del servidor.|  
|NTUserName|32|8|Contiene la cuenta de usuario de Windows asociada al evento de detección de estado del servidor.|  
|NTDomainName|33|8|Contiene la cuenta de usuario de dominio de Windows asociada al evento de detección de estado del servidor.|  
|ClientProcessID|36|1|Contiene el identificador de proceso de la aplicación cliente que inició la solicitud de XMLA.|  
|ApplicationName|37|8|Contiene el nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|Contiene la cuenta de usuario de dominio de Windows asociada al evento de detección de estado del servidor.|  
|NTCanonicalUserName|40|8|Contiene el nombre de usuario de Windows asociado al evento de detección de estado del servidor. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contiene el identificador de proceso de servidor (SPID) que identifica de forma única la sesión de usuario asociada al evento de detección de estado del servidor. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Contiene los datos de texto asociados a la respuesta del servidor con respecto a la solicitud de detección.|  
|ServerName|43|8|Contiene el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de detección de estado del servidor.|  
  
## <a name="see-also"></a>Vea también  
 [Categoría de eventos Detección de estado del servidor](discover-server-state-event-category.md)  
  
  
