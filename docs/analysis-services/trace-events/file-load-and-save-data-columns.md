---
title: Cargar y guardar las columnas de datos de archivos | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 0101e809-d6ea-4d0c-95ec-65dd77acf665
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2e711c51d3a6d8cae4fc437c9b9f6f0bc758c899
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="file-load-and-save-data-columns"></a>Columnas de datos de la categoría de eventos Cargar y guardar archivos
  La categoría de eventos Cargar y guardar archivos tiene la siguiente clase de eventos:  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|90|Inicio de la carga de archivo.|Inicio de la carga de archivo.|  
|91|Final de la carga de archivo.|Final de la carga de archivo.|  
|92|Inicio del guardado de archivo.|Inicio del guardado de archivo.|  
|93|Final del guardado de archivo.|Final del guardado de archivo.|  
|94|Inicio de PageOut.|Inicio de PageOut.|  
|95|Final de PageOut.|Final de PageOut.|  
|96|Inicio de PageIn.|Inicio de PageIn.|  
|97|Final de PageIn.|Final de PageIn.|  
  
 En la siguiente tabla se muestran las columnas de datos de esta clase de eventos.  
  
## <a name="file-load-begin"></a>Inicio de la carga de archivo.  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|SessionID|39|8|GUID de la sesión.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="file-load-end"></a>Final de la carga de archivo.  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|IntegerData|10|1|Datos enteros.|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|Severity|22|1|Nivel de gravedad de una excepción.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|Error|24|1|Número de error de un evento dado.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|SessionID|39|8|GUID de la sesión.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="file-save-begin"></a>Inicio del guardado de archivo.  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|SessionID|39|8|GUID de la sesión.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="file-save-end"></a>Final del guardado de archivo.  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|IntegerData|10|1|Datos enteros.|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|Severity|22|1|Nivel de gravedad de una excepción.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|Error|24|1|Número de error de un evento dado.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|SessionID|39|8|GUID de la sesión.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="pageout-begin"></a>Inicio de PageOut.  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|SessionID|39|8|GUID de la sesión.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="pageout-end"></a>Final de PageOut.  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|IntegerData|10|1|Datos enteros.|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|Severity|22|1|Nivel de gravedad de una excepción.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|Error|24|1|Número de error de un evento dado.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|SessionID|39|8|GUID de la sesión.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="pagein-begin"></a>Inicio de PageIn.  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|SessionID|39|8|GUID de la sesión.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="pagein-end"></a>Final de PageIn.  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|IntegerData|10|1|Datos enteros.|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|Severity|22|1|Nivel de gravedad de una excepción.|  
|Correcto|23|1|1 = correcto. 0 = error (por ejemplo, 1 significa que se ha comprobado un permiso correctamente y 0 significa que se ha producido un error en la comprobación).|  
|Error|24|1|Número de error de un evento dado.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|SessionID|39|8|GUID de la sesión.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="see-also"></a>Vea también  
 [Categoría de eventos Cargar y guardar archivos](../../analysis-services/trace-events/file-load-and-save-event-category.md)  
  
  
