---
title: "Aumentar el rendimiento de la replicación de mezcla | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Merge Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- subscriptions [SQL Server replication], performance considerations
- performance [SQL Server replication], merge replication
- agents [SQL Server replication], performance
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
caps.latest.revision: "47"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10bc53216b65298837a5086adf89550ad97606a7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="enhance-merge-replication-performance"></a>Aumentar el rendimiento de la replicación de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Tras considerar las sugerencias generales de rendimiento que se describen en [Aumentar el rendimiento general de la replicación](../../../relational-databases/replication/administration/enhance-general-replication-performance.md), tenga en cuenta estas otras áreas específicas de la replicación de mezcla.  
  
## <a name="database-design"></a>Diseño de la base de datos  
  
-   Indice las columnas utilizadas en filtros de fila y de combinación.  
  
     Cuando utilice un filtro de fila en un artículo publicado, cree un índice en cada una de las columnas utilizadas en la cláusula WHERE del filtro. Sin los índices, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tiene que leer todas las filas de la tabla para determinar si la fila debe incluirse en la partición. Con los índices, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede encontrar rápidamente qué filas se deben incluir. El procesamiento es más rápido si la replicación puede resolver completamente la cláusula WHERE del filtro solamente a partir del índice.  
  
     La indización de todas las columnas utilizadas en los filtros de combinación también es importante. Cada vez que se ejecuta el Agente de mezcla, busca la tabla base para determinar qué filas de la tabla principal y qué filas de las tablas relacionadas están incluidas en la partición. La creación de un índice en las columnas de combinación evita que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] lea todas las filas de la tabla cada vez que se ejecute el Agente de mezcla.  
  
     Para obtener más información sobre el filtrado, consulte [Filtrar datos publicados para la replicación de mezcla](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Considere la posibilidad de aplicar una normalización excesiva a las tablas que incluyan tipos de datos de objetos grandes (LOB).  
  
     Cuando se produce la sincronización, el Agente de mezcla puede tener que leer y transferir todas las filas de datos de un publicador o un suscriptor. Si la fila contiene columnas que utilizan LOB, este proceso puede requerir una asignación de memoria adicional y causar un impacto negativo en el rendimiento aunque no se hayan actualizado estas columnas. Para reducir la probabilidad de que se produzca este impacto en el rendimiento, considere colocar las columnas LOB en una tabla independiente con una relación de uno a uno al resto de datos de las filas. Los tipos de datos **text**, **ntext**y **image** han quedado desusados. Si incluye LOB, se recomienda que utilice los tipos de datos **varchar(max)**, **nvarchar(max)**y **varbinary(max)**, respectivamente.  
  
## <a name="publication-design"></a>Diseño de la publicación  
  
-   Use un nivel de compatibilidad de la publicación de 90RTM ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versión posterior).  
  
     A menos que uno o varios suscriptores usen una versión diferente de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especifique que la publicación admita únicamente [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versión posterior. Esto permite que la publicación aproveche las nuevas características y optimizaciones de rendimiento.  
  
-   Use la configuración correcta de retención de la publicación.  
  
     El período de retención de la publicación, que es la cantidad máxima de tiempo que debe transcurrir antes de que una suscripción se deba sincronizar, determina el tiempo de almacenamiento del seguimiento de metadatos. Un valor alto puede afectar el rendimiento de almacenamiento y procesamiento. Para obtener más información acerca de cómo configurar el período de retención de la publicación, vea [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
-   Utilice los artículos de solo descarga en las tablas que únicamente se cambian en el publicador. Para obtener más información, consulte [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
### <a name="filter-design-and-use"></a>Diseño y uso de filtros  
  
-   Limite la complejidad de las cláusulas de filtros de fila.  
  
     Limitar la complejidad del criterio de filtro ayuda a mejorar el rendimiento cuando el Agente de mezcla calcula los cambios de filas que se van a enviar a los suscriptores. Evite el uso de subselecciones dentro de las cláusulas de filtros de fila de mezcla. En su lugar, considere el uso de filtros de combinación, que normalmente son más eficaces cuando se utilizan para crear particiones de datos de una tabla en función de la cláusula de filtro de fila de otra tabla. Para obtener más información sobre el filtrado, consulte [Filtrar datos publicados para la replicación de mezcla](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md).  
  
-   Utilice particiones precalculadas con filtros con parámetros (esta característica se usa de manera predeterminada). Para obtener más información, vea [Optimización del rendimiento de los filtros con parámetros con particiones calculadas previamente](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
     Las particiones precalculadas imponen una serie de limitaciones en el comportamiento de los filtros. Si la aplicación no puede respetar estas limitaciones, establezca la opción **keep_partition_changes** en **True**, y así obtendrá ventajas de rendimiento. Para obtener más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Utilice particiones que no se superpongan si los datos se filtran pero no se comparten entre usuarios.  
  
     La replicación puede optimizar el rendimiento de los datos que no se comparten entre particiones o suscripciones. Para obtener más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   No cree jerarquías complejas de filtros de combinación.  
  
     Los filtros de combinación con cinco tablas o más pueden producir un efecto significativo en el rendimiento durante el proceso de mezcla. Se recomienda que considere otras soluciones si va a generar filtros de combinación de cinco o más tablas:  
  
    -   Evite el filtro de tablas que básicamente son tablas de búsqueda, tablas pequeñas y tablas que no están sujetas a cambios. Haga que estas tablas formen parte de la publicación en su totalidad. Se recomienda que utilice los filtros de combinación solamente entre tablas que se deben partir entre suscriptores. Para obtener más información, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
    -   Considere la posibilidad de eliminar la normalización del diseño de la base de datos o la utilización de una tabla de asignaciones si hay un gran número de tablas en una combinación. Por ejemplo, si un vendedor solamente necesita los datos de sus clientes, pero se requieren seis combinaciones para asociar un cliente con un vendedor, considere la posibilidad de agregar una columna a la tabla de clientes que identifique al vendedor. Los datos del vendedor son redundantes, pero los costos de eliminar la normalización de las tablas pueden ser en cierto modo compensados por los beneficios en el rendimiento de la partición de replicación.  
  
    -   Para aumentar el rendimiento de las particiones precalculadas cuando los lotes incluyen numerosos cambios de datos, diseñe su aplicación con cuidado. Asegúrese de que los cambios en los datos de la tabla primaria de un filtro de combinación se realicen antes que los cambios correspondientes de las tablas secundarias.  
  
-   Establezca la opción **join_unique_key** en **1** si lo permite la lógica.  
  
     Al establecer este parámetro en **1** , se indica que la relación entre la tabla principal y la secundaria de un filtro de combinación es de uno a uno o de uno a varios. Configure este parámetro en **1** únicamente si tiene una restricción en la columna de combinación de la tabla secundaria que garantiza la exclusividad. Si el parámetro se establece en **1** de forma incorrecta, se podría producir la no convergencia de los datos. Para obtener más información, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
-   Evite la ejecución de lotes con muchos cambios cuando use particiones precalculadas.  
  
     Cuando el Agente de mezcla se ejecute tras la ejecución de un lote que contenga numerosos cambios de datos, el agente intentará dividir este lote de gran tamaño en lotes más pequeños. Durante este tiempo, pueden bloquearse otros procesos del Agente de mezcla. Considere la posibilidad de reducir el número de cambios de un lote y ejecutar el Agente de mezcla entre los distintos lotes. Si esto último no es posible, aumente el valor de **generation_leveling_threshold** para la publicación.  
  
## <a name="subscription-considerations"></a>Consideraciones acerca de las suscripciones  
  
-   Establezca programaciones para sincronizar las suscripciones.  
  
     Si un gran número de suscriptores se sincronizan con un publicador, considere la posibilidad de escalonar las programaciones con el fin de que el Agente de mezcla se ejecute en distintos momentos. Para más información, consulte [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md).  
  
## <a name="merge-agent-parameters"></a>Parámetros del Agente de mezcla  
 Para obtener información sobre el Agente de mezcla y sus parámetros, vea [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md).  
  
-   Actualice todos los suscriptores de suscripciones de extracción a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versión posterior.  
  
     Al actualizar el suscriptor a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versión posterior se actualiza el Agente de mezcla que usan las suscripciones en el suscriptor. Para aprovechar muchas de las nuevas características y optimizaciones de rendimiento, se requiere el Agente de mezcla de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versión posterior.  
  
-   Si una suscripción se sincroniza mediante una conexión rápida y los cambios se envían desde el publicador y el suscriptor, use el parámetro **–ParallelUploadDownload** en el Agente de mezcla.  
  
     [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introdujo un nuevo parámetro del Agente de mezcla: **–ParallelUploadDownload**. Establecer este parámetro permite al Agente de mezcla procesar en paralelo los cambios cargados en el publicador y los descargados en el suscriptor. Esto resulta útil en entornos de grandes volúmenes con gran ancho de banda de red. Los parámetros del agente se pueden especificar en los perfiles del agente y en la línea de comandos. Para obtener más información, vea:  
  
    -   [Trabajar con perfiles del Agente de replicación](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [Ver y modificar parámetros del símbolo del sistema de los agentes de replicación &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   Considere aumentar el valor del parámetro **-MakeGenerationInterval** , especialmente si la sincronización implica más cargas de suscriptores que descargas a suscriptores.  
  
-   Cuando se sincronizan filas de datos con una gran cantidad de datos, como las filas que contienen columnas LOB, la sincronización web puede requerir la asignación de memoria adicional y afectar al rendimiento. Esto sucede cuando el Agente de mezcla genera un mensaje XML que contiene demasiadas filas de datos con grandes cantidades de datos. Si el Agente de mezcla consume demasiados recursos durante la sincronización web, se recomienda reducir el número de filas que se envían en un mismo mensaje mediante alguno de los siguientes procedimientos:  
  
    -   Usar el perfil de agente de conexión lenta para el Agente de mezcla. Para obtener más información, consulte [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
    -   Reduzca los parámetros **-DownloadGenerationsPerBatch** y **-UploadGenerationsPerBatch** del Agente de mezcla a un valor de 10 o menos. El valor predeterminado de esos parámetros es 50.  
  
## <a name="snapshot-considerations"></a>Consideraciones acerca de las instantáneas  
  
-   Cree una columna ROWGUIDCOL en tablas grandes antes de generar la instantánea inicial.  
  
     La replicación de mezcla requiere que todas las tablas publicadas tengan una columna ROWGUIDCOL. Si no existe una columna ROWGUIDCOL en la tabla antes de que el Agente de instantáneas cree los archivos de instantánea iniciales, el agente debe agregar y llenar primero la columna ROWGUIDCOL. Para mejorar el rendimiento cuando se generan instantáneas durante la replicación de mezcla, puede crear una columna ROWGUIDCOL en cada una de las tablas antes de publicar. La columna puede tener cualquier nombre (de forma predeterminada, el Agente de instantáneas utiliza**rowguid** ), pero debe tener las siguientes características de tipo de datos:  
  
    -   Un tipo de datos de UNIQUEIDENTIFIER.  
  
    -   Un valor predeterminado de NEWSEQUENTIALID() o NEWID(). Se recomienda NEWSEQUENTIALID() porque puede proporcionar un mayor rendimiento al efectuar cambios y realizar un seguimiento de los mismos.  
  
    -   El conjunto de propiedades ROWGUIDCOL.  
  
    -   Un índice único en la columna.  
  
-   Genere instantáneas previamente y/o permita a los suscriptores que soliciten la generación y aplicación de instantáneas la primera vez que se sincronizan.  
  
     Utilice una de estas opciones o las dos para proporcionar instantáneas para publicaciones que utilicen filtros con parámetros. Si no especifica una de estas opciones, las suscripciones se inicializan utilizando una serie de instrucciones SELECT e INSERT, en lugar de la utilidad **bcp** ; este proceso es mucho más lento. Para obtener más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
## <a name="maintenance-and-monitoring-considerations"></a>Consideraciones acerca del mantenimiento y la supervisión  
  
-   De vez en cuando, vuelva a crear los índices de tablas del sistema de la replicación de mezcla.  
  
     Como parte del mantenimiento de la replicación de mezcla, compruebe ocasionalmente el crecimiento de las tablas del sistema asociadas con la replicación de mezcla: **MSmerge_contents**, **MSmerge_genhistory**, **MSmerge_tombstone**, **MSmerge_current_partition_mappings**y **MSmerge_past_partition_mappings**. Vuelva a indizar estas tablas periódicamente. Para obtener más información, vea [Reorganizar y volver a generar índices](../../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
-   Supervise el rendimiento de la sincronización utilizando la pestaña **Historial de sincronizaciones** del Monitor de replicación.  
  
     En la replicación de mezcla, el Monitor de replicación muestra en la pestaña **Historial de sincronizaciones** estadísticas detalladas de cada artículo que se procesa durante la sincronización, incluida la cantidad de tiempo de cada fase del proceso (carga de cambios, descarga de cambios, etc.). Esto puede ayudar a identificar las tablas específicas que están causando una reducción de la velocidad y es el mejor lugar para solucionar problemas de rendimiento con las suscripciones de mezcla. Para obtener más información sobre cómo ver estadísticas detalladas, consulte [Ver información y realizar tareas para los agentes asociados a una suscripción &#40;Monitor de replicación&#41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md).  
  
  
