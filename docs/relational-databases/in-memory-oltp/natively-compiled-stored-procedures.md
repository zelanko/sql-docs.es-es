---
title: Procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b718bafa35ae753eba0064db2af168054fd211ca
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="natively-compiled-stored-procedures"></a>Procedimientos almacenados compilados de forma nativa
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Los procedimientos almacenados compilados de forma nativa son los procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados para código nativo que tienen acceso a las tablas con optimización para memoria. Los procedimientos almacenados compilados de forma nativa permiten la ejecución eficaz de consultas y la lógica empresarial en el procedimiento almacenado. Para obtener más información sobre el proceso de compilación nativa, vea [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md). Para obtener más información sobre cómo migrar procedimientos almacenados basados en disco a procedimientos almacenados compilados de forma nativa, vea [Problemas de migración para los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md).  
  
> [!NOTE]  
>  Una diferencia entre los procedimientos almacenados (basados en disco) interpretados y los procedimientos almacenados compilados de forma nativa es que un procedimiento almacenado interpretado se compila en la primera ejecución mientras que un procedimiento almacenado compilado se compila cuando se crea. Con los procedimientos almacenados compilados de forma nativa, muchas condiciones de error se pueden detectar en el momento de la creación y harán que la creación del procedimiento almacenado compilado de forma nativa genere un error (desbordamiento aritmético, conversión de tipo y otras condiciones de división por cero). Con los procedimientos almacenados interpretados, estas condiciones de error normalmente no provocan un error al crear el procedimiento almacenado, pero todas las ejecuciones producirán un error.  
  
 Temas de esta sección:  
  
-   [Crear procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/creating-natively-compiled-stored-procedures.md)  
  
-   [Bloques atomic](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)  
  
-   [Características admitidas en los módulos T-SQL compilados de forma nativa](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [Construcciones DDL admitidas para módulos T-SQL compilados de forma nativa](../../relational-databases/in-memory-oltp/supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [Procedimientos almacenados compilados de forma nativa y opciones SET de ejecución.](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [Prácticas recomendadas para llamar a un procedimiento almacenado compilado de forma nativa](../../relational-databases/in-memory-oltp/best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [Supervisar el rendimiento de los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [Llamar a procedimientos almacenados compilados de forma nativa desde aplicaciones de acceso a datos](../../relational-databases/in-memory-oltp/calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>Vea también  
 [Tablas con optimización para memoria](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  

