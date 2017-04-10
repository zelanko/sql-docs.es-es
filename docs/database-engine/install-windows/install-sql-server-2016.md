---
title: "Instalar SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Base de datos de ejemplo AdventureWorks"
  - "instalar SQL Server, prepararse para instalar"
  - "instalación [SQL Server]"
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 59
ms.author: "mikeray"
manager: "jhubbard"
---
# Instalar SQL Server 2016
  SQL Server 2016 es una aplicación de 64 bits. Aquí encontrará información importante acerca de cómo obtener SQL Server y cómo instalarlo.

## <a name="installation-details"></a>Detalles de la instalación
  
*  **Opciones**: instale, mediante el Asistente para la instalación, un símbolo del sistema o sysprep
 
*  **Requisitos**: antes de instalar, dedique algo de tiempo a revisar los requisitos de instalación, las comprobaciones de configuración del sistema y las consideraciones de seguridad de [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) 

* **Proceso**: vea [Instalación de SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md) para obtener instrucciones completas sobre el proceso de instalación

* **Bases de datos de ejemplo y código de ejemplo**: 
    * No se instalan como parte de la configuración de SQL Server de forma predeterminada. 
    * Para instalarlos para ediciones distintas de Express de SQL Server, consulte el [sitio web de CodePlex](http://go.microsoft.com/fwlink/?LinkId=87843).
    * Para obtener información sobre la compatibilidad con las bases de datos de ejemplo de SQL Server y el código de ejemplo para SQL Server Express, consulte [Databases and Samples Overview (Información general sobre bases de datos y ejemplos)](http://go.microsoft.com/fwlink/?LinkId=110391).
    

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

La ubicación de descarga de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] depende de la edición:

- **Las ediciones Enterprise, Standard y Express de SQL Server** tienen licencia para su uso en producción. En el caso de las ediciones Enterprise y Standard, póngase en contacto con su proveedor de software para obtener los medios de instalación. Encontrará información sobre la adquisición y un directorio de asociados de Microsoft en el [sitio web de adquisición de Microsoft](https://www.microsoft.com/en-us/server-cloud/products/sql-server/overview.aspx). 

- En estos vínculos están disponibles **ediciones gratuitas**:

| Edición | Description
|---------|--------
|[Developer Edition](http://myprodscussu1.app.vssubscriptions.visualstudio.com/Downloads?q=SQL%20Server%20Developer) | Conjunto gratuito y con todas las características del software de SQL Server 2016 Enterprise Edition que permite a los desarrolladores compilar, probar y demostrar aplicaciones en un entorno que no sea de producción. 
|[Express Edition](http://www.microsoft.com/download/details.aspx?id=52679)|  Base de datos gratuita de nivel básico ideal para implementar bases de datos pequeñas en entornos de producción. Permite compilar aplicaciones controladas por datos de escritorio y servidores pequeños con un tamaño del disco de hasta 10 GB. 
| [Evaluation Edition](http://technet.microsoft.com/evalcenter/mt130694) | Conjunto con todas las características del software de SQL Server Enterprise Edition que proporciona un período de evaluación de 180 días.
   
 
  

## <a name="how-to-install-sql-server"></a>Cómo instalar SQL Server
 
|Title|Description|  
|-----------|-----------------|  
|[Instalación de SQL Server 2016 en Server Core](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md)|Vea este tema para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en Windows Server Core.|  
|[Comprobar los parámetros del Comprobador de configuración del sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Describe la función del Comprobador de la configuración del sistema (SCC).|  
|[Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)|Tema de procedimientos para realizar una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] típica con el Asistente para la instalación.|  
|[Instalar SQL Server 2016 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Tema de procedimientos que proporciona los parámetros de la instalación y la sintaxis de ejemplo para ejecutar una instalación desatendida.|  
|[Instalar SQL Server 2016 mediante un archivo de configuración](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Tema de procedimientos que proporciona los parámetros de la instalación y la sintaxis de ejemplo para ejecutar una instalación mediante un archivo de configuración.|  
|[Instalar SQL Server 2016 mediante SysPrep](../../database-engine/install-windows/install-sql-server-2016-using-sysprep.md)|Tema de procedimientos que proporciona parámetros de ejemplo de instalación y sintaxis para ejecutar el programa de instalación mediante sysprep.|  
|[Agregar características a una instancia de SQL Server 2016 &#40;programa de instalación&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Tema de procedimientos que permite actualizar los componentes de una instancia existente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|[Reparar una instalación de SQL Server 2016 con errores](../../database-engine/install-windows/repair-a-failed-sql-server-2016-installation.md)|Tema de procedimientos para reparar una instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dañada.|  
|[Cambiar el nombre de un equipo que hospeda una instancia independiente de SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Tema de procedimientos para actualizar los metadatos del sistema que se almacenan en sys.servers.|  
|[Instalar actualizaciones de servicio de SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-servicing-updates.md)|Tema de procedimientos para instalar actualizaciones para SQL Server 2016.|  
|[Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|Tema de procedimientos para comprobar si hay errores en los archivos de registro de una instalación.|  
|[Validar una instalación de SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Revise el uso del informe de SQL Discovery para comprobar la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo.|  
  
  
## <a name="how-to-install-individual-components"></a>Cómo instalar los componentes individuales  
  
|Tema|Description|  
|-----------|-----------------|  
|[Instalar el motor de base de datos de SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)|Describe cómo instalar y configurar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Instalar la replicación de SQL Server](../../database-engine/install-windows/install-sql-server-replication.md)|Describe cómo instalar y configurar la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Install Distributed Replay - Overview (Instalar Distributed Replay: información general)](../../tools/distributed-replay/install-distributed-replay-overview.md)|Enumera los temas para instalar la característica Distributed Replay.|  
|[Instalar las Herramientas de administración de SQL Server con SSMS](Install%20SQL%20Server%20Management%20Tools%20\(SSMS\).md)|Describe cómo instalar y configurar las herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Instalar SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|Describe las consideraciones para instalar los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|  
  

## <a name="how-to-configure-sql-server"></a>Cómo configurar SQL Server  
  
|Tema|Description|  
|-----------|-----------------|  
|[Configure the Windows Firewall to Allow SQL Server Access (Configurar el Firewall de Windows para permitir el acceso a SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|En este tema se proporciona información general de la configuración del firewall y de cómo configurar Firewall de Windows.|  
|[Configurar un equipo de host múltiple para el acceso a SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|En este tema se describe cómo configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Firewall de Windows con seguridad avanzada para proporcionar las conexiones de red a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno de host múltiple.|  
|[Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Puede seguir los pasos proporcionados en este tema para configurar los valores de puerto y firewall para permitir el acceso a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Características compatibles con la edición de SQL Server 2016](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
[Instalar características de SQL Server 2016 Business Intelligence](../../sql-server/install/install-sql-server-2016-business-intelligence-features.md)  
  [Instalación de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>Vea también  

[Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Actualizar a SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [Desinstalar SQL Server 2016](../../sql-server/install/uninstall-sql-server-2016.md)   
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  