---
title: Planear una instalación de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, planning
ms.assetid: b1d56f2f-603f-48f2-b902-c715f14a6db9
caps.latest.revision: 33
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e6b68b7cee6f530a8c5f24d54732654da4f89f8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151786"
---
# <a name="planning-a-sql-server-installation"></a>Planear una instalación de SQL Server
  Para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], siga estos pasos:  
  
-   Revise los requisitos de instalación, las comprobaciones de la configuración del sistema y las consideraciones de seguridad para una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar o actualizar a una versión posterior.  
  
-   Utilice las utilidades de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Con independencia del método de instalación, es necesario confirmar la aceptación de los términos de la licencia de software como usuario individual o en nombre de una entidad, a menos que el uso del software en su caso se rija por un acuerdo independiente, como un acuerdo de licencia por volumen de [!INCLUDE[msCoName](../../includes/msconame-md.md)] o un acuerdo suscrito con un ISV u OEM.  
  
 Los términos de la licencia se muestran para revisarlos y aceptarlos en la interfaz de usuario del programa de instalación. Las instalaciones desatendidas (mediante los parámetros /Q o /QS) deben incluir el parámetro /IAcceptSQLServerLicenseTerms. Puede revisar separadamente los términos de licencia en [Términos de licencia de software de Microsoft](http://go.microsoft.com/fwlink/?LinkID=148209).  
  
> [!NOTE]  
>  En función de cómo haya recibido el software (por ejemplo, a través de un contrato de licencias por volumen de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), su uso del software puede estar sujeto a términos y condiciones adicionales.  
  
## <a name="in-this-section"></a>En esta sección  
 [Novedades de la instalación de SQL Server](../../../2014/sql-server/install/what-s-new-in-sql-server-installation.md)  
 En este tema se describen los detalles sobre las características nuevas o mejoradas de la instalación de esta versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Requisitos de hardware y software para instalar SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
 En este tema se enumeran los requisitos mínimos de hardware y software para instalar y ejecutar una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Consideraciones de seguridad para una instalación de SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
 En este tema se describen algunas prácticas recomendadas de seguridad que deben tenerse en cuenta antes de instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y después de instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  
 En este tema se describe la configuración predeterminada de los servicios en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como las opciones de configuración de los servicios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se pueden establecer durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y después.  
  
 [Protocolos de red y bibliotecas de red](../../../2014/sql-server/install/network-protocols-and-network-libraries.md)  
 En este tema se describe la configuración predeterminada de los protocolos de red en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y las opciones de configuración disponibles.  
  
 [Trabajar con varias versiones e instancias de SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)  
 En este tema se describen las consideraciones para instalar varias versiones e instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Versiones en idioma local en SQL Server](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
 En este tema se describen las versiones traducidas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Instalar SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)  
 En esta sección se proporciona información general de las distintas opciones de instalación de que se dispone para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Instalar las características de BI de SQL Server 2014](install-sql-server-business-intelligence-features.md)  
 Esta sección de la documentación de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar las funciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que forman parte de la plataforma de BI de Microsoft.  
  
 [Actualizar a SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)  
 En esta sección se proporciona información general sobre la actualización de las instancias de la versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 [Desinstalar SQL Server 2014](uninstall-sql-server.md)  
 Consulte esta sección para desinstalar por completo una instancia existente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y preparar el sistema para poder volver a instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Instalación de clúster de conmutación por error de SQL Server](../failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar y configurar el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Inicio rápido de instalación de SQL Server 2014](../../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)   
 [Instalar a SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../failover-clusters/high-availability-solutions-sql-server.md)   
 [Antes de instalar los clústeres de conmutación por error](../failover-clusters/install/before-installing-failover-clustering.md)   
 [Actualización a SQL Server 2014 mediante el Asistente para instalación &#40;el programa de instalación&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
