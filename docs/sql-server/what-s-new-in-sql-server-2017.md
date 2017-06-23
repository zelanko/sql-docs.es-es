---
title: "¿Qué &#39; s de SQL Server de 2017 | Documentos de Microsoft"
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: aa08b5e7de9bb317fd781a98ee5d829431b92df6
ms.openlocfilehash: 66c9bc4f2cba20076c357d27fdfacbc767a94c5c
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="what39s-new-in-sql-server-2017"></a>¿Qué &#39; s de SQL Server de 2017
SQL Server 2017 representa un paso importante hacia convirtiendo SQL Server en una plataforma que proporciona opciones de lenguajes de desarrollo, los tipos de datos, local y en la nube y en sistemas operativos si se ponen la potencia de SQL Server para Linux, contenedores de Docker basados en Linux y Windows.

Este tema es un resumen de lo que es nuevo en la última versión de Community Technical Preview (CTP) y vínculos a más detallados ¿cuál es la nueva información de las áreas de características específicas.

![info_tip](../sql-server/media/info-tip.png) Ejecute SQL Server en Linux. Para obtener más información, vea:
-  [Novedades de SQL Server 2017 en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)
-  [SQL Server on Linux Documentation (Documentación de SQL Server en Linux)](https://docs.microsoft.com/sql/linux/)


**Pruébelo:**    
   -   [![Descargar desde el centro de evaluación](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477)  **[descargar Community Technology Preview SQL Server de 2017](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="whats-new-in-sql-server-2017-ctp-21-may-2017"></a>Novedades de CTP de SQL Server de 2017 2.1 (mayo de 2017)
### <a name="sql-server-database-engine"></a>Motor de base de datos de SQL Server  
- Un nuevo DMF, [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), se ha introducido para exponer atributos de nivel de resumen e información sobre los archivos de registro de transacciones; es útil para supervisar el estado del registro de transacciones.  
- Esta versión de CTP contiene correcciones de errores y mejoras de rendimiento para el motor de base de datos.
- Para obtener una lista detallada de 2017 mejoras CTP en versiones anteriores de CTP, consulte [What's New en SQL Server 2017 (motor de base de datos)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- SQL Server Reporting Services ya no está disponible para instalarse, mediante el programa de instalación de SQL Server a partir de CTP 2.1.
- Comentarios ahora están disponibles para los informes. Los comentarios permiten agregar perspectiva con lo que se encuentra en un informe y colaborar con otras personas de su organización. También puede incluir archivos adjuntos con el comentario.
- Para información más detallada sobre las novedades de SSRS, incluidos los detalles de las versiones anteriores, consulte [Novedades de Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 
- Para obtener información sobre el servidor de informes de Power BI, consulte [empezar a trabajar con el servidor de informes de Power BI](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

### <a name="sql-server-machine-learning-services"></a>Servicios de aprendizaje de máquina SQL Server
- No hay ninguna característica de servicios de aprendizaje de máquinas nuevas en esta versión de CTP.
- Para obtener más servicios de aprendizaje de máquina lo que nueva información, incluidos los detalles de los lanzamientos anteriores de CTP, consulte [What's New en servicios de aprendizaje de máquina de SQL Server](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).  

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- No hay características de SSAS nuevas en este CTP.  
- Para obtener más información sobre mejoras y correcciones de errores en esta versión, consulte [What's New en Analysis Services de SQL Server de 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
-   Ahora puede usar el **Use32BitRuntime** parámetro.
-   Se ha mejorado el rendimiento de inicio de sesión.
- Para obtener más SSIS lo que nueva información, incluidos los detalles de los lanzamientos anteriores de CTP, consulte [What's New en servicios de integración de SQL Server de 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md).  

![barra_horizontal](../sql-server/media/horizontal-bar.png)
## <a name="whats-new-in-sql-server-2017-ctp-20-april-2017"></a>Novedades de CTP de SQL Server de 2017 2.0 (abril de 2017)
### <a name="sql-server-database-engine"></a>Motor de base de datos de SQL Server
- **La reconstrucción de índices en línea reanudables**. La reconstrucción de índices en línea reanudable permite reanudar una operación de regeneración de índice en línea desde donde se detuvo después de un error. Por ejemplo, una conmutación por error a una réplica o una situación de espacio en disco insuficiente. Puede pausar y reanudar posteriormente una operación de regeneración de índice en línea. Por ejemplo, deberá liberar temporalmente recursos de sistemas con el fin de ejecutar una tarea de prioridad alta o completar la reconstrucción de índices en otra ventana de miniatous si las ventanas de mantenimiento disponible es demasiado corto para una tabla grande. Por último, la reconstrucción de índices en línea reanudables no requiere espacio de registro significativa, lo que le permite realizar el truncamiento del registro mientras se ejecuta la operación de regeneración reanudables. Vea [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) y [directrices para operaciones de índice en línea](../relational-databases/indexes/guidelines-for-online-index-operations.md).
- **Opción de IDENTITY_CACHE para ALTER DATABASE SCOPED CONFIGURATION**. Se ha agregado una nueva opción IDENTITY_CACHE a la instrucción ALTER DATABASE con ámbito de configuración T-SQL. Cuando esta opción se establece en OFF, se pueden evitar huecos en los valores de las columnas de identidad en caso de que un servidor se reinicia inesperadamente o conmuta por error a un servidor secundario. Vea [configuración de ALTER DATABASE en el ámbito](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).  
- CLR usa la seguridad de acceso del código (CAS) de .NET Framework, que ya no se admite como un límite de seguridad. Un ensamblado CLR creado con `PERMISSION_SET = SAFE` posible que pueda tener acceso a recursos externos del sistema, llamar a código no administrado y adquirir privilegios de sysadmin. A partir de [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)], `sp_configure` opción denominada `clr strict security` se introduce para mejorar la seguridad de los ensamblados CLR. `clr strict security`está habilitada de forma predeterminada y trata `SAFE` y `EXTERNAL_ACCESS` ensamblados como si se han marcado `UNSAFE`. El `clr strict security` se puede deshabilitar la opción de compatibilidad con versiones anteriores, pero no se recomienda. Microsoft recomienda que todos los ensamblados firmarse con un certificado o clave asimétrica con el correspondiente inicio de sesión que se ha concedido `UNSAFE ASSEMBLY` permiso en la base de datos maestra. Para obtener más información, consulte [seguridad estricta de CLR](../database-engine/configure-windows/clr-strict-security.md).  
- Capacidades de base de datos de gráfico para modelar las relaciones de varios a varios. Esto incluye nuevos [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) sintaxis para crear el nodo y tablas de borde y la palabra clave [coincidencia](../t-sql/queries/match-sql-graph.md) para las consultas. Para obtener más información, consulte [gráfico procesamiento con SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md).   
- El ajuste automático es una característica de base de datos que proporciona una visión general de la consulta posible problemas de rendimiento, pueden recomendar soluciones y corrección identifica automáticamente problemas. El ajuste automático [!INCLUDE[ssnoversion](../includes/ssnoversion.md)], le notifica cada vez que se detecta un posible problema de rendimiento y le permite aplicar acciones correctivas o permite el [!INCLUDE[ssde](../includes/ssde-md.md)] reparar automáticamente problemas de rendimiento. Para obtener más información, consulte [el ajuste automático](../relational-databases/automatic-tuning/automatic-tuning.md).  
-   Procesar por lotes modo unir adaptable para mejorar la calidad del plan (bajo 140 de compatibilidad de base de datos).
-   Ejecución intercalada de TVF de múltiples instrucciones T-SQL mejorar la calidad del plan (bajo 140 de compatibilidad de base de datos).
- Almacén de consultas ahora también realiza un seguimiento de información de resumen de estadísticas de espera. Categorías de estadísticas de espera por cada consulta en el almacén de consultas de seguimiento habilita el siguiente nivel de rendimiento experiencia de solución de problemas, lo que proporciona, incluso más, información sobre el rendimiento de la carga de trabajo y sus cuellos de botella conservando las ventajas claves de almacén de consultas.
- Compatibilidad con DTC para grupos de disponibilidad AlwaysOn para todas las transacciones entre bases de datos entre bases de datos que forman parte del grupo de disponibilidad, incluidas las bases de datos que forman parte de la misma instancia. Para obtener más información, vea [transacciones - grupos de disponibilidad AlwaysOn y creación de reflejo de base de datos](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)
- Una nueva columna **modified_extent_page_count** se incorporó en [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) para realizar un seguimiento de los cambios diferenciales de cada archivo de base de datos de la base de datos.
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) ahora admite la carga de una tabla en un grupo de archivos que no sea un grupo de archivos predeterminado del usuario mediante el **ON** (palabra clave).
- El programa de instalación de SQL Server permite especificar el tamaño del archivo de tempdb inicial hasta **256 GB (262.144 MB)** por cada archivo con una advertencia si el tamaño del archivo se establece en valor mayor que **1 GB** y si IFI no está habilitado.
- Una nueva vista de administración dinámica (DMV) [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) se introdujo para realizar el seguimiento de uso del almacén de versión por base de datos.
- Una nueva DMV [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) se introduce para exponer la información de VLF similar a DBCC LOGINFO.
- Las tablas temporales con versión del sistema admiten ahora CASCADE UPDATE y eliminación en cascada.
- Este CTP contiene correcciones de errores para el Motor de base de datos.
- Para obtener una lista detallada de 2017 mejoras CTP en versiones anteriores de CTP, consulte [What's New en SQL Server 2017 (motor de base de datos)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).   

### <a name="sql-server-machine-learning-services"></a>Servicios de aprendizaje de máquina SQL Server
- SQL Server R Services tiene un nuevo nombre para reflejar la compatibilidad con el lenguaje de Python en CTP 2.0. Ahora puede usar servicios de aprendizaje de máquina (en bases de datos) de SQL Server para ejecutar scripts de R o Python en SQL Server. O bien, puede instalar el servidor de aprendizaje de máquina (independiente) de Microsoft para implementar y usar modelos de R y Python que no requieren SQL Server. 
- Ambas plataformas incluyen nuevos algoritmos de MicrosoftML de aprendizaje automático de distribuida y la versión más reciente de Microsoft R (versión 9.1.0).
- Para obtener más información, consulte [What's new para el aprendizaje automático](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).

![barra_horizontal](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-14-march-2017"></a>Novedades de CTP de SQL Server de 2017 1.4 (marzo de 2017)
### <a name="sql-server-database-engine"></a>Motor de base de datos de SQL Server
- No hay nuevas características del Motor de base de datos en esta versión de CTP.
- Este CTP contiene correcciones de errores para el Motor de base de datos.
- Para obtener una lista detallada de 2017 mejoras CTP en versiones anteriores de CTP, consulte [What's New en SQL Server 2017 (motor de base de datos)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

### <a name="sql-server-r-services"></a>SQL Server R Services
- No hay características nuevas de R Services en esta versión de CTP.
- Para obtener información más detallada sobre las novedades de R Services, incluidos los detalles de las versiones de CTP anteriores, consulte [Novedades de SQL Server R Services](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md).  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- No hay características nuevas de SSRS en esta versión de CTP.
- Para información más detallada sobre las novedades de SSRS, incluidos los detalles de las versiones anteriores, consulte [Novedades de Reporting Services](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- No hay características de SSAS nuevas en este CTP.  
- Para obtener más información, incluidas las novedades de Analysis Services en las últimas versiones de vista previa de SSDT y SSMS, vea [What's New en Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- No hay características nuevas de SSIS en esta versión de CTP.
- Para obtener más SSIS lo que nueva información, incluidos los detalles de los lanzamientos anteriores de CTP, consulte [What's New en servicios de integración de 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md).  

![barra_horizontal](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-13-february-2017"></a>Novedades de CTP de SQL Server de 2017 1.3 (febrero de 2017)
### <a name="sql-server-database-engine"></a>Motor de base de datos de SQL Server
- Mejoras en el rendimiento del punto de comprobación indirecto.
- Se agregó compatibilidad con grupos de disponibilidad sin clúster.
- Se agregó la configuración de los grupos de disponibilidad de confirmación de réplica mínima.
- Los grupos de disponibilidad ahora pueden funcionar entre Windows y Linux para habilitar las migraciones y pruebas entre distintos sistemas operativos.
- Se agregó compatibilidad de directiva de retención de las tablas temporales. Para obtener más información, consulte [administrar retención de datos históricos en las tablas temporales con versión del sistema](../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md#using-temporal-history-retention-policy-approach).
- Nuevo DMV SYS.DM_DB_STATS_HISTOGRAM.
- Almacén de columnas no clúster en línea generación de índice y vuelva a generar compatibilidad agregada
- Cinco vistas de administración dinámica para devolver información sobre el proceso Linux. Para más información, consulte [Vistas de administración dinámica del proceso Linux](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md).   
- [sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) se agregó para examinar las estadísticas.

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- Sugerencias de codificación: una característica avanzada que se usa para optimizar el procesamiento (actualización de datos) de modelos tabulares en memoria de gran tamaño. Para obtener más información, consulte [What's New en Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md). 


![barra_horizontal](../sql-server/media/horizontal-bar.png)

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) Comunicación con el equipo de ingeniería de SQL Server 
- [Stack Overflow (etiqueta SQL Server)](http://stackoverflow.com/questions/tagged/sql-server)
- [Foros de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect: informar sobre errores y solicitar características](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit: debate general sobre R](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>Vea también    
- ![Notas de la versión](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) [notas de la versión SQL Server de 2017](../sql-server/sql-server-2017-release-notes.md). 
- [Características compatibles por edición](https://msdn.microsoft.com/library/cc645993.aspx)
- [Requisitos de hardware y software para instalar](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [Asistente para la instalación de SQL Server](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [Instalar las actualizaciones de mantenimiento de SQL Server](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)

