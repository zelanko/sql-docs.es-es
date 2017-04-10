---
title: "Novedades de SQL Server vNext | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: "craigg-msft"
ms.author: "craigg"
manager: "jhubbard"
caps.handback.revision: 65
---
# Novedades de SQL Server vNext
SQL Server vNext representa un paso importante para convertir SQL Server en una plataforma que permite elegir lenguajes de desarrollo, tipos de datos, instalaciones locales o en la nube y diversos sistemas operativos, ya que aporta la eficacia de SQL Server a Linux, contenedores de Docker basados en Linux y Windows.

Este tema contiene un resumen de las novedades de la versión más reciente de Community Technical Preview (CTP), así como vínculos a información más detallada sobre las novedades de las áreas de características específicas.

![info_tip](../sql-server/media/info-tip.png) Ejecute SQL Server en Linux. Para obtener más información, vea:
-  [What's new for SQL Server vNext on Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-whats-new) (Novedades de SQL Server vNext en Linux)
-  [SQL Server on Linux Documentation (Documentación de SQL Server en Linux)](https://docs.microsoft.com/en-us/sql/linux/)


**Pruébelo:**    
   -   [![Descargar desde el Centro de evaluación](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[Descargar SQL Server vNext Community Technology Preview](http://go.microsoft.com/fwlink/?LinkID=829477)**


## <a name="whats-new-in-sql-server-vnext-ctp-13-february-2017"></a>Novedades de SQL Server vNext CTP 1.3 (febrero de 2017)
### <a name="sql-server-database-engine"></a>Motor de base de datos de SQL Server
- Mejoras en el rendimiento del punto de comprobación indirecto.
- Se agregó compatibilidad con grupos de disponibilidad sin clúster.
- Se agregó la configuración de los grupos de disponibilidad de confirmación de réplica mínima.
- Los grupos de disponibilidad ahora pueden funcionar entre Windows y Linux para habilitar las migraciones y pruebas entre distintos sistemas operativos.
- Se agregó compatibilidad con la directiva de retención de tablas temporales.
- Nuevo DMV SYS.DM_DB_STATS_HISTOGRAM.
- Se agregó compatibilidad con compilación y recompilación de índice de almacén de columnas no en clúster en línea.
- Cinco vistas de administración dinámica para devolver información sobre el proceso Linux. Para más información, consulte [Vistas de administración dinámica del proceso Linux](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md).   
- [sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) se agregó para examinar las estadísticas.

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- Sugerencias de codificación: una característica avanzada que se usa para optimizar el procesamiento (actualización de datos) de modelos tabulares en memoria de gran tamaño. Para más información, consulte [Novedades de Analysis Services vNext](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md). 

## <a name="whats-new-in-sql-server-vnext-ctp-12-january-2017"></a>Novedades de SQL Server vNext CTP 1.2 (enero de 2017)
### <a name="sql-server-database-engine"></a>Motor de base de datos de SQL Server
- Compatibilidad con compilación y recompilación de índices en línea para índices de almacén de columnas no en clúster.
- Este CTP también contiene corrección de errores para el motor de base de datos.
- Para una lista detallada de las mejoras de vNext CTP de las versiones anteriores de CTP, consulte [Novedades de SQL Server vNext (motor de base de datos)](../database-engine/configure-windows/what-s-new-in-sql-server-vnext-database-engine.md).

### <a name="sql-server-r-services"></a>SQL Server R Services
- No hay características nuevas de R Services en esta versión de CTP.
- Para obtener información más detallada sobre las novedades de R Services, incluidos los detalles de las versiones de CTP anteriores, consulte [Novedades de SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md).  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- No hay características nuevas de SSRS en esta versión de CTP.
- Para información más detallada sobre las novedades de SSRS, incluidos los detalles de las versiones anteriores, consulte [Novedades de Reporting Services](../reporting-services/novedades-de-sql-server-reporting-services-ssrs.md). 

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- No hay características de SSAS nuevas en este CTP.  
- Para obtener más información, consulte [What's New in Analysis Services vNext](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md) (Novedades de Analysis Services vNext).  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- No hay características nuevas de SSIS en esta versión de CTP.
- Para obtener información más detallada sobre las novedades de SSIS, incluidos los detalles de las versiones de CTP anteriores, consulte [What's New in Integration Services vNext](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md) (Novedades de Integration Services vNext).  

### <a name="master-data-services-mds"></a>Master Data Services (MDS)
- No hay características nuevas de Master Data Services en esta versión de CTP.

##  <a name="infotipimageshiproominfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Comunicación con el equipo de ingeniería de SQL Server 
- [Stack Overflow (etiqueta SQL Server)](http://stackoverflow.com/questions/tagged/sql-server)
- [Foros de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: informar sobre errores y solicitar características](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: debate general sobre R](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>Vea también    
 + [![Notas de la versión](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png)](SQL%20Server%20vNext%20Release%20Notes.md) [Notas de la versión de SQL Server vNext](../sql-server/sql-server-vnext-release-notes.md). 
+ [Características compatibles por edición](https://msdn.microsoft.com/library/cc645993.aspx)
 + [[Requisitos de hardware y software para instalar](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)](Hardware%20and%20Software%20Requirements%20for%20Installing%20SQL%20Server%202016.md)
 + [Asistente para la instalación](../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)
 
 + [Instalación inicial y de servicio](Setup%20and%20Servicing%20Installation.md)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)