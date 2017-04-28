---
title: "Creación y ejecución de seguimientos mediante procedimientos almacenados de Transact-SQL | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0af5c400a4973f711b2b3162f6fa05ca0371adeb
ms.lasthandoff: 04/11/2017

---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>Crear y ejecutar seguimientos mediante procedimientos almacenados de Transact-SQL
  El proceso de creación de trazas con Seguimiento de SQL varía en función de si el usuario crea y ejecuta su seguimiento mediante el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] de Microsoft o mediante procedimientos almacenados del sistema.  
  
 Como alternativa al [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], se pueden utilizar procedimientos almacenados del sistema de [!INCLUDE[tsql](../../includes/tsql-md.md)] para crear y ejecutar seguimientos. El proceso de creación de trazas mediante procedimientos almacenados del sistema es el siguiente:  
  
1.  Cree un seguimiento mediante **sp_trace_create**.  
  
2.  Agregue eventos con **sp_trace_setevent**.  
  
3.  (Opcional) Establezca un filtro con **sp_trace_setfilter**.  
  
4.  Inicie el seguimiento con **sp_trace_setstatus**.  
  
5.  Detenga el seguimiento con **sp_trace_setstatus**.  
  
6.  Cierre el seguimiento con **sp_trace_setstatus**.  
  
    > [!NOTE]  
    >  El uso de procedimientos almacenados del sistema de [!INCLUDE[tsql](../../includes/tsql-md.md)] crea un seguimiento en el servidor, que garantiza que no se perderá ningún evento mientras haya espacio en el disco y no se produzcan errores de escritura. Si el disco se llena o tiene un error, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sigue ejecutándose, pero se detiene la traza. Si está establecida la opción **c2 audit mode** y hay un error de escritura, se detiene la traza y se cierra la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información sobre la opción **c2 audit mode** , vea [c2 audit mode (opción de configuración del servidor)](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Optimizar el seguimiento de SQL](../../relational-databases/sql-trace/optimize-sql-trace.md)|Contiene información acerca de cómo se pueden reducir los efectos de la traza en el rendimiento del sistema.|  
|[Filtrar un seguimiento](../../relational-databases/sql-trace/filter-a-trace.md)|Contiene información acerca del uso de filtros para la traza.|  
|[Limitar el tamaño de la tabla y el archivo de seguimiento](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md)|Contiene información acerca de cómo limitar el tamaño de los archivos y las tablas donde se escriben los datos de seguimiento. Tenga en cuenta que solo el [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] puede escribir información sobre el seguimiento en las tablas.|  
|[Programar seguimientos](../../relational-databases/sql-trace/schedule-traces.md)|Contiene información acerca de cómo establecer la hora de inicio y de finalización de la traza.|  
  
## <a name="see-also"></a>Vea también  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
