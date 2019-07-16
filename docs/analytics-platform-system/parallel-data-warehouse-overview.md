---
title: 'Componentes de almacenamiento de datos: Analytics Platform System en paralelo | Microsoft Docs'
description: En este artículo se explica el software del dispositivo y los componentes de software que no sea de dispositivo de Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 87525a741c1d0081b366394c0c5dd1b152ad15f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960476"
---
# <a name="parallel-data-warehouse-components---analytics-platform-system"></a>Componentes de almacenamiento de datos: Analytics Platform System en paralelo
En este artículo se explica el software del dispositivo y los componentes de software que no sea de dispositivo de Analytics Platform System.  
  
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
  
## <a name="sec1"></a>Software de dispositivo: consulta de procesamiento y almacenamiento de datos de usuario  
  
### <a name="control-node"></a>Nodo de control  
Motor de MPP  
El motor de MPP es el cerebro del sistema de procesamiento paralelo masivo (MPP). Realiza las operaciones siguientes:  
  
-   Crea planes de consulta paralelos y coordina la ejecución de consultas en paralelo en los nodos de proceso.  
  
-   Almacena y coordina los datos de configuración y metadatos para todas las bases de datos.  
  
-   Administra la autorización y autenticación de base de datos de SQL Server PDW.  
  
-   Realiza un seguimiento del estado del hardware y software.  
  
### <a name="data-movement-service-dms"></a>Servicio de movimiento de datos (DMS)  
Servicio de movimiento de datos (DMS) es parte de la "salsa secreta" de PDW. Realiza las operaciones siguientes:  
  
-   Transfiere datos desde y hacia los nodos de PDW de SQL Server.  
  
-   Los procesos de operaciones de consulta que requieren la transferencia de datos entre los nodos.  
  
-   Mejora el rendimiento de las consultas al optimizar la velocidad de transferencia de datos.  
  
### <a name="admin-console"></a>Consola de administración  
La consola de administración es una aplicación web que presenta el estado del dispositivo, el estado y la información de rendimiento.  
  
### <a name="configuration-manager"></a>Administrador de configuración  
El Administrador de configuración (dwconfig.exe), es la herramienta que utilizan los administradores de equipo para configurar Analytics Platform System.  
  
### <a name="control-node-databases"></a>Bases de datos del nodo de control  
SQL Server administra todas las bases de datos en el nodo de Control.  
  
-   La base de datos de Shell administra los metadatos para todas las bases de datos de usuario distribuida.  
  
-   TempDB contiene los metadatos para todas las tablas temporales del usuario en todo el dispositivo.  
  
-   Master es la tabla maestra de SQL Server en el nodo de Control.  
  
### <a name="compute-node"></a>Nodo de proceso  
Los nodos de proceso son las unidades de almacenamiento y de procesamiento paralelo de datos. Tienen almacenamiento conectado directamente y usar SQL Server para administrar los datos de usuario.  
  
### <a name="data-movement-service-dms"></a>Servicio de movimiento de datos (DMS)  
Servicio de movimiento de datos (DMS) se ejecuta en cada nodo de proceso para hacer lo siguiente:  
  
-   Como parte del procesamiento de consultas en paralelo, DMS transferir datos hacia y desde otros nodos de equipo y el nodo de Control.  
  
-   DMS, que se ejecuta en cada nodo de proceso recibe las cargas de datos en paralelo. Se cargan datos en paralelo directamente desde el servidor de carga para los nodos de proceso  
  
-   DMS transfiere datos desde cada nodo de cálculo directamente en el servidor de copia de seguridad.  
  
-   Uso de PolyBase, DMS transfiere los datos hacia y desde un clúster de Hadoop externo o Azure Storage Blob.  
  
### <a name="compute-node-databases"></a>Las bases de datos del nodo de proceso 
Cada nodo de proceso ejecuta una instancia de SQL Server para procesar las consultas y administrar datos de usuario.  
  
## <a name="appliance-fabric"></a>Tejido del dispositivo  
El tejido de la aplicación proporciona el sistema operativo, servicios e infraestructura de red para el dispositivo.  
  
### <a name="domain-controller"></a>Controlador de dominio  
Servicios de dominio de Active Directory (AD) (DS)  
Analytics Platform System realiza la autenticación entre los nodos de Analytics Platform System y administra la autenticación de inicios de sesión de autenticación de Windows de PDW de SQL Server.  
  
Servicio DNS  
Servicio de nombres de dominio (DNS) de Windows resuelve los nombres de dominio en direcciones IP para la aplicación Analytics Platform System.  
  
### <a name="windows-deployment-service"></a>Servicios de implementación de Windows  
Servicio de implementación de Windows (WDS) implementa el sistema operativo Windows Server en el dispositivo. Se implementa en cada host y máquina virtual en todo el dispositivo.  
  
El servicio DHCP crea las direcciones IP para que los hosts en el dominio del equipo pueden unirse a la red del dispositivo sin tener una dirección IP configurada previamente.  
  
### <a name="virtual-machine-manager"></a>Virtual Machine Manager  
Analytics Platform System usa la virtualización para lograr una alta disponibilidad. El Virtual Machine Manager hospeda System Center para implementar el sistema operativo en los hosts físicos.  
  
Windows Server Update Services (WSUS) para aplicar o quitar las actualizaciones de Windows en todos los hosts y máquinas virtuales.  
  
### <a name="windows-server"></a>Windows Server  
Todos los hosts y máquinas virtuales en el dispositivo ejecutan el sistema operativo Windows Server.  
  
### <a name="failover-clustering"></a>Agrupación en clústeres de conmutación por error  
Agrupación en clústeres de conmutación por error de Windows proporciona la capacidad para reiniciar los procesos en un host pasivo en caso de que se produce un error en un host.  
  
### <a name="storage-spaces"></a>Espacios de almacenamiento  
Espacios de almacenamiento de Windows administra los datos de usuario como un bloque de almacenamiento para un grupo pequeño de nodos de proceso. Si se produce un error en un nodo de proceso, los datos están siendo accesibles a través de otro nodo de proceso en el grupo.  
  
### <a name="hyper-v"></a>Hyper-V  
Microsoft Hyper-V Server proporciona una solución de virtualización confiable y simple. Analytics Platform System usa virtualización para equilibrar los recursos de CPU y para proporcionar alta disponibilidad para los nodos PDW y el dispositivo de los componentes del tejido.  
  
## <a name="sec2"></a>Datos no relacionales
La tecnología PolyBase integra datos de SQL Server PDW con datos externos de Hadoop. Los datos de Hadoop pueden almacenarse en cualquiera de estos orígenes de datos de Hadoop:  
  
-   Distribución de Hortonworks Hadoop  
  
-   Cloudera distribución de Hadoop  
  
-   Datos de HDInsight almacenados en Azure Storage Blob  
  
## <a name="query-tools"></a>Herramientas de consulta   
  
Las consultas se escriben con Transact\-SQL modificarse para ajustarla a la naturaleza MPP de las consultas. Todas las consultas se envían al nodo de Control, lo que genera un plan de consulta en paralelo para ejecutar la consulta en todos los nodos de proceso.  
  
### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)  
SQL Server Data Tools se ejecuta dentro de Visual Studio y es nuestra herramienta de GUI recomendada para enviar consultas de PDW de SQL Server. Es similar a SQL Server Management Studio, ya que permite navegar a través de un explorador de objetos.  
  
Si aún no tiene Visual Studio, puede descargar las herramientas que necesita de forma gratuita. 
<!-- MISSING LINKS
For more information, see [Install SQL Server database tooling  for Visual Studio &#40;SQL Server PDW&#41;](../sqlpdw/install-sql-server-database-tooling-for-visual-studio-sql-server-pdw.md).  
-->
  
### <a name="sqlcmd-command-line-query-tool"></a>Herramienta de consulta de línea de comandos de SQLCMD  
Sqlcmd es la herramienta de línea de comandos de SQL Server para ejecutar Transact\-SQL instrucciones y comandos del sistema. Funciona con PDW de SQL Server y es nuestra herramienta de línea de comandos recomendado para las consultas de PDW de SQL Server. Con sqlcmd se puede ejecutar Transact\-instrucciones de SQL forma interactiva desde la línea de comandos, como un archivo por lotes, o desde Windows PowerShell.  
  
<!-- MISSING LINKS

If you don't have SQL Server, you can download this as a standalone package. For more information, see [Install sqlcmd Command-Line Client &#40;SQL Server PDW&#41;](../sqlpdw/install-sqlcmd-command-line-client-sql-server-pdw.md) 
--> 
  
### <a name="integration-services"></a>Integration Services  
Puede usar Integration Services a PDW de SQL Server de la consulta. 

<!-- MISSING LINKS
For more information, see [Connect With SQL Server Integration Services for Querying &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-integration-services-for-querying-sql-server-pdw.md). 

--> 
  
### <a name="linked-server"></a>Servidor vinculado  
Mediante el uso de una conexión de servidor vinculado de SQL Server, puede usar SQL Server para enviar Transact\-instrucciones SQL para PDW de SQL Server. 
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Linked Server &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-linked-server-sql-server-pdw.md). 
--> 
  
## <a name="business-intelligence-tools"></a>Herramientas de inteligencia empresarial
  
### <a name="analysis-services"></a>Analysis Services  
SQL Server PDW es un origen de datos válido para las bases de datos de Analysis Services y los modelos de PowerPivot para Excel. Mediante el proveedor OLE DB, puede configurar un cubo de Analysis Services para utilizar procesamiento analítico en línea multidimensional (MOLAP) o almacenamiento de procesamiento analítico en línea relacional (ROLAP).  
  
<!-- MISSING LINKS
For more information, see [Connect With SQL Server Analysis Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-analysis-services-sql-server-pdw.md).  

-->
  
### <a name="report-builder"></a>Generador de informes  
Puede usar SQL Server PDW como un origen de datos de SQL Server para informes que desarrolle para Reporting Services utilizando el generador de informes de SQL Server. También puede usar SQL Server PDW como un origen de SQL Server para los modelos de informe. Mediante el Administrador de informes o la API de servidor de informes, puede generar un modelo desde una base de datos de SQL Server PDW.  
  
<!-- MISSING LINKS

For more information, see [Connect With SQL Server Report Builder &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-report-builder-sql-server-pdw.md) and [Connect With SQL Server Reporting Services &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-sql-server-reporting-services-sql-server-pdw.md). 

--> 
  
### <a name="power-pivot-for-excel"></a>Power Pivot para Excel  
Puede conectarse a SQL Server PDW con PowerPivot para Excel, una descarga gratuita que amplía las capacidades de análisis de datos de Excel de forma significativa.  
  
<!-- MISSING LINKS

For more information, see [Connect With PowerPivot for Excel &#40;SQL Server PDW&#41;](../sqlpdw/connect-with-powerpivot-for-excel-sql-server-pdw.md).  

-->
  
## <a name="loading-tools"></a>Herramientas de carga 
  
### <a name="integration-services"></a>Integration Services  
Instale a los adaptadores de destino de PDW específicos que le permiten usar SQL ServerIntegration Services para cargar datos en PDW de SQL Server.  

<!-- MISSING LINKS
For more information, see [Install Integration Services Destination Adapters &#40;SQL Server PDW&#41;](../sqlpdw/install-integration-services-destination-adapters-sql-server-pdw.md). 
--> 
  
### <a name="dwloader-command-line-loader"></a>Cargador de la línea de comandos de dwloader  
dwloader es una herramienta de línea de comandos de carga que carga los datos en paralelo desde el servidor de la carga en los nodos de proceso de SQL Server PDW. 

<!-- MISSING LINKS
For more information, see [Install dwloader Command-Line Loader &#40;SQL Server PDW&#41;](../sqlpdw/install-dwloader-command-line-loader-sql-server-pdw.md)  
-->
  
### <a name="polybase-for-hadoop-integration"></a>PolyBase para la integración de Hadoop  
Con la tecnología PolyBase, puede cargar los datos no relacionales de un clúster de Hadoop en una tabla relacional en PDW de SQL Server. Los datos de Hadoop pueden encontrarse en un clúster de Hadoop externo o en un Blob de almacenamiento de Azure.  

<!-- MISSING LINKS
For more information, see [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md).
-->  
  
## <a name="database-backup-and-restore"></a>Restauración y copia de seguridad de base de datos  
PDW de SQL Server utiliza la copia de seguridad de base de datos de Transact-SQL y restaurar los comandos en la copia de seguridad y restaurar bases de datos de usuario, en paralelo, a y desde un servidor de copia de seguridad. PDW de SQL Server escribe la copia de seguridad en un directorio en un recurso compartido de archivos de Windows y, a continuación, se restaura del mismo modo datos desde un recurso compartido de archivos de Windows.  
  
Para obtener más información, consulte [planear la copia de seguridad y la carga de Hardware](backup-and-loading-hardware.md) y [copia de seguridad y restaurar información general](backup-and-restore-overview.md)  
  
## <a name="remote-table-copy"></a>Copia de la tabla remota  
La característica de copia de la tabla remota permite copiar tablas de bases de datos PDW de SQL Server para bases de datos de SQL Server de SMP de remotas (que no sea de dispositivo). Esto habilita escenarios de concentrador y radio para PDW de SQL Server.  
  
<!-- MISSING LINKS

For more information, see [Remote Table Copy &#40;SQL Server PDW&#41;](../sqlpdw/remote-table-copy-sql-server-pdw.md).  

-->
  
## <a name="monitoring"></a>Supervisión  
Analytics Platform System ofrece varias maneras para supervisar la actividad de dispositivo  
  
### <a name="admin-console"></a>Consola de administración  
La consola de administración permite ver el estado actual sobre el estado del dispositivo. Esto se ejecuta como una aplicación web en el nodo de Control y es accesible a través de https.  
  
Para obtener más información, consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  

### <a name="system-views"></a>Vistas del sistema  
La consola de administración se basa en las consultas de vista del sistema. Puede consultar las vistas del sistema individualmente para obtener la parte específica de la información que necesita.  

Para obtener más información, consulte [supervisar el dispositivo mediante el uso de vistas del sistema &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md) 
  
### <a name="system-center-operations-manager"></a>System Center Operations Manager  
Hay módulos de administración de System Center Operations Manager (SCOM) para PDW de SQL Server. 

Para configurar el dispositivo para SCOM, consulte [supervisar el dispositivo mediante el uso de System Center Operations Manager &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
