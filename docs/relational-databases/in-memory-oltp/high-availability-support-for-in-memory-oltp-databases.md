---
title: "Compatibilidad con alta disponibilidad para bases de datos OLTP en memoria | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Compatibilidad con alta disponibilidad para bases de datos OLTP en memoria
  Las bases de datos que contienen tablas con optimización para memoria, con o sin procedimientos almacenados compilados nativos, son totalmente compatibles con grupos de disponibilidad AlwaysOn.  No hay ninguna diferencia en la configuración y la compatibilidad de las bases de datos que contienen objetos de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] en comparación con las que no tienen.  
  
 Cuando se implementa una base de datos de OLTP en memoria en una configuración de Grupo de disponibilidad AlwaysOn, los cambios en las tablas con optimización para memoria en la réplica principal se aplican en memoria a las tablas de las réplicas secundarias, cuando se aplica REDO. Esto significa que la conmutación por error a una réplica secundaria puede ser muy rápida, puesto que los datos ya están en memoria. Además, las tablas están disponibles para las consultas en las réplicas secundarias que se han configurado para el acceso de lectura.  
  
## Grupos de disponibilidad AlwaysOn y bases de datos OLTP en memoria  
 La configuración de bases de datos con componentes de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] proporciona lo siguiente:  
  
-   **Una experiencia completamente integrada**   
    Puede configurar las bases de datos que contienen tablas con optimización para memoria usando el mismo asistente con el mismo nivel de compatibilidad para las réplicas secundarias sincrónicas y asincrónicas. Además, el seguimiento de estado se proporciona con el panel AlwaysOn familiar en SQL Server Management Studio.  
  
-   **Tiempo de conmutación por error comparable**   
    Las réplicas secundarias mantienen el estado en memoria de las tablas duraderas con optimización para memoria. En caso de conmutación por error automática o forzada, el tiempo de conmutación por error a la nueva principal es comparable a las tablas de bases de disco ya que no es necesaria la recuperación. En esta configuración, se admiten tablas con optimización para memoria creadas como SCHEMA_ONLY. Sin embargo, no se registran los cambios en estas tablas y, por tanto, no existirá ningún dato en estas tablas en la réplica secundaria.  
  
-   **Secundario legible**   
    Puede obtener acceso a las tablas con optimización para memoria en la réplica secundaria y consultarlas si se ha configurado para acceso de lectura. En [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], la marca de tiempo de lectura en la réplica secundaria está en estrecha sincronía con la marca de tiempo de lectura en la réplica principal, lo que significa que los cambios en la principal se ven muy rápidamente en la secundaria. Este comportamiento de sincronización tan estrecho es diferente de OLTP en memoria de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
## Instancia de clústeres de conmutación por error (FCI) y bases de datos OLTP en memoria  
 Para lograr alta disponibilidad en una configuración de almacenamiento compartido, puede configurar clústeres de conmutación por error en instancias con una o varias bases de datos con tablas con optimización para memoria. Necesitará tener en cuenta los siguientes factores como parte de la configuración de una FCI.  
  
-   **Objetivo de tiempo de recuperación**   
    El tiempo de conmutación por error será mayor ya que las tablas con optimización para memoria deben cargarse en memoria antes de que la base de datos pueda estar disponible.  
  
-   **Tablas SCHEMA_ONLY**   
    Tenga en cuenta que las tablas SCHEMA_ONLY estarán vacías sin filas después de la conmutación por error. Así es como se ha diseñado y definido por la aplicación. Este es exactamente el mismo comportamiento que cuando se reinicia una base de datos [!INCLUDE[hek_2](../../includes/hek-2-md.md)] con una o más tablas SCHEMA_ONLY.  
  
## Compatibilidad para la replicación de transacciones en OLTP en memoria  
 Las tablas que actúan como suscriptores de replicación transaccional, excluida la replicación transaccional punto a punto, pueden configurarse como tablas con optimización para memoria. Otras configuraciones de replicación no son compatibles con las tablas con optimización para memoria.  Para obtener más información, vea [Replicación en suscriptores de tablas con optimización para memoria](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md).  
  
## Vea también  
 [Grupos de disponibilidad AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Secundarias activas: réplicas secundarias legibles (grupos de disponibilidad AlwaysOn)](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Replicación en suscriptores de tablas con optimización para memoria](../../relational-databases/replication/replication-to-memory-optimized-table-subscribers.md)  
  
  