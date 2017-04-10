---
title: "Buffer Manager (objeto de SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Buffer Manager [objeto]"
  - "SQLServer:Buffer Manager"
ms.assetid: 9775ebde-111d-476c-9188-b77805f90e98
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Buffer Manager (objeto de SQL Server)
  El objeto **Buffer Manager** proporciona contadores para supervisar cómo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza:  
  
-   La memoria para almacenar las páginas de datos.  
  
-   Los contadores para supervisar la E/S física mientras [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lee y escribe páginas de la base de datos.  
  
-   Extensión del grupo de búferes para ampliar la memoria caché del búfer utilizando el almacenamiento no volátil rápido como las unidades de estado sólido (SSD).  
  
 Supervisar la memoria y los contadores que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ayuda a determinar:  
  
-   Si existen cuellos de botella a causa de una memoria física inadecuada. Si no puede almacenar los datos a los que se tiene acceso con frecuencia en la memoria caché, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe recuperar los datos del disco.   
  
-   Si se puede mejorar el rendimiento de las consultas agregando memoria o aumentando la memoria disponible para la caché de datos o las estructuras internas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   La frecuencia con que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesita leer los datos del disco. En comparación con otras operaciones, como el acceso a memoria, la E/S física consume mucho tiempo. La reducción de la E/S física puede mejorar el rendimiento de las consultas.  
  
## Objetos de rendimiento del administrador de búfer  
 En esta tabla se describen los objetos de rendimiento del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Buffer Manager** .  
  
|Contadores de SQLServer:Buffer Manager|Description|  
|----------------------------------------|-----------------|  
|**Páginas del escritor en segundo plano/s**|Número de páginas vaciadas para aplicar la configuración de intervalo de recuperación.| 
|**Frecuencia de aciertos de caché del búfer**|Indica el porcentaje de páginas encontradas en la memoria caché del búfer sin necesidad de leer el disco. Esta frecuencia es el número total de aciertos de caché dividido por el número total de búsquedas en los últimos miles de accesos a la página. Tras un largo período, la proporción varía muy poco. Como la lectura de la caché es mucho más económica que la lectura del disco, es conveniente que esta frecuencia sea alta. Normalmente, puede aumentar la frecuencia de aciertos de caché del búfer si aumenta la cantidad de memoria disponible para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o utiliza la característica de extensión del grupo de búferes.|  
|**Base de aciertos de caché del búfer**|Exclusivamente para uso interno.|
|**Páginas de punto de comprobación/seg.**|Indica el número de páginas limpiadas en el disco por segundo por los puntos de comprobación u otras operaciones que requieren la limpieza de todas las páginas desfasadas.|  
|**Páginas de base de datos**|Indica el número de páginas en el grupo de búferes con contenido de la base de datos.|  
|**Páginas asignadas de extensión**|Número total de páginas no disponibles en el archivo de la extensión del grupo de búferes.|  
|**Páginas disponibles de extensión**|Número total de páginas disponibles en el archivo de la extensión del grupo de búferes.|  
|**Extensión en uso como porcentaje**|Porcentaje del archivo de paginación de la extensión del grupo de búferes ocupado por las páginas del administrador de búfer.|  
|**Contador de E/S pendientes de extensión**|Longitud de la cola de E/S para el archivo de la extensión del grupo de búferes.|  
|**Expulsiones de página de extensión/s**|Número de páginas expulsadas del archivo de la extensión del grupo de búferes por segundo.|  
|**Lecturas de página de extensión/s**|Número de páginas leídas del archivo de la extensión del grupo de búferes por segundo.|  
|**Tiempo sin referencia de página de extensión**|Promedio de segundos que una página permanecerá en la extensión del grupo de búferes sin referencias a él.|  
|**Escrituras de páginas de extensión/s**|Número de páginas escritas en el archivo de la extensión del grupo de búferes por segundo.|  
|**Obstrucciones de la lista de búferes disponibles/s**|Indica el número de solicitudes por segundo que tuvieron que esperar a una página disponible.|  
|**Pendiente del controlador integral**|Pendiente que el controlador integral del grupo de búferes usó en último lugar, multiplicado por -10 000 millones.| 
|**Escrituras diferidas/seg.**|Indica el número de búferes escritos por el objeto de escritura diferida del administrador de búfer. El objeto de *escritura diferida* es un proceso del sistema que vacía procesos por lotes de búferes antiguos y desfasados (búferes que contienen cambios que se deben volver a escribir en disco antes de volver a usar el búfer para una página diferente), de forma que estén disponibles para procesos de usuario. El objeto de escritura diferida elimina la necesidad de realizar puntos de comprobación con frecuencia con el propósito de crear búferes disponibles.|  
|**Duración prevista de la página**|Indica el número de segundos que una página permanecerá en el grupo de búferes sin referencias.|  
|**Búsquedas de páginas/seg.**|Indica el número de solicitudes por segundo de búsqueda de una página en el grupo de búferes.|  
|**Lecturas de página/seg.**|Indica el número de lecturas de página físicas emitidas por segundo. Esta estadística muestra el número total de lecturas de páginas físicas en todas las bases de datos. Como la E/S física es costosa, puede reducir el costo que supone si utiliza una caché de datos más grande, índices inteligentes y consultas más eficaces, o bien si cambia el diseño de la base de datos.|  
|**Escrituras de página/seg.**|Indica el número de escrituras de página físicas emitidas por segundo.|  
|**Páginas de lectura previa/seg.**|Indica el número de páginas leídas por segundo antes de su uso.|  
|**Tiempo de lectura previa/s**|Tiempo (en microsegundos) empleado emitiendo lecturas anticipadas.|
|**Páginas de destino**|Número ideal de páginas en el grupo de búferes.|

  
## Vea también  
 [SQL Server:Buffer Node](../../relational-databases/performance-monitor/sql-server-buffer-node.md)   
 [Opciones de configuración de memoria del servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Plan Cache (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)   
 [Supervisar el uso de recursos &#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)   
 [Extensión del grupo de búferes](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  