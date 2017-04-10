---
title: "Columnas de datos de Auditor&#237;a de seguridad | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
helpviewer_keywords: 
  - "auditoría de seguridad, categoría de eventos [SQL Server]"
ms.assetid: fac1a7f9-5961-4f4b-bb04-847616b505d7
caps.latest.revision: 36
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 36
---
# Columnas de datos de Auditor&#237;a de seguridad
  La categoría de eventos Auditoría de seguridad tiene las siguientes clases de eventos:  
  
||||  
|-|-|-|  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|1|Audit Login|Recopila todos los nuevos eventos de conexión desde que se inició el seguimiento, como cuando un cliente solicita una conexión a un servidor que ejecuta una instancia de SQL Server.|  
|2|Audit Logout|Recopila todos los nuevos eventos de desconexión desde que se inició el seguimiento, como cuando un cliente envía un comando de desconexión.|  
|4|Audit Server Starts And Stops|Registra las actividades de cierre, inicio y pausa de los servicios.|  
|18|Audit Object Permission Event|Registra los cambios de permiso de un objeto.|  
|19|Audit Admin Operations Event|Registra las operaciones de copia de seguridad/restauración/sincronización/operaciones de adjuntar o separar/carga de imágenes/guardado de imágenes realizadas en el servidor.|  
  
 En las siguientes tablas se muestran las columnas de datos de cada una de estas clases de eventos.  
  
## Audit Login  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Severity|22|1|Nivel de gravedad de una excepción.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|Error|24|1|Número de error de un evento dado.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|ClientHostName|35|8|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## Audit Logout  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|ClientHostName|35|8|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## Audit Server Starts And Stops  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: Instance Shutdown<br /><br /> 2: Instance Started<br /><br /> 3: Instance Paused<br /><br /> 4: Instance Continued|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Severity|22|1|Nivel de gravedad de una excepción.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|Error|24|1|Número de error de un evento dado.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## Audit Object Permission Event  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ObjectReference|15|8|Referencia al objeto. Codificado como XML para todos los elementos primarios, usando etiquetas para describir el objeto.|  
|Severity|22|1|Nivel de gravedad de una excepción.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|Error|24|1|Número de error de un evento dado.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|ClientHostName|35|8|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## Audit Admin Operations Event  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: **Backup**<br /><br /> 2: **Restore**<br /><br /> 3: **Synchronize**<br /><br /> 4: **Detach**<br /><br /> 5: **Attach**<br /><br /> 6: **ImageLoad**<br /><br /> 7: **ImageSave**|  
|Severity|22|1|Nivel de gravedad de una excepción.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|Error|24|1|Número de error de un evento dado.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|ClientHostName|35|8|Nombre del equipo en el que se está ejecutando el cliente. Esta columna de datos se rellena si el cliente proporciona el nombre del host.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## Vea también  
 [Auditoría de seguridad (categoría de eventos)](../../analysis-services/trace-events/security-audit-event-category.md)  
  
  