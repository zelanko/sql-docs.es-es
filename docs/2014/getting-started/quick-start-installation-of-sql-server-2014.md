---
title: Instalación de inicio rápido de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- quick start installation [SQL Server]
- installation [SQL Server]
- installing SQL Server, quick start installations
ms.assetid: 672afac9-364d-4946-ad5d-8a2d89cf8d81
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ec876262387ba4470bf225d53320ad62b4b2101
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890129"
---
# <a name="quick-start-installation-of-sql-server-2014"></a>Instalación del tutorial de SQL Server 2014
    
## <a name="introduction"></a>Introducción  
 El Asistente para la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se basa en Windows Installer. Proporciona un único árbol de características para la instalación de los siguientes componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssDE](../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)]  
  
-   Herramientas de administración  
  
-   Componentes de conectividad  
  
 Puede instalar cada componente individualmente o seleccionar una combinación de los componentes enumerados anteriormente. Para elegir la mejor opción entre las ediciones y los componentes disponibles [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]en, consulte [ediciones y componentes de SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está disponible en las ediciones de 32 bits y de 64 bits. El programa de instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite las opciones de instalación siguientes:  
  
-   **Asistente para la instalación**  
  
     Consulte [install SQL Server 2014 (instalación del asistente &#40;&#41; para la instalación](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md) ) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para obtener información de procedimientos sobre la instalación de mediante el Asistente para la instalación de.  
  
-   **Símbolo del sistema**  
  
     Vea [Install SQL Server 2014 desde el símbolo del sistema](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md) para obtener la sintaxis de ejemplo y los parámetros de instalación para ejecutar la instalación desatendida.  
  
-   **Archivo de configuración**  
  
     Consulte [instalación de SQL Server 2014 mediante un archivo de configuración](../database-engine/install-windows/install-sql-server-using-a-configuration-file.md) para ver la sintaxis de ejemplo y los parámetros de instalación para ejecutar el programa de instalación a través de un archivo de configuración.  
  
-   **SysPrep**  
  
     Vea [instalar SQL Server 2014 con Sysprep](../database-engine/install-windows/install-sql-server-using-sysprep.md) para obtener información de procedimientos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] acerca de cómo instalar con Sysprep.  
  
-   **Instalación Server Core**  
  
     Consulte [instalación de SQL Server 2014 en Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md) para obtener información de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] procedimientos sobre la instalación de en Windows Server Core.  
  
-   **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]Instalación de características de BI**  
  
     Para obtener información sobre la instalación de las características que forman parte de la plataforma de BI de Microsoft, consulte Instalación de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]las [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]características [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [BI SQL Server 2014](../sql-server/install/install-sql-server-business-intelligence-features.md) , que incluyen,,, y varias aplicaciones cliente usadas para crear o trabajar con datos analíticos.  
  
-   **Instalación de clústeres de conmutación por error**  
  
     Consulte [SQL Server instalación de clúster de conmutación por error](../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] obtener información de procedimientos sobre cómo instalar en un [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] clúster de conmutación por error.  
  
 De forma predeterminada, las bases de datos y el código de ejemplo no se instalan como parte del programa de instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para instalar las bases de datos y el código de ejemplo para las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que no son Express, vea el [sitio web de CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843). Para obtener información sobre la compatibilidad de las bases de datos y el código muestra de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], vea [Información general sobre bases de datos y ejemplos](https://go.microsoft.com/fwlink/?LinkId=110391).  
  
## <a name="includessnoversionincludesssnoversion-mdmd-installation"></a>Instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Independientemente de si usa el Asistente para la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o el símbolo del sistema para instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el programa de instalación incluye uno o varios de los pasos siguientes:  
  
-   Revise los requisitos de instalación, las comprobaciones de la configuración del sistema y las consideraciones de seguridad para una instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  Para más información, consulte [Planning a SQL Server Installation](quick-start-installation-of-sql-server-2014.md#BKMK_BeforeYouInstall).  
  
-   Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para actualizar una versión existente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obtener más información, consulte [actualización a SQL Server 2014](#BKMK_Upgrading).  
  
-   Ejecute el programa de instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para instalar una nueva instancia de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obtener más información, consulte [instalación de SQL Server 2014](#BKMK_Install).  
  
-   Cuando haya terminado con la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el paso siguiente principal es la configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y sus componentes. Utilice las utilidades de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, consulte [configuración de SQL Server 2014](#BKMK_Configure).  
  
 Puede encontrar explicaciones detalladas de estas tareas en la próxima sección.  
  
## <a name="related-tasks"></a>Related Tasks  
  
###  <a name="BKMK_BeforeYouInstall"></a>Planeación [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de una instalación  
 Antes de instalar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], debe revisar los requisitos de hardware y software, las consideraciones de red y de Internet, y las consideraciones de seguridad para instalar y ejecutar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, vea [planear una instalación de SQL Server](../../2014/sql-server/install/planning-a-sql-server-installation.md) y también los temas siguientes:  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Revisar los requisitos de hardware y software, la compatibilidad del sistema operativo, consideraciones de red y de Internet, y los requisitos de espacio en disco duro.|[Requisitos previos de la instalación](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)|  
|Revise las consideraciones de seguridad para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] una instalación de.|[Consideraciones de seguridad](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)|  
|Revisar los detalles de las características admitidas por las diversas ediciones de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Características y ediciones](features-supported-by-the-editions-of-sql-server-2014.md)|  
|Determinar la mejor opción entre las ediciones y los componentes disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Ediciones y componentes de SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md)|  
|Revisar la configuración de hardware, y aprender a preparar la instalación de un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Antes de instalar los clústeres de conmutación por error](../sql-server/failover-clusters/install/before-installing-failover-clustering.md)|  
  
###  <a name="BKMK_Upgrading"></a>Actualizar a[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Puede actualizar las instancias existentes de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obtener más información, consulte [actualización a SQL Server 2014](../database-engine/install-windows/upgrade-sql-server.md). Antes de ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para actualizar a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], revise los temas siguientes acerca del proceso de actualización:  
  
|Descripción|Tema|  
|-----------------|-----------|  
|Documenta las formas de actualización admitidas para [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Actualizaciones admitidas](../database-engine/install-windows/supported-version-and-edition-upgrades.md)|  
|Describe el Asesor de actualizaciones, una herramienta que analiza las instancias de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] y [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] para identificar problemas de actualización conocidos.|[Usar el Asesor de actualizaciones para preparar las actualizaciones](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)|  
|Describe Distributed Replay Utility, una herramienta que puede usar varios equipos para reproducir datos de seguimiento, simulando una carga de trabajo crítica para una misión. Realizando una reproducción en un servidor de prueba antes y después de una actualización de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], puede medir las diferencias de rendimiento y buscar cualquier incompatibilidad que su aplicación pueda tener con la actualización.|[Emplear Distributed Replay Utility para preparar las actualizaciones](../../2014/sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)|  
|Enumera los cambios importantes que pueden afectar a las aplicaciones después de actualizar a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Compatibilidad con versiones anteriores](backward-compatibility.md)|  
|El tema de procedimientos para actualizar una instancia independiente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Actualice a SQL Server 2014 mediante la instalación del &#40;Asistente para la instalación&#41;](../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)|  
|El tema de procedimientos para actualizar una edición de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] a otra edición. Para obtener información sobre rutas de actualización de ediciones admitidas, vea [Actualizaciones de ediciones y versiones admitidas](../database-engine/install-windows/supported-version-and-edition-upgrades.md).|[Actualización a una edición diferente de la instalación &#40;de SQL Server 2014&#41;](../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite la actualización del [!INCLUDE[ssDE](../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] desde clústeres de conmutación por error de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] por separado en todos los nodos de clúster de conmutación por error. Vea este tema para obtener más información.|[Actualizar un clúster de conmutación por error de SQL Server](../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)|  
  
###  <a name="BKMK_Install"></a>Instalar[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Revise los temas siguientes para obtener información acerca de los diferentes escenarios de instalación de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
|Descripción|Tema|  
|-----------------|-----------|  
|Proporciona vínculos a temas para instalar varios componentes de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y temas de procedimientos para instalar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Instalar SQL Server 2014](../database-engine/install-windows/install-sql-server.md)|  
|Vea este tema para instalar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] en Windows Server Core.|[Instalación de SQL Server 2014 en Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md)|  
|Examine este tema para agregar características individuales a una instancia existente de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|[Agregar características a una instancia de SQL Server el &#40;programa de instalación de 2014&#41;](../database-engine/install-windows/add-features-to-an-instance-of-sql-server-setup.md)|  
|Consulte este tema para crear una nueva instancia del clúster de conmutación por error de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Crear un nuevo clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)|  
|Use este tema para administrar los nodos de una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] existente.|[Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)|  
|Use este tema para instalar las herramientas de cliente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un clúster de conmutación por error.|[Instalar las herramientas de cliente en un clúster de conmutación por error de SQL Server](../sql-server/failover-clusters/install/install-client-tools-on-a-sql-server-failover-cluster.md)|  
|Revise el uso del informe de SQL Discovery para comprobar la versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y las características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instaladas en el equipo.|[Validar una instalación de SQL Server](../database-engine/install-windows/validate-a-sql-server-installation.md)|  
|Proporciona vínculos a temas de procedimientos para instalar [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] con el Asistente para la instalación, desde el símbolo del sistema, utilizando los archivos de configuración y usando SysPrep.|[Temas de procedimientos de instalación](../../2014/sql-server/install/installation-how-to-topics.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
 En esta sección se proporciona información acerca de la configuración y la desinstalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
###  <a name="BKMK_Configure"></a>Configurado[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 Después de instalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], puede seguir configurando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mediante utilidades gráficas y de símbolo del sistema. Vea los temas siguientes para configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] por primera vez:  
  
|Descripción|Tema|  
|-----------------|-----------|  
|Use la información de este tema para determinar si necesita desbloquear puertos de un firewall para permitir el acceso a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o a PowerPivot para SharePoint. Puede seguir los pasos proporcionados en este tema para configurar las opciones de los puertos y del firewall.|[Configurar Firewall de Windows para permitir el acceso a Analysis Services](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|  
|En este tema se proporciona información general de configuración del firewall y se resume información de interés para un administrador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|[Configure the Windows Firewall to Allow SQL Server Access (Configurar el Firewall de Windows para permitir el acceso a SQL Server)](../../2014/sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|En este tema se describe cómo configurar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y Firewall de Windows con seguridad avanzada para proporcionar las conexiones de red a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en un entorno de host múltiple.|[Configurar un equipo de host múltiple para el acceso a SQL Server](../../2014/sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|  
  
###  <a name="BKMK_Uninstalling"></a>Desinstalar[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 En los temas siguientes se describe cómo se desinstala manualmente una instancia independiente y una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
|Descripción|Tema|  
|-----------------|-----------|  
|En este tema se describe cómo desinstalar manualmente una instancia independiente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Desinstalar SQL Server 2014](../sql-server/install/uninstall-sql-server.md)|  
|En este tema se describe cómo desinstalar una instancia en clúster de conmutación por error de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Quitar una instancia de clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)|  
|En este tema se proporciona información sobre cómo quitar manualmente objetos de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) después de desinstalar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o simplemente el servidor DQS.|[Quitar objetos del servidor de calidad de datos](../../2014/sql-server/install/remove-data-quality-server-objects.md)|  
  
## <a name="see-also"></a>Vea también  
 [Especificaciones del producto para SQL Server 2014](sql-server-2014-product-specifications.md)   
 [Introducción a la documentación del producto para SQL Server](../2014-toc/books-online-for-sql-server-2014.md) [Compatibilidad con versiones anteriores](backward-compatibility.md)  
  
  
