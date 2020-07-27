---
title: Establecer una línea base del rendimiento | Microsoft Docs
description: Tome medidas del rendimiento a intervalos regulares, incluso cuando no existan problemas, para establecer una base de referencia del rendimiento del servidor en SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], baselines
- monitoring performance [SQL Server], baselines
- tuning databases [SQL Server], baselines
- server performance [SQL Server], baselines
- performance [SQL Server], baselines
- baseline performance [SQL Server]
- measurements for baseline statistics [SQL Server]
- monitoring server performance [SQL Server], establishing baseline
- database monitoring [SQL Server], baselines
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 619e9d6ad55f17fece2a9d327d4e0d67512e4b90
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457693"
---
# <a name="establish-a-performance-baseline"></a>Establecer una línea base del rendimiento
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Para determinar si el sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funciona de forma óptima, tome medidas del rendimiento a intervalos regulares, incluso cuando no existan problemas, para establecer una línea base del rendimiento del servidor. Compare cada conjunto de medidas nuevo con las medidas tomadas anteriormente.  
  
 Las áreas siguientes afectan al rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Recursos del sistema (hardware)  
  
-   Arquitectura de red  
  
-   Sistema operativo  
  
-   Aplicaciones de bases de datos  
  
-   Aplicaciones cliente  
  
 Como mínimo, utilice las medidas de línea base para determinar:  
  
-   Las horas con el máximo y el mínimo nivel de funcionamiento.  
  
-   Tiempos de respuesta de comandos de procesamiento por lotes o consultas de producción.  
  
-   Tiempos de finalización de operaciones de copias de seguridad y restauración de bases de datos  
  
 Cuando haya establecido la línea base para el rendimiento del servidor, compare las estadísticas de la línea base con el rendimiento actual del servidor. Unas cifras demasiado elevadas o demasiado reducidas con respecto a la línea base indican que hay que realizar una investigación más detallada. Pueden indicar áreas que hay que optimizar o volver a configurar. Por ejemplo, si aumenta el tiempo necesario para ejecutar un conjunto de consultas, examine las consultas para determinar si puede volver a escribirlas o si es necesario agregar estadísticas de columnas u otros índices.  
  
## <a name="see-also"></a>Consulte también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
