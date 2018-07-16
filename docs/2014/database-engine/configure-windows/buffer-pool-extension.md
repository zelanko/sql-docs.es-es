---
title: Extensión del grupo de búferes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 909ab7d2-2b29-46f5-aea1-280a5f8fedb4
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e143cbf9540aab467bd57a5c4f923df81d658fb0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37328424"
---
# <a name="buffer-pool-extension"></a>Buffer Pool Extension
  A partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], la extensión del grupo de búferes proporciona una perfecta integración de una extensión de la memoria de acceso aleatorio no volátil (es decir, una unidad de estado sólido) con el grupo de búferes del [!INCLUDE[ssDE](../../includes/ssde-md.md)] para mejorar considerablemente el rendimiento de E/S. La extensión del grupo de búferes no está disponible en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="benefits-of-the-buffer-pool-extension"></a>Ventajas de la extensión del grupo de búferes  
 El propósito principal de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es almacenar y recuperar datos, por lo que una E/S de disco intensiva es una de las características principales del Motor de base de datos. Dado que las operaciones de E/S de disco pueden consumir muchos recursos y tardar bastante tiempo en completarse, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se centra en hacer la E/S muy eficaz. El grupo de búferes se utiliza como origen principal de asignación de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La administración de búfer es un componente clave para lograr esta eficacia. El componente de administración de búfer consta de dos mecanismos: el administrador de búfer para obtener acceso a las páginas de bases de datos y actualizarlas, y el grupo de búferes para reducir la E/S de archivos de base de datos.  
  
 Las páginas de datos y de índice se leen desde el disco en el grupo de búferes y las páginas modificadas (también conocidas como páginas desfasadas) se escriben en el disco. La presión de memoria en los puntos de comprobación de la base de datos y el servidor hace que las páginas desfasadas (activas) de la memoria caché del búfer se expulsen de la memoria caché y se escriban en discos mecánicos y después se lean de nuevo en la memoria caché. Estas operaciones de E/S suelen ser pequeñas lecturas y escrituras aleatorias del orden de 4 a 16 kB de datos. Los patrones aleatorios de E/S pequeños incurren en búsquedas frecuentes, compitiendo por el brazo del disco mecánico, lo que aumenta la latencia de E/S y reduce el rendimiento de E/S global del sistema.  
  
 El enfoque típico para solucionar estos cuellos de botella de E/S consiste en agregar más DRAM o, como alternativa, agregar ejes SAS de alto rendimiento. Aunque estas opciones son útiles, presentan unas desventajas importantes: la DRAM es más cara que las unidades de almacenamiento de datos y agregar ejes aumenta el gasto de la inversión para la adquisición de hardware y los costos operativos debido al mayor consumo energético y a la mayor probabilidad de que se produzca un error en un componente.  
  
 La característica de extensión del grupo de búferes extiende la memoria caché del grupo de búferes con almacenamiento no volátil (generalmente SSD). Debido a esta extensión, el grupo de búferes puede contener un espacio de trabajo de la base de datos mayor, lo que fuerza la paginación de operaciones de E/S entre la RAM y las SSD. Esto descarga de forma efectiva las pequeñas operaciones de E/S aleatorias de los discos mecánicos a las SSD. Debido a la menor latencia y al mejor rendimiento de E/S aleatoria de las SSD, la extensión del grupo de búferes mejora considerablemente el rendimiento de las operaciones de E/S.  
  
 En la lista siguiente se describen las ventajas de la característica de extensión del grupo de búferes.  
  
-   Mayor rendimiento de E/S aleatoria  
  
-   Menor latencia de E/S  
  
-   Mayor rendimiento de las transacciones  
  
-   El rendimiento de lectura mejora con un grupo de búferes híbrido mayor  
  
-   Una arquitectura de almacenamiento en memoria caché que puede aprovechar las unidades de memoria de bajo costo actuales y futuras  
  
### <a name="concepts"></a>Conceptos  
 Los siguientes términos son aplicables a la característica de extensión del grupo de búferes.  
  
 Unidad de estado sólido (SSD)  
 Las unidades de estado sólido almacenan los datos en memoria (RAM) de forma persistente. Para obtener más información, vea [esta definición](http://en.wikipedia.org/wiki/Solid-state_drive).  
  
 Búfer  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], un búfer es una página de 8 kB en memoria (el mismo tamaño que una página de índice o de datos). Por tanto, la memoria caché del búfer está dividida en páginas de 8 kB. Una página permanece en la memoria caché del búfer hasta que el administrador de búfer necesita el área del búfer para leer en ella más datos. Los datos solo vuelven a escribirse en el disco si se han modificado. Estas páginas modificadas en memoria se conocen como páginas desfasadas. Una página está limpia cuando es equivalente a su imagen de la base de datos en el disco. Los datos de la memoria caché del búfer se pueden modificar varias veces antes de que se vuelvan a escribir en el disco.  
  
 Grupo de búferes  
 También se llama memoria caché del búfer. El grupo de búferes es un recurso global compartido por todas las bases de datos para sus páginas de datos en caché. El tamaño máximo y mínimo de la memoria caché del grupo de búferes se determina durante el inicio o cuando la instancia de SQL Server se reconfigura dinámicamente mediante sp_configure. Este tamaño determina el número máximo de páginas que se pueden almacenar en memoria caché en el grupo de búferes en cualquier momento en la instancia en ejecución.  
  
 Punto de comprobación  
 Un punto de comprobación crea un punto conocido correcto desde el que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede empezar a aplicar los cambios incluidos en el registro de transacciones durante la recuperación después de un cierre inesperado o un bloqueo del sistema. Un punto de comprobación escribe las páginas desfasadas y la información del registro de transacciones de la memoria al disco y, además, registra información acerca del registro de transacciones. Para obtener más información, vea [Puntos de comprobación de base de datos &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
## <a name="buffer-pool-extension-details"></a>Detalles de la extensión del grupo de búferes  
 El almacenamiento SSD se utiliza como extensión del subsistema de memoria en lugar del subsistema de almacenamiento en disco. Es decir, el archivo de la extensión del grupo de búferes permite que el administrador del grupo de búferes utilice tanto memoria DRAM como NAND-Flash para mantener un grupo de búferes mucho mayor de páginas normales en memoria de acceso aleatorio no volátil respaldada por SSD. Esto crea una jerarquía de almacenamiento en memoria caché de varios niveles, siendo el nivel 1 (L1) la DRAM y el nivel 2 (L2) el archivo de extensión del grupo de búferes en la SSD. Solo las páginas limpias se escriben en la memoria caché L2, lo que ayuda a mantener la seguridad de los datos. El administrador de búfer controla el movimiento de páginas limpias entre las memorias caché L1 y L2.  
  
 En la ilustración siguiente se proporciona información general sobre la arquitectura del grupo de búferes con respecto a otros componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 ![Arquitectura de la extensión del grupo de búferes SSD](../media/ssdbufferpoolextensionarchitecture.gif "Arquitectura de la extensión del grupo de búferes SSD")  
  
 Cuando está habilitada, la extensión del grupo de búferes especifica el tamaño y la ruta de acceso del archivo de almacenamiento en caché del grupo de búferes en la SSD. Este archivo es una extensión contigua del almacenamiento en la SSD y se configura de forma estática durante el inicio de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las modificaciones de los parámetros de configuración del archivo solo se pueden hacer cuando la característica de extensión del grupo de búferes está deshabilitada. Cuando la extensión del grupo de búferes está deshabilitada, toda la configuración relacionada se quita del Registro. El archivo de la extensión del grupo de búferes se elimina tras el cierre de la instancia de SQL Server.  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Se aconseja seguir estas prácticas recomendadas.  
  
-   Tras habilitar la extensión del grupo de búferes por primera vez, se recomienda reiniciar la instancia de SQL Server para aprovechar las ventajas derivadas de un rendimiento máximo.  
  
-   El tamaño de extensión del grupo de búferes puede ser hasta 32 veces el valor de max_server_memory en las ediciones Enterprise y hasta cuatro veces para la edición Standard.  Se recomienda una proporción no superior a 1:16 entre el tamaño de la memoria física (max_server_memory) y el tamaño de la extensión del grupo de búferes. Puede ser óptima una proporción menor entre 1:4 y 1:8. Para obtener más información sobre cómo establecer la opción max_server_memory, vea [Opciones de configuración de memoria de servidor](server-memory-server-configuration-options.md).  
  
-   Pruebe la extensión del grupo de búferes minuciosamente antes de implementarla en un entorno de producción. Una vez en producción, evite realizar cambios de configuración en el archivo o desactivar la característica. Estas actividades pueden afectar negativamente al rendimiento del servidor porque el tamaño del grupo de búferes se reduce considerablemente cuando se deshabilita la característica. Cuando está deshabilitada, la memoria empleada para admitir la característica no se recupera hasta que no se reinicia la instancia de SQL Server. Sin embargo, si se vuelve a habilitar la característica, la memoria se reutilizará sin reiniciar la instancia.  
  
## <a name="return-information-about-the-buffer-pool-extension"></a>Devolver información sobre la extensión del grupo de búferes  
 Puede utilizar las siguientes vistas de administración dinámica para mostrar la configuración de la extensión del grupo de búferes y devolver información acerca de las páginas de datos de la extensión.  
  
-   [sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql)  
  
-   [sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql)  
  
 En el objeto Buffer Manager de SQL Server hay disponibles contadores de rendimiento para hacer un seguimiento de las páginas de datos en el archivo de la extensión del grupo de búferes. Para obtener más información, vea los [contadores de rendimiento de la extensión del grupo de búferes](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md).  
  
 Están disponibles los siguientes Xevents.  
  
|XEvent|Descripción|Parámetros|  
|------------|-----------------|----------------|  
|sqlserver.buffer_pool_extension_pages_written|Se desencadena cuando una página o un grupo de páginas se expulsan del grupo de búferes y se escriben en el archivo de extensión del grupo de búferes.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|  
|sqlserver.buffer_pool_extension_pages_read|Se desencadena cuando se lee en el grupo de búferes una página del archivo de la extensión del grupo de búferes.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|  
|sqlserver.buffer_pool_extension_pages_evicted|Se desencadena cuando se expulsa una página del archivo de la extensión del grupo de búferes.|number_page<br /><br /> first_page_id<br /><br /> first_page_offset<br /><br /> initiator_numa_node_id|  
|sqlserver.buffer_pool_eviction_thresholds_recalculated|Se desencadena cuando se calcula el umbral de expulsión.|warm_threshold<br /><br /> cold_threshold<br /><br /> pages_bypassed_eviction<br /><br /> eviction_bypass_reason<br /><br /> eviction_bypass_reason_description|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descripción de la tarea**|**Tema**|  
|Habilitar y configurar la extensión del grupo de búferes|[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)|  
|Modificar la configuración de la extensión del grupo de búferes|[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)|  
|Ver la configuración de la extensión del grupo de búferes|[sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql)|  
|Supervisar la extensión del grupo de búferes|[sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql)<br /><br /> [Contadores de rendimiento](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)|  
  
  
