---
title: Instalar SQL Server | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 07/24/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: "59"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: eab4b7f0ac099d615df1eda831adf04dfd29a7f6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="install-sql-server"></a>Instalar SQL Server

 > Para obtener contenido relacionado sobre las versiones anteriores de SQL Server, vea [Instalar SQL Server 2014](https://msdn.microsoft.com/library/bb500395(SQL.120).aspx).

 A partir de [!INCLUDE[sssql15](../../includes/sssql15-md.md)], [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] solo está disponible como una aplicación de 64 bits. Aquí encontrará información importante acerca de cómo obtener SQL Server y cómo instalarlo.

## <a name="installation-details"></a>Detalles de la instalación
  
*  **Opciones**: instale, mediante el Asistente para la instalación, un símbolo del sistema o sysprep
 
*  **Requisitos**: antes de instalar, dedique algo de tiempo a revisar los requisitos de instalación, las comprobaciones de configuración del sistema y las consideraciones de seguridad de [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) 

* **Proceso**: vea [Instalación de SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md) para obtener instrucciones completas sobre el proceso de instalación

* **Bases de datos de ejemplo y código de ejemplo**: 
    * No se instalan como parte de la configuración de SQL Server de forma predeterminada. 
    * Para instalarlos para ediciones distintas de Express de SQL Server, vea [GitHub](http://github.com/Microsoft/sql-server-samples).
    

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="how-to-install-includessnoversionincludesssnoversion-mdmd"></a>Cómo instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]
 
|Title|Description|  
|-----------|-----------------|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] en Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Vea este tema para instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] en Windows Server Core.|  
|[Comprobar los parámetros del Comprobador de configuración del sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Describe la función del Comprobador de la configuración del sistema (SCC).|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|Tema de procedimientos para realizar una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] típica con el Asistente para la instalación.|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Tema de procedimientos que proporciona los parámetros de la instalación y la sintaxis de ejemplo para ejecutar una instalación desatendida.|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] mediante un archivo de configuración](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Tema de procedimientos que proporciona los parámetros de la instalación y la sintaxis de ejemplo para ejecutar una instalación mediante un archivo de configuración.|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] con SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|Tema de procedimientos que proporciona parámetros de ejemplo de instalación y sintaxis para ejecutar el programa de instalación mediante sysprep.|  
|[Agregar características a una instancia de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] &#40;programa de instalación&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Tema de procedimientos que permite actualizar los componentes de una instancia existente de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Reparar una instalación de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] con errores](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|Tema de procedimientos para reparar una instalación de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] dañada.|  
|[Cambiar el nombre de un equipo que hospeda una instancia independiente de SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Tema de procedimientos para actualizar los metadatos del sistema que se almacenan en sys.servers.|  
|[Instalar actualizaciones de servicio de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|Tema de procedimientos para instalar actualizaciones de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|Tema de procedimientos para comprobar si hay errores en los archivos de registro de una instalación.|  
|[Validar una instalación de SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Revise el uso del informe de SQL Discovery para comprobar la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo.|  
  
  
## <a name="how-to-install-individual-components"></a>Cómo instalar los componentes individuales  
  
|Tema|Description|  
|-----------|-----------------|  
|[Instalar el motor de base de datos de SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)|Describe cómo instalar y configurar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Instalar la replicación de SQL Server](../../database-engine/install-windows/install-sql-server-replication.md)|Describe cómo instalar y configurar la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Install Distributed Replay - Overview (Instalar Distributed Replay: información general)](../../tools/distributed-replay/install-distributed-replay-overview.md)|Enumera los temas para instalar la característica Distributed Replay.|  
|[Instalar las Herramientas de administración de SQL Server con SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|Describe cómo instalar y configurar las herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Instalar SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|Describe las consideraciones para instalar los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|  
  

## <a name="how-to-configure-sql-server"></a>Cómo configurar SQL Server  
  
|Tema|Description|  
|-----------|-----------------|  
|[Configure the Windows Firewall to Allow SQL Server Access (Configurar el Firewall de Windows para permitir el acceso a SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|En este tema se proporciona información general de la configuración del firewall y de cómo configurar Firewall de Windows.|  
|[Configurar un equipo de host múltiple para el acceso a SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|En este tema se describe cómo configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Firewall de Windows con seguridad avanzada para proporcionar las conexiones de red a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno de host múltiple.|  
|[Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Puede seguir los pasos proporcionados en este tema para configurar los valores de puerto y firewall para permitir el acceso a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Ediciones y características admitidas de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[Instalar características de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Business Intelligence](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  [Instalación de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>Vea también  

[Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Actualización a [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Desinstalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
