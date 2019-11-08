---
title: Características de SQL Server no incluidas en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 0678bfbc-5d3f-44f4-89c0-13e8e52404da
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8f7ab6cdbc1b6e0e3dc7d26fb579943a0c8fa95
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637773"
---
# <a name="discontinued-sql-server-features-in-sql-server-2014"></a>Características de SQL Server no disponibles en SQL Server 2014
  En este tema se describen las características que ya no están disponibles tras actualizar a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>Características no incluidas en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Características no incluidas en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>Características no incluidas en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="discontinued-active-directory-helper-service"></a>Servicio del asistente de Active Directory no incluido  
 El Servicio del asistente de Active Directory los componentes relacionados se han quitado. En la siguiente tabla se muestran los componentes asociados que se quitan como resultado:  
  
|Categoría|Característica no incluida|Sustituta|  
|--------------|--------------------------|-----------------|  
|Procedimientos almacenados del sistema|sp_ActiveDirectory_Obj<br /><br /> sp_ActiveDirectory_SCP<br /><br /> sp_ActiveDirectory_Start|Ningún reemplazo disponible|  
  
## <a name="discontinued-features-in-sql-server-2008-r2"></a>Características de SQL Server no incluidas en SQL Server 2008 R2  
  
### <a name="64-bit-platform-support-in-reporting-services"></a>Compatibilidad de la plataforma de 64 bits en Reporting Services  
 A partir de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], el componente de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ya no admite servidores basados en Itanium que ejecuten Windows Server 2003 o Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sigue admitiendo otros sistemas operativos de 64 bits, incluido Windows Server°2008 para sistemas basados en Itanium y Windows Server°2008°R2 para sistemas basados en Itanium. Para actualizar a [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] desde una instalación de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en una edición del sistema basada en Itanium de Windows Server 2003 o Windows Server 2003 R2, primero debe actualizar el sistema operativo.  
  
## <a name="discontinued-features-in-sql-server-2008"></a>Características de SQL Server no incluidas en SQL Server 2008  
  
### <a name="discontinued-sql-dmo-from-sql-server-express-installation"></a>SQL-DMO no está disponible desde la instalación de SQL Server Express  
 SQL-DMO para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se ha quitado de [!INCLUDE[ssExpressEd10](../includes/ssexpressed10-md.md)]. Le recomendamos que modifique las aplicaciones que actualmente utilicen esta característica tan pronto como le sea posible. Si debe admitir SQL-DMO para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express, instale los componentes de compatibilidad con versiones anteriores del Feature Pack de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] desde el [centro de descarga de Microsoft](https://www.microsoft.com/download/details.aspx?id=24793). Use Objetos de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (SMO) en nuevos trabajos de desarrollo.  
  
### <a name="discontinued-option-for-web-assistant"></a>Opción no incluida para Asistente de Web  
 La opción `sp_configure` para habilitar el Asistente de Web se ha quitado de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Se recomienda utilizar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en su lugar.  
  
### <a name="surface-area-configuration-tool"></a>herramienta de configuración de área expuesta  
 La herramienta de configuración de área expuesta ya no se incluye en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. En la tabla siguiente se muestra lo que se puede utilizar para configurar valores, opciones y características de componentes en esta versión.  
  
|Configuración de reemplazo y características de componentes|Cómo se configura|  
|-------------------------------------------------|----------------------|  
|Protocolos, conexiones y opciones de inicio|Use el Administrador de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|Características del [!INCLUDE[ssDE](../includes/ssde-md.md)]|Utilice la administración basada en directivas, la configuración de propiedades de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o sp_Configure.|  
|Características del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Utilice la configuración de propiedades de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].|  
|propiedad de seguridad [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-EnableIntegrated|Utilice la configuración de propiedades de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-"eventos de programación y entrega de informes" y "acceso HTTP y servicio Web"|Modifique el archivo de configuración RSReportServer.config|  
|Opciones de la línea de comandos|No existe compatibilidad en esta versión.|  
|SOAP y extremos de [!INCLUDE[ssSB](../includes/sssb-md.md)]|Utilice [Create Endpoint](/sql/t-sql/statements/create-endpoint-transact-sql)y [ALTER Endpoint](/sql/t-sql/statements/alter-endpoint-transact-sql).|  
  
### <a name="discontinued-command-prompt-parameters-for-sql-server-setup"></a>Parámetros del símbolo del sistema no incluidos para el programa de instalación de SQL Server  
 En la tabla siguiente se muestran los parámetros del símbolo del sistema de las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que no se admiten en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
|Parámetro no incluido|Parámetros de reemplazo|  
|----------------------------|---------------------------|  
|ADDLOCAL|/ACTION=Uninstall y /FEATURES|  
|DISABLENETWORKPROTOCOLS|/TCPENABLED para TCP/IP<sup>1</sup>|  
|DISABLENETWORKPROTOCOLS|/NPENABLED para canalizaciones con nombre<sup>1</sup>|  
|INSTALLSQLDATADIR|/SQLUSERDBDIR<br /><br /> /SQLUSERDBLOGDIR<br /><br /> /SQLBACKUPDIR<br /><br /> /SQLTEMPDBDIR<br /><br /> /SQLTEMPDBLOGDIR|  
|REINSTALL|Sin equivalencia en esta versión.|  
|REINSTALLMODE|Sin equivalencia en esta versión.|  
|REMOVE|/ACTION=Uninstall y /FEATURES|  
|SAMPLEDATABASE|Sin equivalencia en esta versión.|  
|SAVESYSDB|Sin equivalencia en esta versión.|  
|SKUUPGRADE<sup>2</sup>|Sin equivalencia en esta versión.|  
|UPGRADE|/ACTION=Upgrade y /FEATURES|  
|USESYSDB|Sin equivalencia en esta versión.|  
  
 <sup>1</sup> Estos parámetros solo son válidos para la instalación de.  
  
 <sup>2</sup> A partir de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], especifique/Action = EditionUpgrade para actualizar una edición existente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a una edición diferente en cualquier momento sin usar los medios de instalación originales. Para obtener más información acerca de las actualizaciones de edición y versión compatibles, vea [Supported Version and Edition Upgrades](../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
 Para obtener más información, vea [Instalar SQL Server 2014 desde el símbolo del sistema](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
  
