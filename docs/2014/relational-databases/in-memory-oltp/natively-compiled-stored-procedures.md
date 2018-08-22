---
title: Procedimientos almacenados compilados de forma nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- natively compiled stored procedures
ms.assetid: d5ed432c-10c5-4e4f-883c-ef4d1fa32366
caps.latest.revision: 54
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 79dbaba00d9eb8ff0b344fb713ee6599344ec317
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392605"
---
# <a name="natively-compiled-stored-procedures"></a>procedimientos almacenados compilados de forma nativa
  Los procedimientos almacenados compilados de forma nativa son los procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados para código nativo que tienen acceso a las tablas optimizadas para memoria. Los procedimientos almacenados compilados de forma nativa permiten la ejecución eficaz de consultas y la lógica empresarial en el procedimiento almacenado. Para obtener más información sobre el proceso de compilación nativa, vea [Native Compilation of Tables and Stored Procedures](native-compilation-of-tables-and-stored-procedures.md). Para obtener más información sobre cómo migrar procedimientos almacenados basados en disco a procedimientos almacenados compilados de forma nativa, vea [Problemas de migración para los procedimientos almacenados compilados de forma nativa](migration-issues-for-natively-compiled-stored-procedures.md).  
  
> [!NOTE]  
>  Una diferencia entre los procedimientos almacenados (basados en disco) interpretados y los procedimientos almacenados compilados de forma nativa es que un procedimiento almacenado interpretado se compila en la primera ejecución mientras que un procedimiento almacenado compilado se compila cuando se crea. Con los procedimientos almacenados compilados de forma nativa, muchas condiciones de error (desbordamiento aritmético, conversión de tipo y otras condiciones de división por cero) se pueden detectar en el momento de la creación y harán que la creación del procedimiento almacenado compilado de forma nativa genere un error. Con los procedimientos almacenados interpretados, estas condiciones de error normalmente no provocarán un error al crear el procedimiento almacenado, pero todas las ejecuciones producirán un error.  
  
 Temas de esta sección:  
  
-   [Crear procedimientos almacenados compilados de forma nativa](creating-natively-compiled-stored-procedures.md)  
  
-   [Bloques atómicos](atomic-blocks-in-native-procedures.md)  
  
-   [Construcciones admitidas en procedimientos almacenados compilados de forma nativa](supported-features-for-natively-compiled-t-sql-modules.md)  
  
-   [Utilizar Try..Catch en procedimientos almacenados compilados de forma nativa](../../database-engine/using-try-catch-in-natively-compiled-stored-procedures.md)  
  
-   [Construcciones admitidas en procedimientos almacenados compilados de forma nativa](supported-ddl-for-natively-compiled-t-sql-modules.md)  
  
-   [Procedimientos almacenados compilados de forma nativa y opciones SET de ejecución](natively-compiled-stored-procedures-and-execution-set-options.md)  
  
-   [Prácticas recomendadas para llamar a un procedimiento almacenado compilado de forma nativa](best-practices-for-calling-natively-compiled-stored-procedures.md)  
  
-   [Supervisar el rendimiento de los procedimientos almacenados compilados de forma nativa](monitoring-performance-of-natively-compiled-stored-procedures.md)  
  
-   [Llamar a procedimientos almacenados compilados de forma nativa desde aplicaciones de acceso a datos](calling-natively-compiled-stored-procedures-from-data-access-applications.md)  
  
## <a name="see-also"></a>Vea también  
 [Tablas con optimización para memoria](memory-optimized-tables.md)  
  
  
