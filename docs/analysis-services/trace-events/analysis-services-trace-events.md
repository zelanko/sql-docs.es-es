---
title: Eventos de seguimiento de Analysis Services | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 07e7f1e61d2675a46ab9dbb5aca574aeb76c1729
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="analysis-services-trace-events"></a>Eventos de seguimiento de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Puede seguir la actividad de una instancia de Microsoft SQL Server Analysis Services (SSAS) capturando y analizando los eventos de seguimiento generados por la instancia.  Los eventos de seguimiento están agrupados para que pueda encontrar más fácilmente aquellos que estén relacionados.  Cada uno de los eventos de seguimiento contiene un conjunto de datos sobre el evento; no todos los datos están relacionados con todos los eventos.  
  
 Los eventos de seguimiento se pueden iniciar y capturar mediante **[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]**(vea [Usar SQL Server Profiler para supervisar Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)) o se pueden iniciar mediante un comando XMLA como **Eventos extendidos de SQL Server** y analizarse posteriormente (vea [Supervisar Analysis Services con SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)).  
  
 En las tablas siguientes se describen las categorías de eventos y los eventos pertenecientes a cada una de ellas. Cada tabla contiene las columnas siguientes:  
  
**Identificador del evento**  
 Valor entero que identifica el tipo de evento. Este valor es útil cuando esté leyendo seguimientos convertidos en tablas o archivos XML para filtrar el tipo de evento.  
  
**Nombre del evento**  
 El nombre dado al evento en las aplicaciones cliente de Analysis Services.  
  
**Descripción del evento**  
 Breve descripción del evento.  
  
 **[Eventos de comandos (categoría de eventos)](../../analysis-services/trace-events/command-events-event-category.md)**  
  
 Colección de eventos para los comandos.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|15|Command Begin|Inicio del comando.|  
|16|Command End|Final del comando.|  
  
 **[Eventos de detección (categoría de eventos)](../../analysis-services/trace-events/discover-events-event-category.md)**  
  
 Colección de eventos para las solicitudes de detección.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|36|Discover Begin|Inicio de la solicitud de detección.|  
|38|Discover End|Fin de la solicitud de detección.|  
  
 **[Detección de estado del servidor (categoría de eventos)](../../analysis-services/trace-events/discover-server-state-event-category.md)**  
  
 Colección de eventos para detecciones de estado del servidor.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|33|Server State Discover Begin|Inicio de la detección del estado del servidor.|  
|34|Server State Discover Data|Contenido de la respuesta de detección del estado del servidor.|  
|35|Server State Discover End|Fin de la detección del estado del servidor.|  
  
 **[Errores y advertencias (categoría de eventos)](../../analysis-services/trace-events/errors-and-warnings-event-category.md)**  
  
 Colección de eventos para errores del servidor.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|17|Error|Error del servidor.|  
  
 **[Categoría de eventos Cargar y guardar archivos](../../analysis-services/trace-events/file-load-and-save-event-category.md)**  
  
 Colección de eventos para los informes de las operaciones de carga y guardado de archivos.  
  
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
  
 **[Bloqueo (categoría de eventos)](../../analysis-services/trace-events/lock-events-category.md)**  
  
 Colección de eventos relacionados con los bloqueos.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|50|Deadlock|Interbloqueo de bloqueos de metadatos.|  
|51|Lock Timeout|Tiempo de espera de bloqueos de metadatos.|  
|52|Lock Acquired|Lock Acquired|  
|53|Lock Released|Lock Released|  
|54|Lock Waiting|Lock Waiting|  
  
 **[Eventos de notificación (categoría de eventos)](../../analysis-services/trace-events/notification-events-event-category.md)**  
  
 Colección de eventos de notificación.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|39|Notification|Evento de notificación.|  
|40|User Defined|Evento definido por el usuario.|  
  
 **[Informes de progreso (categoría de eventos)](../../analysis-services/trace-events/progress-reports-event-category.md)**  
  
 Colección de eventos para informes de progreso.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|5|Progress Report Begin|Inicio del informe de progreso.|  
|6|Progress Report End|Final del informe de progreso.|  
|7|Progress Report Current|Informe de progreso en curso.|  
|8|Progress Report Error|Error del informe de progreso.|  
  
 **[Categoría Eventos de consultas](../../analysis-services/trace-events/queries-events-category.md)**  
  
 Colección de eventos para las consultas.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|9|Query Begin|Inicio de la consulta.|  
|10|Query End|Final de la consulta.|  
  
 **[Procesamiento de consultas (categoría de eventos)](../../analysis-services/trace-events/query-processing-events-category.md)**  
  
 Colección de eventos clave durante el proceso de ejecución de una consulta.  
  
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
  
 **[Auditoría de seguridad (categoría de eventos)](../../analysis-services/trace-events/security-audit-event-category.md)**  
  
 Colección de clases de eventos de auditoría de la base de datos.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|1|Audit Login|Recopila todos los nuevos eventos de conexión desde que se inició el seguimiento, como cuando un cliente solicita una conexión a un servidor que ejecuta una instancia de SQL Server.|  
|2|Audit Logout|Recopila todos los nuevos eventos de desconexión desde que se inició el seguimiento, como cuando un cliente envía un comando de desconexión.|  
|4|Audit Server Starts And Stops|Registra las actividades de cierre, inicio y pausa de los servicios.|  
|18|Audit Object Permission Event|Registra los cambios de permiso de un objeto.|  
|19|Audit Admin Operations Event|Registra las operaciones de copia de seguridad/restauración/sincronización/operaciones de adjuntar o separar/carga de imágenes/guardado de imágenes realizadas en el servidor.|  
  
 [Eventos de sesión (categoría de eventos)](../../analysis-services/trace-events/session-events-event-category.md)  
  
 Colección de eventos de sesión.  
  
|**Identificador del evento**|**Nombre del evento**|**Descripción del evento**|  
|------------------|--------------------|---------------------------|  
|41|Existing Connection|Conexión existente del usuario.|  
|42|Existing Session|Sesión existente.|  
|43|Session Initialize|Sesión inicializada.|  
  
## <a name="see-also"></a>Vea también  
 [Usar SQL Server Profiler para supervisar Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
  
