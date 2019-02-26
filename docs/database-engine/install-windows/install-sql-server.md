---
title: Instalar SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: quickstart
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 184654ada07be1ab7c51d32bdee9770790204647
ms.sourcegitcommit: a13256f484eee2f52c812646cc989eb0ce6cf6aa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/25/2019
ms.locfileid: "56802639"
---
# <a name="install-sql-server"></a>Instalar SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 A partir de [!INCLUDE[sssql15](../../includes/sssql15-md.md)], [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] solo está disponible como una aplicación de 64 bits. Aquí encontrará información importante acerca de cómo obtener SQL Server y cómo instalarlo.

## <a name="installation-details"></a>Detalles de la instalación
  
*  **Opciones**: instale mediante el Asistente para la instalación, un símbolo del sistema o sysprep
 
*  **Requisitos**: antes de instalar, dedique algo de tiempo a revisar los requisitos de instalación, las comprobaciones de configuración del sistema y las consideraciones de seguridad de [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md) 

* **Proceso**: vea [Instalación de SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md) para obtener instrucciones completas sobre el proceso de instalación

* **Bases de datos de ejemplo y código de ejemplo**: 
    * No se instalan como parte de la configuración de SQL Server de forma predeterminada. 
    * Para instalarlos para ediciones distintas de Express de SQL Server, vea [GitHub](https://github.com/Microsoft/sql-server-samples).
    

## <a name="get-the-installation-media"></a>Obtener los medios de instalación

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="how-to-install-includessnoversionincludesssnoversion-mdmd"></a>Cómo instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]
 
|Title|Descripción|  
|-----------|-----------------|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] en Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|Lea este artículo para instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] en Windows Server Core.|  
|[Comprobar los parámetros del Comprobador de configuración del sistema](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|Describe la función del Comprobador de la configuración del sistema (SCC).|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|Artículo con procedimientos para realizar una instalación típica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el Asistente para la instalación.|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|Artículo con procedimientos que proporciona parámetros de la instalación y sintaxis de ejemplo para ejecutar una instalación desatendida.|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] mediante un archivo de configuración](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|Artículo con procedimientos que proporciona parámetros de la instalación y sintaxis de ejemplo para ejecutar una instalación mediante un archivo de configuración.|  
|[Instalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] con SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|Artículo con procedimientos que proporciona parámetros de ejemplo de instalación y sintaxis para ejecutar el programa de instalación mediante sysprep.|  
|[Agregar características a una instancia de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] &#40;programa de instalación&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|Artículo con procedimientos para actualizar los componentes de una instancia existente de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Reparar una instalación de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] con errores](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|Artículo con procedimientos para reparar una instalación de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] dañada.|  
|[Cambiar el nombre de un equipo que hospeda una instancia independiente de SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|Artículo con procedimientos para actualizar los metadatos del sistema que se almacenan en sys.servers.|  
|[Instalar actualizaciones de servicio de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|Artículo con procedimientos para instalar actualizaciones de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].|  
|[Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|Artículo con procedimientos para comprobar si hay errores en los archivos de registro de una instalación.|  
|[Validar una instalación de SQL Server](../../database-engine/install-windows/validate-a-sql-server-installation.md)|Revise el uso del informe de SQL Discovery para comprobar la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo.|  
  
  
## <a name="how-to-install-individual-components"></a>Cómo instalar los componentes individuales  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Instalar el motor de base de datos de SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)|Describe cómo instalar y configurar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Instalar la replicación de SQL Server](../../database-engine/install-windows/install-sql-server-replication.md)|Describe cómo instalar y configurar la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Install Distributed Replay - Overview (Instalar Distributed Replay: información general)](../../tools/distributed-replay/install-distributed-replay-overview.md)|Enumera los artículos para instalar la característica Distributed Replay.|  
|[Instalar las Herramientas de administración de SQL Server con SSMS](https://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|Describe cómo instalar y configurar las herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Instalar SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|Describe las consideraciones para instalar los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|  
  

## <a name="how-to-configure-sql-server"></a>Cómo configurar SQL Server  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Configure the Windows Firewall to Allow SQL Server Access (Configurar el Firewall de Windows para permitir el acceso a SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|En este artículo se incluye información general sobre la configuración del firewall y el procedimiento para configurar Firewall de Windows.|  
|[Configurar un equipo de host múltiple para el acceso a SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|En este artículo se describe cómo configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Firewall de Windows con seguridad avanzada para proporcionar las conexiones de red a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno de host múltiple.|  
|[Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Puede seguir los pasos proporcionados en este artículo para configurar los valores de puerto y firewall para permitir el acceso a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Ediciones y características admitidas de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[Instalar características de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Business Intelligence](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  [Instalación de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>Vea también  

[Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Actualización a [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Desinstalar [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
