---
title: Aislamiento de problemas de rendimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- isolating performance problems [SQL Server]
- monitoring performance [SQL Server], isolating problems
- database monitoring [SQL Server], isolating problems
- tuning databases [SQL Server], isolating problems
- monitoring server performance [SQL Server], isolating problems
- database performance [SQL Server], isolating problems
- server performance [SQL Server], isolating problems
ms.assetid: 2eb425cb-9166-4027-ae08-c8fc2d236f44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e700f5178a3520fe83f4d896662a8741aa166b9a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63150914"
---
# <a name="isolate-performance-problems"></a>Aislar problemas de rendimiento
  A menudo, es más eficaz usar varias [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] herramientas de o Microsoft Windows juntas para aislar los problemas de rendimiento de la base de datos que usar una herramienta a la vez. Por ejemplo, la característica Plan de ejecución gráfico, denominada también plan de presentación, le ayuda a reconocer los interbloqueos en una sola consulta. Sin embargo, puede reconocer más fácilmente otros problemas de rendimiento si utiliza conjuntamente las características de supervisión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Windows.  
  
 
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] puede usarse para supervisar y solucionar problemas de Transact-SQL o problemas relacionados con las aplicaciones. Asimismo, puede utilizar el Monitor de sistema para supervisar problemas relativos al hardware y otros problemas relacionados con el sistema.  
  
 Puede supervisar las siguientes áreas para solucionar problemas:  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o lotes de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] enviadas por aplicaciones de usuarios.  
  
-   Actividad de los usuarios, como bloqueos o interbloqueos.  
  
-   Actividad del hardware, como el uso de los discos.  
  
 Algunos problemas posibles son:  
  
-   Errores de programación de aplicaciones debidos a instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] escritas incorrectamente.  
  
-   Errores de hardware, como los relativos a discos o a la red.  
  
-   Bloqueo excesivo debido a un diseño incorrecto de la base de datos.  
  
## <a name="tools-for-common-performance-problems"></a>Herramientas para solucionar problemas comunes de rendimiento  
 Igual de importante es la correcta selección del problema de rendimiento que desea que cada herramienta supervise u optimice. La herramienta y la utilidad dependen del tipo de problema de rendimiento que desee resolver.  
  
 En los temas siguientes se describen diversas herramientas de supervisión y optimización y los problemas que ayudan a solucionar.  
  
 [Identificar los cuellos de botella](identify-bottlenecks.md)  
  
 [Supervisar el uso de la memoria](../performance-monitor/monitor-memory-usage.md)  
  
  
