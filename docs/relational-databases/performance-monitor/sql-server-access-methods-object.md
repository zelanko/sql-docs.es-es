---
title: "Access Methods (objeto de SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Access Methods, objeto"
  - "SQLServer:Access Methods"
ms.assetid: 27558585-e780-48bb-a042-30d664662ebc
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Access Methods (objeto de SQL Server)
  El objeto **Access Methods** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar la forma en que se obtiene acceso a los datos lógicos de una base de datos. El acceso físico a las páginas de base de datos en disco se supervisa mediante los contadores de **Buffer Manager** . La supervisión de los métodos que se utilizan para el acceso a los datos almacenados en la base de datos puede ayudar a determinar si se puede mejorar el rendimiento de las consultas al agregar o modificar índices, agregar o mover particiones, agregar archivos o grupos de archivos, desfragmentar índices o volver a escribir las consultas. Los contadores de **Access Methods** también se pueden utilizar para supervisar la cantidad de datos, los índices y el espacio disponible en la base de datos, con lo que se indica el volumen de datos y la fragmentación para cada instancia de servidor. Una fragmentación excesiva de los índices puede tener un efecto negativo sobre el rendimiento.  
  
 Para obtener información detallada acerca del volumen de datos, la fragmentación y el uso, utilice las siguientes vistas de administración dinámica:  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)  
  
-   [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)  
  
 Para el consumo de espacio en **tempdb** en el nivel de archivo, tarea y sesión, utilice las siguientes vistas de administración dinámica:  
  
-   [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
-   [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)  
  
-   [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
  
 En esta tabla se describen los contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Access Methods** .  
  
|Contadores de Access Methods de SQL Server|Description|  
|----------------------------------------|-----------------|  
|**Lotes de limpieza de UA/seg.**|Número de lotes por segundo completados correctamente por la tarea en segundo plano que limpia las unidades de asignación eliminadas y diferidas.|  
|**Limpiezas de UA/seg.**|Número de unidades de asignación por segundo eliminadas con éxito por la tarea en segundo plano que limpia las unidades de asignación eliminadas y diferidas. Cada eliminación de una unidad de asignación requiere varios lotes.|  
|**Recuento de creación de Lob por referencia**|Recuento de valores de objetos grandes (lob) que se han pasado por referencia. Los Lobs por referencia se utilizan en ciertas operaciones masivas para evitar el costo que implica pasarlos por valor.|  
|**Recuento de uso de Lob por referencia**|Recuento de los valores Lob por referencia que se han utilizado. Los Lobs por referencia se utilizan en ciertas operaciones masivas para evitar el costo que implica pasarlos por valor.|  
|**Recuento de lectura previa de objetos grandes (lob)**|Recuento de páginas Lob en las que se ha emitido una lectura previa.|  
|**Recuento de extracciones de manera consecutiva**|Recuento de valores de columna que se han extraído de manera consecutiva a no consecutiva.|  
|**Recuento de inserciones de manera no consecutiva**|Recuento de los valores de columna de inserción de manera consecutiva a no consecutiva.|  
|**UA quitadas diferidas**|Número de unidades de asignación a la espera de ser eliminadas por la tarea en segundo plano que limpia las unidades de asignación eliminadas y diferidas.|  
|**Conjuntos de filas quitados diferidos**|Número de conjuntos de filas creados como consecuencia de operaciones anuladas de creación de índices en línea a la espera de ser eliminados por la tarea en segundo plano que limpia los conjuntos de filas eliminados y diferidos.|  
|**Limpiezas de conjuntos de filas quitados/s**|Número de conjuntos de filas creados por segundo como consecuencia de operaciones anuladas de creación de índices en línea que ha eliminado con éxito la tarea en segundo plano que limpia los conjuntos de filas eliminados y diferidos.|  
|**Conjuntos de filas quitados omitidos/seg.**|Número de conjuntos de filas creados por segundo como consecuencia de operaciones anuladas de creación de índices en línea que ha omitido la tarea en segundo plano que limpia los conjuntos de filas eliminados y diferidos.|  
|**Cancelaciones de asignación de extensiones/seg.**|Número de cancelaciones de asignación de extensiones por segundo en todas las bases de datos de esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Extensiones asignadas/seg.**|Número de asignaciones de extensiones por segundo en todas las bases de datos de esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Lotes de limpieza de UA con error/seg.**|Número de lotes por segundo erróneos y que se han vuelto a intentar por la tarea en segundo plano que limpia las unidades de asignación eliminadas y diferidas. El error podría ser debido a la falta de memoria o espacio en disco, a un error de hardware o a ambas circunstancias.|  
|**Error de cookie de página hoja**|Número de veces que la cookie de una página hoja no se ha podido utilizar durante una búsqueda de índices porque se han producido cambios en la página hoja. La cookie se utiliza para acelerar la búsqueda de índices.|  
|**Error de cookie de página de árbol**|Número de veces que la cookie de una página de árbol no se ha podido utilizar durante una búsqueda de índices porque se han producido cambios en las páginas primarias de esas páginas de árbol. La cookie se utiliza para acelerar la búsqueda de índices.|  
|**Registros reenviados/seg.**|Número de registros por segundo capturados mediante punteros de registros reenviados.|  
|**Capturas de páginas de espacio disponible/seg.**|Número de capturas de página por segundo por los recorridos de espacio disponible. Estos recorridos buscan espacio libre en las páginas que ya están asignadas a una unidad de asignación para satisfacer las solicitudes de inserción o modificación de fragmentos de registro.|  
|**Recorridos de espacio disponible/seg.**|Número de recorridos por segundo iniciados para buscar espacio libre en las páginas que ya están asignadas a una unidad de asignación para insertar o modificar un fragmento de registro. Cada recorrido puede encontrar varias páginas.|  
|**Recorridos completos/seg.**|Número de recorridos completos sin restricciones por segundo. Puede tratarse de recorridos de tablas base o de índices completos.|  
|**Búsquedas en índices/seg.**|Número de búsquedas en índices por segundo. Se utiliza para iniciar un recorrido de intervalo, cambiar la posición de un recorrido de intervalo, revalidar un punto de recorrido, capturar un registro de índice y buscar en el índice el punto de inserción de una nueva fila.|  
|**Esperas de InSysXact/seg.**|Número de veces que un lector debe esperar una página porque está establecido el bit InSysXact.|  
|**Recuento de creación de LobHandle**|Recuento de los Lobs creados temporalmente.|  
|**Recuento de destrucción de LobHandle**|Recuento de los Lobs destruidos temporalmente.|  
|**Recuento de creación de proveedores de LobSS**|Recuento de proveedores de servicios de almacenamiento de LOB (LobSSP) creados. Se crea una tabla de trabajo por LobSSP.|  
|**Recuento de destrucción de proveedores de LobSS**|Recuento de LobSSP destruidos.|  
|**Recuento de truncamiento de proveedores de LobSS**|Recuento de LobSSP truncados.|  
|**Asignaciones de página mixta/seg.**|Número de páginas asignadas por segundo desde extensiones mixtas. Puede utilizarse para almacenar las páginas IAM y las primeras ocho páginas asignadas a una unidad de asignación.|  
|**Intentos de compresión de página por segundo**|El número de páginas evaluado para la compresión de nivel de página. Incluye páginas que no se comprimieron porque se consiguieron ahorros de espacio significativos. Incluye todos los objetos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información sobre objetos específicos, vea [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md).|  
|**Cancelaciones de asignación de páginas/seg.**|Número de cancelaciones de asignación de páginas por segundo en todas las bases de datos de esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se incluyen las páginas de extensiones mixtas y extensiones uniformes.|  
|**Divisiones de páginas/seg.**|Número de divisiones de páginas por segundo que se producen como resultado del desbordamiento de páginas de índices.|  
|**Páginas asignadas/seg.**|Número de asignaciones de páginas por segundo en todas las bases de datos de esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se incluyen las asignaciones de páginas de extensiones mixtas y extensiones uniformes.|  
|**Páginas comprimidas por segundo**|Número de páginas de datos que se comprimen usando la compresión PAGE. Incluye todos los objetos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información sobre objetos específicos, vea [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md).|  
|**Recorridos de sondeo/seg.**|Número de recorridos de sondeo por segundo que se utilizan para buscar como máximo una fila calificada directamente en una tabla de índices o una tabla base.|  
|**Recorridos de intervalo/seg.**|Número de recorridos de intervalo calificados por segundo a través de índices.|  
|**Revalidaciones del punto de recorrido/seg.**|Número de veces por segundo que fue necesario volver a validar el punto de recorrido para continuar el recorrido.|  
|**Registros fantasma omitidos/seg.**|Número de registros fantasma omitidos por segundo durante los recorridos.|  
|**Extensiones de bloqueo de tabla/seg.**|El número de veces que los bloqueos de las tablas fueron extendidos a la granularidad TABLA o HoBT.|  
|**Cookie de página hoja utilizada**|Número de veces que una cookie de página hoja se utiliza con éxito durante una búsqueda de índices porque no se produjo ningún cambio en la página hoja. La cookie se utiliza para acelerar la búsqueda de índices.|  
|**Cookie de página de árbol utilizada**|Número de veces que una cookie de página de árbol se utiliza con éxito durante una búsqueda de índices porque no se produjo ningún cambio en la página primaria de la página de árbol. La cookie se utiliza para acelerar la búsqueda de índices.|  
|**Archivos de trabajo creados/seg.**|Número de archivos de trabajo creados por segundo. Por ejemplo, los archivos de trabajo se pueden utilizar para almacenar los resultados temporales de las combinaciones hash y agregados hash.|  
|**Tablas de trabajo creadas/seg.**|Número de tablas de trabajo creadas por segundo. Por ejemplo, las tablas de trabajo se pueden utilizar para almacenar los resultados temporales de una cola de consultas, variables lob, variables XML y cursores.|  
|**Base de tablas de trabajo desde caché**|Exclusivamente para uso interno.|  
|**Relación de tablas de trabajo desde caché**|Porcentaje de tablas de trabajo creadas donde las dos páginas iniciales de la tabla de trabajo no fueron asignadas pero estaban inmediatamente disponibles desde la caché de la tabla de trabajo. (Cuando se elimina una tabla de trabajo, dos páginas pueden permanecer asignadas y se devuelven a la caché de la tabla de trabajo. Esto aumenta el rendimiento.)|  
  
## Vea también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  