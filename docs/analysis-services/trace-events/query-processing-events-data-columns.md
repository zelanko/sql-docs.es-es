---
title: Columnas de datos de eventos de procesamiento de consultas | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 81a522bd-440d-406c-a524-3af44a3af101
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0fafade22e12b14c1e11aab4a44ce65433d2a158
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="query-processing-events-data-columns"></a>Columnas de datos de los eventos de procesamiento de consultas
  La categoría de eventos Eventos de procesamiento de consultas tiene las siguientes clases de eventos:  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|70|Query Cube Begin|Inicio de consulta del cubo.|  
|71|Query Cube End|Final de consulta del cubo.|  
|72|Calculate Non Empty Begin|Inicio de calcular no vacío.|  
|73|Calculate Non Empty Current|Calcular no vacío en curso.|  
|74|Calculate Non Empty End|Final de calcular no vacío.|  
|75|Serialize Results Begin|Inicio de serializar resultados.|  
|76|Serialize Results Current|Serializar resultados en curso.|  
|77|Serialize Results End|Final de serializar resultados.|  
|78|Execute MDX Script Begin|Inicio de ejecutar script MDX.|  
|79|Execute MDX Script Current|Ejecutar script MDX en curso. Obsoleto.|  
|80|Execute MDX Script End|Final de ejecutar script MDX.|  
|81|Query Dimension|Consultar dimensión.|  
|11|Query Subcube|Consulta de subcubo para optimización basada en el uso.|  
|12|Query Subcube Verbose|Consulta de subcubo con información detallada. Este evento puede tener un impacto negativo en el rendimiento cuando está activado.|  
|60|Get Data From Aggregation|Responde a la consulta obteniendo datos de agregación. Este evento puede tener un impacto negativo en el rendimiento cuando está activado.|  
|61|Get Data From Cache|Responde a la consulta obteniendo datos de una de las memorias caché. Este evento puede tener un impacto negativo en el rendimiento cuando está activado.|  
|82|VertiPaq SE Query Begin|Consulta de VertiPaq SE.|  
|83|VertiPaq SE Query End|Consulta de VertiPaq SE.|  
|84|Resource Usage|Lecturas, escrituras y uso de cpu de los informes al finalizar los comandos y las consultas.|  
|85|VertiPaq SE Query Cache Match|Uso de la caché de consultas de VertiPaq SE.|  
|98|Direct Query Begin|Inicio de la consulta directa.|  
|99|Direct Query End|Final de la consulta directa.|  
  
 En las siguientes tablas se muestran las columnas de datos de cada una de estas clases de eventos.  
  
## <a name="query-cube-begin"></a>Query Cube Begin  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="query-cube-end"></a>Query Cube End  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="calculate-non-empty-begin"></a>Calculate Non Empty Begin  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="calculate-non-empty-current"></a>Calculate Non Empty Current  
  
|||||  
|-|-|-|-|  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|Event Subclass proporciona información adicional sobre cada clase de evento:<br /><br /> 1: Get Data<br /><br /> 2: Process Calculated Members<br /><br /> 3: Post Order|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="calculate-non-empty-end"></a>Calculate Non Empty End  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="serialize-results-begin"></a>Serialize Results Begin  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="serialize-results-current"></a>Serialize Results Current  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: Serialize Axes<br /><br /> 2: Serialize Cells<br /><br /> 3: Serialize SQL Rowset<br /><br /> 4: Serialize Flattened Rowset|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="serialize-results-end"></a>Serialize Results End  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="execute-mdx-script-begin"></a>Execute MDX Script Begin  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|Event Subclass proporciona información adicional sobre cada clase de evento:<br /><br /> 1: MDX Script<br /><br /> 2: MDX Script Command|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="execute-mdx-script-current"></a>Execute MDX Script Current  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="execute-mdx-script-end"></a>Execute MDX Script End  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|Event Subclass proporciona información adicional sobre cada clase de evento:<br /><br /> 1: MDX Script<br /><br /> 2: MDX Script Command|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="query-dimension"></a>Query Dimension  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: Cache data<br /><br /> 2: Non-cache data|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="query-subcube"></a>Query Subcube  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|Event Subclass proporciona información adicional sobre cada clase de evento:<br /><br /> 1: Cache data<br /><br /> 2: Non-cache data<br /><br /> 3: Internal data<br /><br /> 4: SQL data<br /><br /> 11: Measure Group Structural Change<br /><br /> 12: Measure Group Deletion|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="query-subcube-verbose"></a>Query Subcube Verbose  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|Event Subclass proporciona información adicional sobre cada clase de evento:<br /><br /> 21: Cache data<br /><br /> 22: Non-cache data<br /><br /> 23: Internal data<br /><br /> 24: SQL data|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="get-data-from-aggregation"></a>Get Data From Aggregation  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="get-data-from-cache"></a>Get Data From Cache  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 1: Get data from measure group cache<br /><br /> 2: Get data from flat cache<br /><br /> 3: Get data from calculation cache<br /><br /> 4: Get data from persisted cache|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="vertipaq-se-query-begin"></a>VertiPaq SE Query Begin  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|Event Subclass proporciona información adicional sobre cada clase de evento:<br /><br /> 0: VertiPaq Scan<br /><br /> 1: Tabular Query<br /><br /> 2: User Hierarchy Processing Query<br /><br /> 10: VertiPaq Scan internal<br /><br /> 11: Tabular Query internal<br /><br /> 12: User Hierarchy Processing Query internal|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ObjectReference|15|8|Referencia al objeto. Codificado como XML para todos los elementos primarios, usando etiquetas para describir el objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="vertipaq-se-query-end"></a>VertiPaq SE Query End  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|EventSubclass proporciona información adicional sobre cada clase de eventos.<br /><br /> 0: VertiPaq Scan<br /><br /> 1: Tabular Query<br /><br /> 10: VertiPaq Scan internal<br /><br /> 11: Tabular Query internal|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|ProgressTotal|9|1|Total del progreso.|  
|IntegerData|10|1|Datos enteros.|  
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
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="resource-usage"></a>Resource Usage  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|ClientProcessID|36|1|Identificador del proceso de la aplicación cliente.|  
|ApplicationName|37|8|Nombre de la aplicación cliente que ha creado la conexión con el servidor. Esta columna se rellena con los valores que pasa la aplicación, en lugar de con el nombre que se muestra para el programa.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="vertipaq-se-query-cache-match"></a>VertiPaq SE Query Cache Match  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|EventSubclass|1|1|Event Subclass proporciona información adicional sobre cada clase de evento:<br /><br /> 0: VertiPaq Cache exact match|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|JobID|7|1|Identificador del trabajo para el progreso.|  
|SessionType|8|8|Tipo de la sesión (qué entidad desencadenó la operación).|  
|ObjectID|11|8|Identificador del objeto (tenga en cuenta que es una cadena).|  
|ObjectType|12|1|Tipo de objeto.|  
|ObjectName|13|8|Nombre del objeto.|  
|ObjectPath|14|8|Ruta del objeto. Lista separada por comas de elementos primarios, empezando por el elemento primario del objeto.|  
|ObjectReference|15|8|Referencia al objeto. Codificado como XML para todos los elementos primarios, usando etiquetas para describir el objeto.|  
|ConnectionID|25|1|Identificador único de la conexión.|  
|DatabaseName|28|8|Nombre de la base de datos en la que se ejecuta la instrucción del usuario.|  
|NTUserName|32|8|Nombre del usuario de Windows.|  
|NTDomainName|33|8|Dominio de Windows al que pertenece el usuario.|  
|SessionID|39|8|GUID de la sesión.|  
|NTCanonicalUserName|40|8|Nombre del usuario en formato canónico. Por ejemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="direct-query-begin"></a>Direct Query Begin  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
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
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="direct-query-end"></a>Direct Query End  
  
|**Nombre de la columna**|**Identificador de la columna**|**Tipo de columna**|**Descripción de la columna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|EventClass se usa para clasificar los eventos.|  
|CurrentTime|2|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|StartTime|3|5|Hora a la que se inició el evento, si está disponible. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|EndTime|4|5|Hora a la que finalizó el evento. Esta columna no se llena para las clases de eventos de inicio, como SQL:BatchStarting o SP:Starting. Para filtrar, los formatos esperados son "AAAA-MM-DD" y "AAAA-MM-DD HH:MM:SS".|  
|Duración|5|2|Tiempo (en milisegundos) de duración del evento.|  
|CPUTime|6|2|Cantidad de tiempo de CPU (en milisegundos) que utiliza el evento.|  
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
|SPID|41|1|Identificador de proceso de servidor. Identifica de forma única una sesión de usuario. Se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|TextData|42|9|Datos de texto asociados al evento.|  
|ServerName|43|8|Nombre del servidor que produce el evento.|  
  
## <a name="see-also"></a>Vea también  
 [Procesamiento de consultas (categoría de eventos)](../../analysis-services/trace-events/query-processing-events-category.md)  
  
  
