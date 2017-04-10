---
title: "Aislar problemas de rendimiento | Microsoft Docs"
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
  - "aislar problemas rendimiento [SQL Server]"
  - "supervisar rendimiento [SQL Server], aislar problemas"
  - "supervisión de base de datos [SQL Server], aislar problemas"
  - "optimizar bases de datos [SQL Server], aislar problemas"
  - "supervisar rendimiento de servidor [SQL Server], aislar problemas"
  - "rendimiento de base de datos [SQL Server], aislar problemas"
  - "rendimiento de servidor [SQL Server], aislar problemas"
ms.assetid: 2eb425cb-9166-4027-ae08-c8fc2d236f44
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 16
---
# Aislar problemas de rendimiento
  A menudo suele ser más efectivo utilizar conjuntamente varias herramientas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Microsoft Windows para aislar los problemas de rendimiento de una base de datos que usar solo una herramienta cada vez. Por ejemplo, la característica Plan de ejecución gráfico, denominada también plan de presentación, le ayuda a reconocer los interbloqueos en una sola consulta. Sin embargo, puede reconocer más fácilmente otros problemas de rendimiento si utiliza conjuntamente las características de supervisión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Windows.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] puede usarse para supervisar y solucionar problemas de Transact-SQL o problemas relacionados con las aplicaciones. Asimismo, puede utilizar el Monitor de sistema para supervisar problemas relativos al hardware y otros problemas relacionados con el sistema.  
  
 Puede supervisar las siguientes áreas para solucionar problemas:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o lotes de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] enviadas por aplicaciones de usuarios.  
  
-   Actividad de los usuarios, como bloqueos o interbloqueos.  
  
-   Actividad del hardware, como el uso de los discos.  
  
 Algunos problemas posibles son:  
  
-   Errores de programación de aplicaciones debidos a instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] escritas incorrectamente.  
  
-   Errores de hardware, como los relativos a discos o a la red.  
  
-   Bloqueo excesivo debido a un diseño incorrecto de la base de datos.  
  
## Herramientas para solucionar problemas comunes de rendimiento  
 Igual de importante es la correcta selección del problema de rendimiento que desea que cada herramienta supervise u optimice. La herramienta y la utilidad dependen del tipo de problema de rendimiento que desee resolver.  
  
 En los temas siguientes se describen diversas herramientas de supervisión y optimización y los problemas que ayudan a solucionar.  
  
 [Identificar los cuellos de botella](../../relational-databases/performance/identify-bottlenecks.md)  
  
 [Supervisar el uso de la memoria](../../relational-databases/performance-monitor/monitor-memory-usage.md)  
  
  