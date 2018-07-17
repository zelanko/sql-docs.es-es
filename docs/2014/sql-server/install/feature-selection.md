---
title: Selección de características | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- feature selection, Setup
helpviewer_keywords:
- SQL Server Installation Wizard, Components to Install page
- Components to Install page [SQL Server Installation Wizard]
ms.assetid: 73182088-153b-4634-a060-d14d1fd23b70
caps.latest.revision: 86
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a00261718d83a82c595416b6dd0d9b97e8929e0d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315495"
---
# <a name="feature-selection"></a>Selección de características
  Utilice las casillas de la página **Selección de características** del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el fin de seleccionar los componentes de la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-features"></a>Instalar características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 En la página **Selección de características** , las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están separadas en dos secciones principales: **Características de instancia** y **Características compartidas**.  
  
 **Características de instancia** hace referencia a los componentes instalados una vez para cada instancia, de modo que tenga varias copias de ellas (una para cada instancia). Cada instancia puede ser una versión independiente que tiene otro nivel de revisión. Cuando se instala una revisión, ya sea un Service Pack, una revisión o una actualización acumulativa, solo actualiza los archivos de una instancia de un equipo determinado, más las características compartidas si no se han actualizado ya.  
  
 **Características compartidas** hace referencia a las características comunes a todas las instancias en un equipo determinado. Cada una de estas características compartidas se ha diseñado para ser compatible con las versiones admitidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Service Pack, actualizaciones acumulativas y revisiones) que se pueden instalar en paralelo.  
  
> [!NOTE]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :** el [!INCLUDE[ssDE](../../includes/ssde-md.md)] y los componentes de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] son las únicas características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que admiten los clústeres de conmutación por error. Puede instalar otros componentes, como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], en un nodo de clúster de conmutación por error, pero estos componentes no detectan los clústeres y sus servicios no realizan la conmutación por error si el nodo de clúster de conmutación por error se queda sin conexión. Para obtener más información,vea [Instancias de clúster de conmutación por error de AlwaysOn &#40;SQL Server&#41;](../failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
### <a name="instance-features"></a>Características de instancia  
 En el panel **Descripción** , se muestra una descripción de cada grupo de componentes cuando se selecciona. Puede activar cualquier combinación de casillas. Para continuar, debe realizar una selección.  
  
|Características|Descripción|  
|--------------|-----------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] Servicios|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] incluye el [!INCLUDE[ssDE](../../includes/ssde-md.md)], el servicio principal para almacenar, procesar y proteger datos, replicación, búsqueda de texto completo, herramientas para administrar relacionales y datos XML y el [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] servidor (DQS). Las siguientes son características del motor de base de datos:<br /><br /> [!INCLUDE[ssDE](../../includes/ssde-md.md)] es el servicio principal para almacenar, procesar y proteger los datos.<br /><br /> Replicación (opcional): la replicación es un conjunto de tecnologías destinadas a la copia y distribución de datos y objetos de base de datos desde una base de datos a otra, para luego sincronizar ambas bases de datos y mantener su coherencia.<br /><br /> Búsqueda de texto completo: (opcional) la búsqueda de texto completo proporciona la funcionalidad necesaria para realizar consultas de texto completo en datos formados por caracteres sin formato contenidos en tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]: Opcional: [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) es una solución de limpieza de datos que permite detectar datos incoherentes e incorrectos en el origen de datos y proporciona formas asistida por PC e interactivas de limpiar los datos. Active esta casilla para instalar el servidor DQS. Debe ejecutar el archivo DQSInstaller.exe una vez completado el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para *completar* la instalación del servidor DQS. Si ha instalado la instancia predeterminada de SQL server, este archivo está disponible en C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. MSSQLSERVER\MSSQL\Binn.<br /><br /> <br /><br /> **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Clústeres de conmutación por error:** los componentes de replicación y búsqueda de texto completo son necesarios y los selecciona automáticamente el programa de instalación para las instalaciones de clústeres de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando selecciona Servicios de Motor de base de datos.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye las herramientas para crear y administrar aplicaciones de procesamiento analítico en línea (OLAP) y de minería de datos.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] – Nativo|El modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye componentes de servidor y de cliente para crear, administrar e implementar informes tabulares, matriciales, gráficos y de forma libre. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es también una plataforma extensible que se puede usar para desarrollar aplicaciones de informes.|  
  
> [!IMPORTANT]  
>  1.  El programa de instalación no configura el equilibro de carga ni direcciones URL únicas para varios nodos en una implementación escalada de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para completar una implementación escalada, debe utilizar Windows Server, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Application Center o software de administración de clúster de terceros. Para obtener más información acerca de cómo configurar la implementación de granja de servidores Web, consulte [configurar Reporting Services para la implementación escalada](http://go.microsoft.com/fwlink/?LinkId=199448) (http://go.microsoft.com/fwlink/?LinkId=199448).  
> 2.  Para los requisitos del explorador de componentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Planear la compatibilidad del explorador de Reporting Services y Power View &#40;Reporting Services 2014&#41;](../../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).  
> 3.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no se admite en configuraciones en paralelo en la plataforma de 64 bits y en el subsistema de 32 bits (WOW64) de un servidor de 64 bits al mismo tiempo.  
  
### <a name="shared-features"></a>Características compartidas  
 Las características que comparten todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un mismo equipo se instalan en un solo directorio. Entre ellas se incluyen los siguientes:  
  
|Característica|Descripción|  
|-------------|-----------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] : SharePoint|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] El modo de SharePoint es una aplicación basada servidor para crear, administrar y entregar informes por correo electrónico, múltiples formatos de archivo y formaciones basadas en Web interactivas. El modo de SharePoint integra la experiencia de visualización y administración de informes con los productos de SharePoint. Para obtener más información, vea [Servidor de informes de Reporting Services &#40;modo de SharePoint&#41;](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md).|  
|Complemento[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint Products|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Complemento para productos de SharePoint incluye componentes de interfaz de administración y usuario para integrar un producto de SharePoint con un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de informes en modo de SharePoint. Para obtener más información, vea [Dónde encontrar el complemento Reporting Services para Productos de SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).|  
|Cliente de calidad de datos|El Cliente de calidad de datos es una aplicación independiente que se conecta al servidor DQS y proporciona una interfaz gráfica de usuario intuitiva para realizar operaciones de limpieza de datos y de coincidencia de datos, así como para realizar tareas administrativas en DQS.|  
|Conectividad con las herramientas de cliente|Herramientas de cliente incluye componentes para la comunicación entre los clientes y los servidores, incluidas las bibliotecas de red para DB-Library, OLEDB para OLAP, ODBC, ADODB y ADOMD+.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] es un conjunto de herramientas gráficas y objetos programables para mover, copiar y transformar datos.|  
|Compatibilidad con las versiones anteriores de las herramientas de cliente|Compatibilidad con las versiones anteriores de las herramientas de cliente incluye los componentes siguientes:<br /><br /> Objetos de administración distribuida de SQL (SQL-DMO). Para más información, vea [Características de SQL Server no disponibles en SQL Server 2014](../../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md).<br /><br /> Objetos de ayuda para la toma de decisiones (DSO). Para más información, vea [Cambios recientes en las características de Analysis Services en SQL Server 2014](../../../2014/analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2014.md).|  
|SDK de las herramientas de cliente|Incluye el kit de desarrollo de software que contiene los recursos para programadores.|  
|Componentes de documentación|Los componentes de documentación incluyen componentes para ver y administrar el contenido de la ayuda.|  
|Herramientas de administración: básicas|**Herramientas de administración – Básica:** esto incluye lo siguiente:<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] compatibilidad con la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], **sqlcmd** utilidad y el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de PowerShell<br /><br /> **Herramientas de administración – Completa:** incluyen los componentes siguientes, además de los componentes de la versión básica:<br /><br /> Compatibilidad de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]<br /><br /> Database Engine Tuning Advisor<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Administración de la utilidad|  
|Distributed Replay Controller|El controlador de Distributed Replay orquestra las acciones de los clientes de Distributed Replay. Solo puede haber una instancia de controlador en cada entorno de Distributed Replay. Para obtener más información, vea [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).|  
|Distributed Replay Client|Los clientes de Distributed Replay colaboran para simular cargas de trabajo en una instancia de SQL Server. Puede haber uno o más clientes en cada entorno de Distributed Replay. Para obtener más información, vea [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).|  
|SDK de conectividad de cliente SQL|Incluye el SDK de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC/OLE DB) para el desarrollo de aplicaciones de base de datos.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] es una plataforma para integrar datos de distintos sistemas de una organización en un único origen de datos maestros para lograr precisión y con fines de auditoría. La opción [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] instala [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], ensamblados, un complemento de Windows PowerShell y carpetas y archivos para las aplicaciones y los servicios web.|  
  
 De forma predeterminada, los componentes compartidos se instalan en %Archivos de programa%Microsoft SQL Server\\. Para cambiar la ruta de instalación, haga clic en el botón **Examinar** . Si cambia la ruta de instalación de un componente compartido, también cambia la de los demás componentes compartidos. En las instalaciones posteriores los componentes compartidos se instalarán en la misma ubicación que la instalación original.  
  
 **Directorio raíz de instancia** : de forma predeterminada, el directorio raíz de instancia es C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\. Para especificar un directorio raíz no predeterminado, haga clic en el botón **Examinar** o proporcione un nombre de ruta de acceso.  
  
 En sistemas operativos basados en x64, puede especificar dónde se instalarán los componentes de 64 bits y los componentes de 32 bits del subsistema WOW64.  
  
## <a name="disk-space-requirements"></a>Requisitos de espacio en disco  
 Use la página Resumen de espacio en disco para examinar los requisitos de espacio en disco necesarios para las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleccionadas durante la instalación.  
  
### <a name="options"></a>Opciones  
 Si se requiere mucho espacio en disco, considere las opciones siguientes:  
  
-   Cambie los directorios de instalación por una unidad de disco que disponga de más espacio.  
  
-   Cambie las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleccionadas durante la instalación.  
  
-   Cree más espacio disponible en la unidad de disco especificada; para ello, mueva otros archivos o aplicaciones.  
  
## <a name="installing-adventureworks-sample-databases"></a>Instalar Bases de datos de ejemplo AdventureWorks  
 De forma predeterminada, las bases de datos y el código de ejemplo no se instalan como parte del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información acerca de cómo instalar las bases de datos de ejemplo y ejemplos de código, vea el [Microsoft SQL Server Community Projects & Samples](http://go.microsoft.com/fwlink/?LinkId=87843) (http://go.microsoft.com/fwlink/?LinkId=87843).  
  
 Una vez instalado [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], está disponible la información adicional sobre los ejemplos. Desde el **iniciar** menú, haga clic en **todos los programas**, haga clic en **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**, haga clic en **documentación y tutoriales** y, a continuación, haga clic en  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Samples Overview**.  
  
## <a name="see-also"></a>Vea también  
 [Ediciones y componentes de SQL Server 2014](../editions-and-components-of-sql-server-2016.md)  
  
  
