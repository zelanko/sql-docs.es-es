---
title: "Información general de almacenamiento de datos paralelo"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Este tema explica el software del dispositivo y los componentes de software de dispositivo no es de sistema de la plataforma de análisis."
ms.date: 01/05/2017
ms.topic: article
ms.assetid: db0c4a43-a66d-4c44-ab91-791c5785f71c
caps.latest.revision: "20"
ms.openlocfilehash: f2b6708f6e82340c971bdd3a6cc0cdb7e67f2d65
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="parallel-data-warehouse-overview"></a>Información general de almacenamiento de datos paralelo
Este tema explica el software del dispositivo y los componentes de software de dispositivo no es de sistema de la plataforma de análisis.  
  
<!-- MISSING LINKS

To learn more about Analytics Platform System, see:  
  
-   [Analytics Platform System architecture](architecture-overview.md)  
  
-   [Distributed and Replicated Tables &#40;SQL Server PDW&#41;](../sqlpdw/distributed-and-replicated-tables-sql-server-pdw.md)  
  
-   [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  
  
-   [Clustered Columnstore Indexes &#40;SQL Server PDW&#41;](../sqlpdw/clustered-columnstore-indexes-sql-server-pdw.md)  
  
-   [Query Process &#40;SQL Server PDW&#41;](../sqlpdw/query-process-sql-server-pdw.md)  
  
-   [Minimum and Maximum Values &#40;SQL Server PDW&#41;](../sqlpdw/minimum-and-maximum-values-sql-server-pdw.md)  

-->
   
  
![Software de almacenamiento de datos en paralelo](media/parallel-data-warehouse-software.png "software de almacenamiento de datos paralelos")  
  
## <a name="sec1"></a>Software de dispositivo: consulta de procesamiento y el almacenamiento de datos de usuario  
  
### <a name="control-node"></a>Nodo de control  
Motor MPP  
El motor de MPP es el cerebro del sistema masivo paralelas de procesamiento (MPP). Realiza las operaciones siguientes:  
  
-   Crea planes de consulta en paralelo y coordina la ejecución de consultas en paralelo de los nodos.  
  
-   Almacena y coordina los datos de configuración y metadatos para todas las bases de datos.  
  
-   Administra la autorización y autenticación de base de datos de SQL Server PDW.  
  
-   Realiza un seguimiento de estado del hardware y software.  
  
### <a name="data-movement-service-dms"></a>Servicio de movimiento de datos (DMS)  
Servicio de movimiento de datos (DMS) forma parte de la "salsa secreta" de PDW. Realiza las operaciones siguientes:  
  
-   Transfiere datos desde y hacia los nodos de SQL Server PDW.  
  
-   Procesos de operaciones que requieren la transferencia de datos entre los nodos de consulta.  
  
-   Mejora el rendimiento de las consultas mediante la optimización de velocidades de transferencia de datos.  
  
### <a name="admin-console"></a>Consola de administración  
La consola de administración es una aplicación web que presenta el estado del dispositivo, el estado y la información de rendimiento.  
  
### <a name="configuration-manager"></a>Administrador de configuración  
El Administrador de configuración (dwconfig.exe), es la herramienta que utilizan los administradores del equipo para configurar el sistema de la plataforma de análisis.  
  
### <a name="control-node-databases"></a>Bases de datos del nodo de control  
SQL Server administra todas las bases de datos en el nodo de Control.  
  
-   La base de datos de Shell administra los metadatos para todas las bases de datos de usuario distribuida.  
  
-   TempDB contiene los metadatos de todas las tablas temporales de usuario en el dispositivo.  
  
-   Maestro es la tabla maestra de SQL Server en el nodo de Control.  
  
### <a name="compute-node"></a>Nodo de ejecución  
Los nodos de proceso son las unidades de almacenamiento y de procesamiento paralelo de datos. Tienen almacenamiento de conexión directa y usar SQL Server para administrar los datos de usuario.  
  
### <a name="data-movement-service-dms"></a>Servicio de movimiento de datos (DMS)  
Servicio de movimiento de datos (DMS) se ejecuta en cada nodo de proceso para hacer lo siguiente:  
  
-   Como parte del procesamiento de consultas en paralelo, DMS transferir datos hacia y desde otros nodos de equipo y el nodo de Control.  
  
-   DMS, que se ejecuta en cada nodo de proceso, recibe las cargas de datos en paralelo. Se cargan datos en paralelo directamente desde el servidor de carga para los nodos de proceso  
  
-   DMS transfiere los datos de cada nodo de ejecución directamente en el servidor de copia de seguridad.  
  
-   Con PolyBase, DMS transfiere datos desde y hacia un clúster de Hadoop externo o la HDInsight región en el dispositivo.  
  
### <a name="compute-node-databases"></a>Las bases de datos del nodo de proceso 
Cada nodo de proceso ejecuta una instancia de SQL Server para procesar las consultas y administrar los datos de usuario.  
  
## <a name="appliance-fabric"></a>Tejido de dispositivo  
El entramado de dispositivo proporciona el sistema operativo, los servicios y la infraestructura de red para el dispositivo.  
  
### <a name="domain-controller"></a>Controlador de dominio  
Servicios de dominio de Active Directory (AD) (DS)  
Sistema de la plataforma de análisis realiza la autenticación entre los nodos del sistema de la plataforma de análisis y administra la autenticación de inicios de sesión de autenticación de Windows de PDW de SQL Server.  
  
Servicio DNS  
Servicio de nombres de dominio (DNS) de Windows resuelve los nombres de dominio en direcciones IP para el dispositivo de sistema de la plataforma de análisis.  
  
### <a name="windows-deployment-service"></a>Servicios de implementación de Windows  
Servicio de implementación de Windows (WDS) se implementa el sistema operativo Windows Server en el dispositivo. Se implementa en cada host y máquina virtual en el dispositivo.  
  
El servicio DHCP crea direcciones IP para que los hosts en el dominio del equipo pueden unirse a la red de dispositivo sin necesidad de una dirección IP configurada previamente.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Sistema de la plataforma de análisis usa la virtualización para lograr una alta disponibilidad. Virtual Machine Manager hospeda System Center para implementar el sistema operativo en los hosts físicos.  
  
Windows Server Update Services (WSUS) para aplicar o quitar las actualizaciones de Windows en todos los hosts y máquinas virtuales.  
  
### <a name="windows-server"></a>Windows Server  
Todos los hosts y máquinas virtuales en el dispositivo ejecutan el sistema operativo Windows Server.  
  
### <a name="failover-clustering"></a>Agrupación en clústeres de conmutación por error  
Agrupación en clústeres de conmutación por error de Windows proporciona la capacidad para reiniciar los procesos en un host pasivo en el caso de que se produce un error en un host.  
  
### <a name="storage-spaces"></a>Espacios de almacenamiento  
Espacios de almacenamiento de Windows administra los datos de usuario como un bloque de almacenamiento para un grupo pequeño de nodos de proceso. Si se produce un error en un nodo de proceso, los datos aún están accesibles a través de otro nodo de proceso en el grupo.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server proporciona una solución de virtualización confiable y simple. Sistema de la plataforma de análisis usa virtualización: para equilibrar los recursos de CPU y para proporcionar alta disponibilidad para los nodos PDW y dispositivo componentes del tejido.  
  
## <a name="sec2"></a>Datos no relacionales
Tecnología de PolyBase que integra datos de SQL Server PDW con datos externos de Hadoop. Pueden almacenar los datos de Hadoop en cualquiera de estos orígenes de datos de Hadoop:  
  
-   Hortonworks para Linux o Windows Server  
  
-   Cloudera en Linux  
  
-   HDInsight con puntos de acceso  
  
-   HDInsight los datos almacenados en el Blob de almacenamiento de Azure  
  
## <a name="query-tools"></a>Herramientas de consulta   
  
Las consultas se escriben con Transact\-SQL modificado para adaptarlos a la naturaleza MPP de las consultas. Todas las consultas se envían al nodo de Control que genera un plan de consulta en paralelo para ejecutar la consulta en todos los nodos de proceso.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
Herramientas de datos de SQL Server se ejecuta dentro de Visual Studio y es nuestra herramienta de interfaz gráfica de usuario recomendada para el envío de consultas de SQL Server PDW. Es similar a SQL Server Management Studio, ya que permite navegar por un explorador de objetos.  
  
Si ya no tiene Visual Studio, puede descargar las herramientas que necesita de forma gratuita. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>Herramienta de consulta de línea de comandos de SQLCMD  
Sqlcmd es la herramienta de línea de comandos de SQL Server para ejecutar Transact\-SQL instrucciones y comandos del sistema. Funciona con PDW de SQL Server y es nuestra herramienta de línea de comandos recomendado para consultar SQL Server PDW. Con sqlcmd puede ejecutar Transact\-instrucciones de SQL forma interactiva desde la línea de comandos, como un archivo por lotes, o desde Windows PowerShell.  
  
<!-- MISSING LINKS

If you don’t have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
Puede usar servicios de integración para consulta PDW de SQL Server. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>Servidor vinculado  
Mediante el uso de una conexión de servidor vinculado de SQL Server, puede usar SQL Server para enviar Transact\-instrucciones SQL para SQL Server PDW. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>Herramientas de Business Intelligence
  
Analysis Services  
SQL Server PDW es un origen de datos válido para las bases de datos de Analysis Services y modelos de PowerPivot de Excel. Mediante el proveedor OLE DB, puede configurar un cubo de Analysis Services para usar procesamiento analítico en línea multidimensional (MOLAP) o almacenamiento de procesamiento analítico en línea relacional (ROLAP).  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>Generador de informes  
Puede usar SQL Server PDW como un origen de datos de SQL Server para los informes que se desarrollan para Reporting Services usando el generador de informes de SQL Server. También puede utilizar PDW de SQL Server como origen de SQL Server para los modelos de informe. Mediante el Administrador de informes o la API de servidor de informes, puede generar un modelo de una base de datos de SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot para Excel  
Puede conectarse a SQL Server PDW con PowerPivot para Excel, una descarga gratuita que amplía las capacidades de análisis de datos de Excel de manera significativa.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>Herramientas de carga 
  
### <a name="integration-services"></a>Integration Services  
Instalar a adaptadores de destino de PDW específicos que le permiten utilizar SQL ServerIntegration Services para cargar datos en SQL Server PDW.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>Cargador de la línea de comandos de dwloader  
dwloader es una herramienta de línea de comandos de carga que carga datos en paralelo desde el servidor de carga para los nodos de proceso de SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase para la integración de Hadoop  
Con la tecnología de PolyBase, puede cargar los datos no relacionales desde un clúster de Hadoop en una tabla relacional de SQL Server PDW. Los datos de Hadoop pueden encontrarse en una referencia externa clúster de Hadoop, la región de HDI de APS, o en un Blob de almacenamiento de Azure.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>Restauración y copia de seguridad de base de datos  
SQL Server PDW usa Transact\-SQL base de datos de copia de seguridad y restaurar los comandos de copia de seguridad y restaurar bases de datos de usuario, en paralelo, a y desde un servidor de copia de seguridad. SQL Server PDW escribe la copia de seguridad en un directorio en un recurso compartido de archivos de Windows y, a continuación, del mismo modo restaura los datos desde un recurso compartido de archivos de Windows.  
  
Para obtener más información, consulte [Plan de copia de seguridad y la carga de Hardware](backup-and-loading-hardware.md) y [copias de seguridad y restaurar información general](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>Copia de la tabla remota  
La característica de copia de tabla remota permite copiar tablas de bases de datos de SQL Server PDW a las bases de datos de SMP SQL Server remotos de (que no sea de dispositivo). Esto habilita escenarios de concentrador y radio para PDW de SQL Server.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>Supervisión  
Sistema de la plataforma de análisis ofrece varias maneras para supervisar la actividad del dispositivo  
  
### <a name="admin-console"></a>Consola de administración  
La consola de administración permite ver el estado actual sobre el estado del dispositivo. Esto se ejecuta como una aplicación web en el nodo de Control y es accesible a través de https.  
  
Para obtener más información, vea [supervisar el dispositivo mediante la consola de administración &#40; Sistema de la plataforma de análisis &#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>Vistas del sistema  
La consola de administración se basa en consultas de vista del sistema. Puede consultar las vistas del sistema individualmente para obtener la parte concreta de la información que necesita.  

Para obtener más información, vea [supervisar el dispositivo mediante el uso de vistas del sistema &#40; Sistema de la plataforma de análisis &#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
Existen módulos de administración de System Center Operations Manager (SCOM) para SQL Server PDW. 

Para configurar el dispositivo para SCOM, consulte [supervisar el dispositivo mediante el uso de System Center Operations Manager &#40; Sistema de la plataforma de análisis &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
