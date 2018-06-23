---
title: Columnas de datos de eventos de sesión | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Session Events event category
ms.assetid: 35853451-6768-4a02-8b8f-81a8ae37a333
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 555a9eb950a2dcd70935964a8a6f3237f8abb76d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113676"
---
# <a name="session-events-data-columns"></a>Columnas de datos de Eventos de sesión
  La categoría de eventos Eventos de sesión tiene la siguiente clase de eventos:  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|Conexión existente del usuario.|  
|42|Existing Session|Sesión existente.|  
|43|Session Initialize|Sesión inicializada.|  
  
 En la siguiente tabla se muestran las columnas de datos de esta clase de eventos.  
  
## <a name="existing-connection"></a>Existing Connection  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|ClientHostName|35|8|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="existing-session"></a>Existing Session  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duration|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|ClientHostName|35|8|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
|RequestProperties|45|9|Propiedades de la solicitud XMLA.|  
  
## <a name="session-initialize"></a>Session Initialize  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|ClientHostName|35|8|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
|RequestProperties|45|9|Propiedades de la solicitud XMLA.|  
  
## <a name="see-also"></a>Vea también  
 [Auditoría de seguridad (categoría de eventos)](security-audit-event-category.md)  
  
  