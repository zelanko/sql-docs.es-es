---
title: Acceso a tablas con optimización para memoria mediante Transact-SQL interpretado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 92a44d4d-0e53-4fb0-b890-de264c65c95a
author: rothja
ms.author: jroth
ms.openlocfilehash: af4b3ca7731e7ca13e697f43e76ac3cc3cacb4f1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050401"
---
# <a name="accessing-memory-optimized-tables-using-interpreted-transact-sql"></a>Acceso a tablas con optimización para memoria mediante Transact-SQL interpretado
  Salvo unas pocas excepciones, puede acceder a las tablas optimizadas para memoria con cualquier consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] u operación DML (SELECT, INSERT, UPDATE o DELETE), lotes ad hoc y módulos de SQL como, por ejemplo, procedimientos almacenados, funciones con valores de tabla, desencadenadores y vistas.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado hace referencia a procedimientos almacenados o lotes de [!INCLUDE[tsql](../../includes/tsql-md.md)] distintos de un procedimiento almacenado compilado de forma nativa. El acceso de [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado a las tablas optimizadas para memoria se conoce como acceso de interoperabilidad.  
  
 También se puede tener acceso a las tablas con optimización para memoria mediante un procedimiento almacenado compilado de forma nativa. Los procedimientos almacenados compilados de forma nativa se recomiendan para las operaciones OLTP donde el rendimiento es un factor crítico.  
  
 El acceso interpretado de [!INCLUDE[tsql](../../includes/tsql-md.md)] se recomienda en estos casos:  
  
-   Consultas ad hoc y tareas administrativas.  
  
-   Consultas de notificación, que suelen usar construcciones no disponibles en los procedimientos almacenados compilados de forma nativa (como funciones de ventana).  
  
-   Para migrar componentes esenciales para el rendimiento de su aplicación a tablas optimizadas para memoria, con cambios mínimos en el código de la aplicación (o sin ningún cambio). Puede ver mejoras en el rendimiento si se migran las tablas. Si después migra los procedimientos almacenados a procedimientos almacenados compilados de forma nativa, puede ver una mejora adicional del rendimiento.  
  
-   Cuando no hay disponible una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] para los procedimientos almacenados compilados de forma nativa.  
  
 Las siguientes construcciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] no se admiten en los procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado que acceden a los datos de tablas optimizadas para memoria.  
  
|Área|No compatible|  
|----------|-----------------|  
|Acceso a tablas|TRUNCATE TABLE<br /><br /> MERGE (tabla optimizada para memoria como destino).<br /><br /> Cursores dinámicos y keyset (se degradan automáticamente en cursores estáticos).<br /><br /> Acceso de los módulos CLR, con la conexión de contexto.<br /><br /> Hacen referencia a una tabla optimizada para memoria desde una vista indizada.|  
|A través de bases de datos|Consultas entre bases de datos<br /><br /> Transacciones a través de bases de datos<br /><br /> Servidores vinculados|  
  
## <a name="table-hints"></a>Sugerencias de tabla  
 Para obtener más información acerca de las sugerencias de tabla, vea: [Sugerencias de tabla &#40;&#41;de Transact-SQL ](/sql/t-sql/queries/hints-transact-sql-table). Se agregó el aislamiento SNAPSHOT para admitir [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
 Las siguientes sugerencias de tabla no se admiten cuando se obtiene acceso a una tabla optimizada para memoria mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretado.  
  
|||||  
|-|-|-|-|  
|HOLDLOCK|IGNORE_CONSTRAINTS|IGNORE_TRIGGERS|NOWAIT|  
|PAGLOCK|READCOMMITTED|READCOMMITTEDLOCK|READPAST|  
|READUNCOMMITTED|ROWLOCK|SPATIAL_WINDOW_MAX_CELLS = *entero*|TABLOCK|  
|TABLOCKXX|UPDLOCK|XLOCK||  
  
 Al acceder a una tabla optimizada para memoria desde una transacción explícita o implícita con [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretado, debe incluir una sugerencia de tabla de nivel de aislamiento como SNAPSHOT, REPEATABLEREAD o SERIALIZABLE, o bien MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT. Para obtener más información, vea [instrucciones para los niveles de aislamiento de transacción con tablas optimizadas para memoria](memory-optimized-tables.md) y [opciones set de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
> [!NOTE]  
>  Una sugerencia de tabla de nivel de aislamiento no es necesaria para las tablas optimizadas para memoria por las consultas que se ejecutan en modo de confirmación automática.  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad de Transact-SQL con OLTP en memoria](transact-sql-support-for-in-memory-oltp.md)   
 [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)  
  
  
