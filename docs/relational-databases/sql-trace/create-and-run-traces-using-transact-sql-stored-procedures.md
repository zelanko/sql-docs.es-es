---
title: Crear y ejecutar seguimientos mediante procedimientos almacenados de Transact-SQL
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3d1c5a85072bec1fc304156268680c201ad2245e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "74095643"
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>Crear y ejecutar seguimientos mediante procedimientos almacenados de Transact-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Consulte también  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
