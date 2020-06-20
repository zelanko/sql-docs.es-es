---
title: Modificar plantillas de seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- modifying trace templates
- SQL Server Profiler, templates
ms.assetid: 75b62a54-8d16-4599-bd2d-c42cfcc209f4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4a26d0a70f65b6ff60dcf42ffb98e67dc0d2b52d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040308"
---
# <a name="modify-trace-templates"></a>Modificar plantillas de seguimiento
  Puede modificar las plantillas que están guardadas en un archivo en el equipo local en el que se ejecuta el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] . También puede modificar plantillas derivadas de esos archivos. Al modificar plantillas existentes, edite las propiedades de la plantilla, como clases de evento y columnas de datos, en el mismo orden en que se definieron originalmente, en la pestaña **Selección de eventos** del cuadro de diálogo **Propiedades de seguimiento** . Puede agregar o quitar clases de eventos y columnas de datos, así como cambiar filtros. Después de modificar la plantilla, se crea una plantilla específica del usuario y la original se deja intacta. Para obtener más información, vea [Guardar seguimientos y plantillas de seguimiento](save-traces-and-trace-templates.md).  
  
 Es posible que tenga que derivar una plantilla de un archivo de seguimiento existente si no puede recordar (o no ha guardado) la plantilla original que se utilizó para crear el seguimiento o si desea volver a ejecutar el mismo seguimiento posteriormente. Si trabaja con seguimientos existentes, puede ver las propiedades, pero no modificarlas. Para modificar las propiedades, detenga o pause el seguimiento. Para obtener más información, vea [Derivar una plantilla a partir de un archivo o tabla de seguimiento &#40;SQL Server Profiler&#41;](sql-server-profiler.md) y [Derivar una plantilla a partir de un seguimiento en ejecución &#40;SQL Server Profiler&#41;](derive-a-template-from-a-running-trace-sql-server-profiler.md).  
  
 **Para crear una plantilla de seguimiento**  
  
 [Crear una plantilla de seguimiento &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)  
  
 **Para ejecutar un seguimiento desde una plantilla de seguimiento**  
  
 [Crear un seguimiento &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)  
  
 **Para modificar una plantilla de seguimiento**  
  
 [Usar SQL Server Profiler](../../database-engine/modify-a-trace-template-sql-server-profiler.md)  
  
 [Uso de Transact-SQL](../../relational-databases/sql-trace/modify-an-existing-trace-transact-sql.md)  
  
 **Para agregar o quitar eventos de una plantilla de seguimiento o de un archivo de seguimiento**  
  
 [Usar SQL Server Profiler](specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Uso de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar un seguimiento](start-a-trace.md)  
  
  
