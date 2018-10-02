---
title: Procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 44dd4f25c5811501ec4219acbdd9b24c0b96ab04
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674403"
---
# <a name="natively-compiled-stored-procedures"></a>procedimientos almacenados compilados de forma nativa
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Los procedimientos almacenados compilados de forma nativa son los procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados para código nativo que tienen acceso a las tablas optimizadas para memoria. Los procedimientos almacenados compilados de forma nativa permiten la ejecución eficaz de consultas y la lógica empresarial en el procedimiento almacenado. Para obtener más información sobre el proceso de compilación nativa, vea [Native Compilation of Tables and Stored Procedures](../../relational-databases/in-memory-oltp/native-compilation-of-tables-and-stored-procedures.md). Para obtener más información sobre cómo migrar procedimientos almacenados basados en disco a procedimientos almacenados compilados de forma nativa, vea [Problemas de migración para los procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md).  
  
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
  
## <a name="see-also"></a>Ver también  
 [Tablas con optimización para memoria](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
