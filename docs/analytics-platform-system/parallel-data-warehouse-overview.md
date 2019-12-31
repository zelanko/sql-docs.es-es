---
title: Componentes de almacenamiento de datos paralelos
description: En este artículo se explica el software del dispositivo y los componentes de software que no son de la aplicación de Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5e609585e464cb52b996f45c7d8c57aaffcd79fe
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400930"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>Componentes de almacenamiento de datos paralelos: Analytics Platform System
En este artículo se explica el software del dispositivo y los componentes de software que no son de la aplicación de Analytics Platform System.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![Software de almacenamiento de datos paralelos](media/parallel-data-warehouse-software.png "Software de almacenamiento de datos paralelos")  
  
## <a name="sec1"></a>Software de dispositivo: procesamiento de consultas y almacenamiento de datos de usuario  
  
### <a name="control-node"></a>nodo de control  
Motor MPP  
El motor MPP es el cerebro del sistema de procesamiento paralelo masivo (MPP). Hace lo siguiente:  
  
-   Crea planes de consulta paralelos y coordina la ejecución de consultas paralelas en los nodos de proceso.  
  
-   Almacena y coordina los metadatos y los datos de configuración de todas las bases de datos.  
  
-   Administra PDW de SQL Server la autenticación y autorización de bases de datos.  
  
-   Realiza un seguimiento del estado de hardware y software.  
  
### <a name="data-movement-service-dms"></a>Servicio de movimiento de datos (DMS)  
El servicio de movimiento de datos (DMS) forma parte de la "salsa secreta" de PDW. Hace lo siguiente:  
  
-   Transfiere datos hacia y desde los nodos de PDW de SQL Server.  
  
-   Procesa operaciones de consulta que requieren la transferencia de datos entre los nodos.  
  
-   Mejora el rendimiento de las consultas mediante la optimización de la velocidad de transferencia de datos.  
  
### <a name="admin-console"></a>Consola de administración  
La consola de administración es una aplicación web que presenta la información sobre el estado del dispositivo, el estado y el rendimiento.  
  
### <a name="configuration-manager"></a>Administrador de configuración  
El Configuration Manager (dwconfig. exe) es la herramienta que los administradores de dispositivos usan para configurar el sistema de plataforma de análisis.  
  
### <a name="control-node-databases"></a>Controlar las bases de datos de nodo  
SQL Server administra todas las bases de datos del nodo de control.  
  
-   La base de datos de Shell administra los metadatos de todas las bases de datos de usuario distribuidas.  
  
-   TempDB contiene los metadatos de todas las tablas temporales de usuario en el dispositivo.  
  
-   Master es la tabla maestra para SQL Server en el nodo de control.  
  
### <a name="compute-node"></a>Nodo de proceso  
Los nodos de proceso son unidades de almacenamiento y procesamiento de datos paralelos. Tienen almacenamiento conectado directo y usan SQL Server para administrar datos de usuario.  
  
### <a name="data-movement-service-dms"></a>Servicio de movimiento de datos (DMS)  
El servicio de movimiento de datos (DMS) se ejecuta en cada nodo de proceso para hacer lo siguiente:  
  
-   Como parte del procesamiento de consultas paralelas, DMS transfiere datos hacia y desde otros nodos de equipo y el nodo de control.  
  
-   DMS, que se ejecuta en cada nodo de proceso, recibe cargas de datos en paralelo. Los datos se cargan en paralelo directamente desde el servidor de carga a los nodos de proceso.  
  
-   DMS transfiere datos de cada nodo de proceso directamente al servidor de copia de seguridad.  
  
-   Con polybase, DMS transfiere datos hacia y desde un clúster de Hadoop externo o un Azure Storage Blob.  
  
### <a name="compute-node-databases"></a>Bases de datos de nodos de proceso 
Cada nodo de proceso ejecuta una instancia de SQL Server para procesar las consultas y administrar los datos de usuario.  
  
## <a name="appliance-fabric"></a>Tejido del dispositivo  
El tejido del dispositivo proporciona el sistema operativo, los servicios y la infraestructura de red para el dispositivo.  
  
### <a name="domain-controller"></a>Controlador de dominio  
Servicios de dominio de Active Directory (AD) (DS)  
Analytics Platform System realiza la autenticación entre los nodos del sistema de la plataforma de análisis y administra la autenticación de PDW de SQL Server inicios de sesión de autenticación de Windows.  
  
Servicio DNS  
El servicio de nombres de dominio (DNS) de Windows resuelve los nombres de dominio en direcciones IP para el dispositivo de sistema de plataforma de análisis.  
  
### <a name="windows-deployment-service"></a>Servicio de implementación de Windows  
El servicio de implementación de Windows (WDS) implementa el sistema operativo Windows Server en el dispositivo. Se implementa en todos los hosts y máquinas virtuales a través de la aplicación.  
  
El servicio DHCP crea direcciones IP para que los hosts dentro del dominio del dispositivo puedan unirse a la red del dispositivo sin tener una dirección IP preconfigurada.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Analytics Platform System usa la virtualización para lograr alta disponibilidad. El Virtual Machine Manager hospeda System Center para implementar el sistema operativo en los hosts físicos.  
  
Windows Server Update Services (WSUS) para aplicar o quitar actualizaciones de Windows en todos los hosts y máquinas virtuales.  
  
### <a name="windows-server"></a>Windows Server  
Todos los hosts y las máquinas virtuales del dispositivo ejecutan el sistema operativo Windows Server.  
  
### <a name="failover-clustering"></a>Clústeres de conmutación por error  
Los clústeres de conmutación por error de Windows proporcionan la capacidad de reiniciar procesos en un host pasivo en caso de que se produzca un error en un host.  
  
### <a name="storage-spaces"></a>Espacios de almacenamiento  
Los espacios de almacenamiento de Windows administran los datos de usuario como un bloque de almacenamiento para un pequeño grupo de nodos de proceso. Si se produce un error en un nodo de proceso, todavía se puede obtener acceso a los datos a través de otro nodo de proceso del grupo.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server proporciona una solución de virtualización sencilla y confiable. Analytics Platform System usa virtualizaciones para equilibrar los recursos de CPU y proporcionar alta disponibilidad para los nodos PDW y los componentes de fabric del dispositivo.  
  
## <a name="sec2"></a>Datos no relacionales
La tecnología de polybase integra PDW de SQL Server datos con datos de Hadoop externos. Los datos de Hadoop se pueden almacenar en cualquiera de estos orígenes de datos de Hadoop:  
  
-   Hortonworks distribución de Hadoop  
  
-   Distribución de Cloudera de Hadoop  
  
-   Datos almacenados en HDInsight en Azure Storage Blob  
  
## <a name="query-tools"></a>Herramientas de consulta   
  
Las consultas se escriben\-con Transact SQL modificado para ajustarse a la naturaleza MPP de las consultas. Todas las consultas se envían al nodo de control, que genera un plan de consulta paralelo para ejecutar la consulta en los nodos de proceso.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools se ejecuta dentro de Visual Studio y es nuestra herramienta de GUI recomendada para enviar consultas a PDW de SQL Server. Es similar a SQL Server Management Studio permitiéndole desplazarse por un explorador de objetos.  
  
Si aún no tiene Visual Studio, puede descargar las herramientas que necesita de forma gratuita. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>Herramienta de consulta de línea de comandos SQLCMD  
Sqlcmd es la SQL Server herramienta de línea de comandos para ejecutar\-instrucciones de Transact SQL y comandos del sistema. Funciona con PDW de SQL Server y es nuestra herramienta de línea de comandos recomendada para consultar PDW de SQL Server. Con SQLCMD, puede ejecutar instrucciones\-Transact-SQL de forma interactiva desde la línea de comandos, como un archivo por lotes o desde Windows PowerShell.  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Servicios de integración  
Puede usar Integration Services para consultar PDW de SQL Server. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>Servidor vinculado  
Mediante el uso de un SQL Server conexión de servidor vinculado, puede utilizar SQL Server\-para enviar instrucciones Transact SQL a PDW de SQL Server. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>Herramientas de inteligencia empresarial
  
### <a name="analysis-services"></a>Analysis Services  
PDW de SQL Server es un origen de datos válido para las bases de datos de Analysis Services y los modelos de Excel PowerPivot. Con el proveedor de OLE DB, puede configurar un cubo de Analysis Services para utilizar el procesamiento analítico en línea multidimensional (MOLAP) o el almacenamiento de procesamiento analítico en línea relacional (ROLAP).  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>Generador de informes  
Puede usar PDW de SQL Server como un origen de datos SQL Server para los informes que desarrolle para Reporting Services con SQL Server Generador de informes. También puede utilizar PDW de SQL Server como origen de SQL Server para los modelos de informe. Con Administrador de informes o la API del servidor de informes, puede generar un modelo a partir de una base de datos de PDW de SQL Server.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot para Excel  
Puede conectarse a PDW de SQL Server con PowerPivot para Excel, una descarga gratuita que amplía considerablemente las capacidades de análisis de datos de Excel.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>Cargando herramientas 
  
### <a name="integration-services"></a>Servicios de integración  
Instale adaptadores de destino específicos de PDW que le permitan usar SQL ServerIntegration Services para cargar datos en PDW de SQL Server.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>Cargador de línea de comandos de dwloader  
dwloader es una herramienta de carga de línea de comandos que carga datos en paralelo desde el servidor de carga en los nodos de proceso de PDW de SQL Server. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>Polybase para la integración de Hadoop  
Con la tecnología de polybase, puede cargar datos no relacionales desde un clúster de Hadoop en una tabla relacional en PDW de SQL Server. Los datos de Hadoop pueden encontrarse en un clúster de Hadoop externo o en un Azure Storage Blob.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>Copia de seguridad y restauración de bases de datos  
PDW de SQL Server usa comandos de copia de seguridad y restauración de bases de datos de Transact-SQL para realizar copias de seguridad y restaurar bases de datos de usuario, en paralelo, en y desde un servidor de copia de seguridad. PDW de SQL Server escribe la copia de seguridad en un directorio de un recurso compartido de archivos de Windows y, a continuación, restaura los datos de un recurso compartido de archivos de Windows.  
  
Para obtener más información, vea [información general sobre](backup-and-restore-overview.md) el [plan de copia de seguridad y carga de hardware](backup-and-loading-hardware.md) y restauración  
  
## <a name="remote-table-copy"></a>Copia de tabla remota  
La característica de copia de tabla remota permite copiar tablas de PDW de SQL Server bases de datos en bases de datos de SQL Server SMP remotos (no de la aplicación). Esto permite escenarios de concentrador y radio para PDW de SQL Server.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>Supervisión  
Analytics Platform System tiene varias maneras de supervisar la actividad del dispositivo  
  
### <a name="admin-console"></a>Consola de administración  
La consola de administración permite ver el estado actual sobre el estado del dispositivo. Esto se ejecuta como una aplicación web en el nodo de control y es accesible a través de HTTPS.  
  
Para más información, consulte [supervisión del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>Vistas del sistema  
La consola de administración de se basa en las consultas de la vista del sistema. Puede consultar las vistas del sistema individualmente para obtener la parte específica de la información que necesita.  

Para obtener más información, consulte [supervisión del dispositivo mediante las vistas del sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
Hay módulos de administración de System Center Operations Manager (SCOM) para PDW de SQL Server. 

Para configurar el dispositivo para SCOM, consulte [supervisión del dispositivo mediante System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
