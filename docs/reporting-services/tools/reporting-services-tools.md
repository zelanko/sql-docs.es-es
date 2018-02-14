---
title: Herramientas de Reporting Services | Microsoft Docs
ms.custom: 
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: tools
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSRS, tools
- Reporting Services, tools
- components [Reporting Services]
- components [Reporting Services], about components
- Reporting Services, components
- SSRS, components
- reports [Reporting Services], tools
- SQL Server Reporting Services, components
- SQL Server Reporting Services, tools
- architecture [Reporting Services]
ms.assetid: 23d616e3-eb90-43fb-9b7a-869bd7e22e7b
caps.latest.revision: 
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d5027e12a7cc0bfe310c4eb6b291667cfa4d0c4f
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="reporting-services-tools"></a>Herramientas de Reporting Services
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] contiene un conjunto de herramientas gráficas y de scripting que admiten el desarrollo y la utilización de informes completos en un entorno administrado. El conjunto de herramientas incluye herramientas de desarrollo, herramientas de configuración y administración, y herramientas de visualización de informes. Este tema proporciona una breve información general de cada herramienta de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y cómo se puede obtener acceso a ella.  
  
 Para buscar una herramienta inmediatamente, vea [Tutorial: Cómo buscar e iniciar herramientas de Reporting Services &#40;SSRS&#41;](../../reporting-services/tools/tutorial-how-to-locate-and-start-reporting-services-tools-ssrs.md).  
  
## <a name="tools-for-report-authoring"></a>Herramientas de creación de informes  
 En la tabla siguiente se enumeran las herramientas disponibles para la creación de informes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Herramienta|Description|Cómo obtener acceso|  
|----------|-----------------|-------------------|  
|[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long-md.md)]|Con [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short-md.md)], puede crear informes móviles que ajustan dinámicamente el contenido a la pantalla o a la ventana del explorador y escalarlos perfectamente a cualquier tamaño de pantalla.<br /><br /> Cree informes móviles en una superficie de diseño con cuadrícula ajustable de filas y columnas y elementos flexibles de informes móviles.<br /><br /> Para más información, vea [Creación y publicación de informes móviles con el Publicador de informes móviles de SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md).|Descargue el [Publicador de informes móviles de SQL Server](http://go.microsoft.com/fwlink/?LinkId=733527)|  
|[!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)]|Una exploración interactiva de los datos y una experiencia de presentación visual diseñadas para permitirle crear e interactuar con los informes basados en modelos tabulares de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en modo de SharePoint Explorador con Silverlight.|  
|Diseñador de informes|Use esta herramienta para diseñar informes. Incluye las características siguientes:<br /><br /> Implementar en un servidor de informes en modo SharePoint o modo nativo.<br /><br /> Se hospeda en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]<br /><br /> Panel Datos de informe para organizar los datos usados en el informe<br /><br /> Vistas con pestañas Diseño y Vista previa para el diseño de informe interactivo<br /><br /> Diseñadores de consultas asociados con los tipos de origen de datos en [RSReportDesigner Configuration File](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)para ayudar a especificar qué datos se deben recuperar de los orígenes de datos<br /><br /> Editor de expresiones con IntelliSense para generar expresiones de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que personalizan el contenido y el aspecto del informe<br /><br /> Admite elementos de informe personalizados y diseñadores de consultas personalizados<br /><br /> <br /><br /> Para obtener más información, vea [Reporting Services en SQL Server Data Tools &#40;SSDT&#41;](../../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md).|[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]|  
|Generador de informes|Use esta herramienta para diseñar informes. Incluye las características siguientes:<br /><br /> Implementar en un servidor de informes en modo SharePoint o modo nativo.<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] Entorno de creación parecido a Office[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long-md.md)]<br /><br /> Capacidad de guardar los elementos de informe como tales<br /><br /> Un asistente para crear mapas<br /><br /> Agregados de agregados<br /><br /> Compatibilidad mejorada para las expresiones<br /><br /> Diseñadores de consultas para ayudar a especificar los datos que deben recuperarse de una selección de tipos de orígenes de datos integrados<br /><br /> Para más información, vea [Generador de informes en SQL Server 2016](../../reporting-services/report-builder/report-builder-in-sql-server-2016.md).|Descargue la [versión independiente del Generador de informes](http://go.microsoft.com/fwlink/?LinkID=219138).<br /><br /> O ábralo desde el Administrador de informes o SharePoint.|  
  
## <a name="tools-for-report-server-administration"></a>Herramientas para la administración del servidor de informes  
 Hay disponible un conjunto de herramientas gráficas y de scripting para administrar el servidor de informes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Las herramientas que se usan dependen del modo de implementación del servidor de informes.  
  
### <a name="native-mode"></a>Modo nativo  
 En la tabla siguiente se hace una lista de las herramientas disponibles para administrar el servidor de informes que se implementa en modo nativo.  
  
|Herramienta|Description|Cómo obtener acceso|  
|----------|-----------------|-------------------|  
|Administrador de configuración de Reporting Services|Use esta herramienta para configurar una instalación de Reporting Services. Entre las tareas disponibles se incluyen:<br /><br /> Configuración de las instancias local y remota del servidor de informes<br /><br /> Configurar la cuenta de servicio del servidor de informes.<br /><br /> Crear y configurar una o más direcciones URL de servicios web.<br /><br /> Configurar la dirección URL del Administrador de informes<br /><br /> Crear y configurar la base de datos del servidor de informes.<br /><br /> Configurar una implementación escalada.<br /><br /> Realizar copias de seguridad, restaurar o reemplazar la clave simétrica que se usa para cifrar las cadenas de conexión almacenadas y las credenciales.<br /><br /> Configurar la cuenta de ejecución desatendida.<br /><br /> Configurar un servidor SMTP para la entrega por correo electrónico.<br /><br /> <br /><br /> Nota: El Administrador de configuración de Reporting Services no ayuda a administrar el contenido del servidor de informes, a habilitar características adicionales o a conceder acceso al servidor.<br /><br /> Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).|Menú Inicio|  
|SQL Server Management Studio|Use esta herramienta para administrar una o varias instancias del servidor de informes en un entorno único, lo que incluye:<br /><br /> Administrar las instancias local y remota del servidor de informes<br /><br /> Establecer las propiedades del servidor de informes<br /><br /> Modificar las definiciones de roles<br /><br /> Desactivar las características del servidor de informes que no se están usando<br /><br /> Administrar trabajos<br /><br /> Administrar las programaciones compartidas|Menú Inicio|  
|Administrador de configuración de SQL Server|Use esta herramienta para lo siguiente:<br /><br /> Iniciar y detener los servicios de Reporting Services de Windows<br /><br /> Configurar los informes de comentarios de clientes, el directorio de volcado y los informes de errores<br /><br /> <br /><br /> **\*\* Advertencia \*\***No use esta herramienta para configurar una cuenta de servicio. En lugar de ello, use la herramienta Configuración de Reporting Services.<br /><br /> Para obtener más información, vea [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).|Menú Inicio|  
|Utilidad rsconfig|Use esta herramienta para configurar y administrar una conexión del servidor de informes a la base de datos del servidor de informes. También puede utilizarla para especificar la cuenta de usuario que se va a utilizar para el procesamiento de informes desatendidos.<br /><br /> Para más información, vea [Utilidades del símbolo del sistema del servidor de informes &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Símbolo del sistema|  
|Utilidad Rskeymgmt|Use esta herramienta para lo siguiente:<br /><br /> Extraer, restaurar, crear y eliminar la clave simétrica usada para cifrar datos del servidor de informes<br /><br /> Combinar instancias del servidor de informes en una implementación escalada<br /><br /> <br /><br /> Para más información, vea [Utilidades del símbolo del sistema del servidor de informes &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Símbolo del sistema|  
|Clases de Instrumental de administración de Windows (WMI)|Use estas clases para automatizar las tareas de configuración en el administrador de configuración de Reporting Services sin necesidad de usar la interfaz gráfica de usuario.<br /><br /> Para obtener más información, vea [Accessing the WMI Provider Programmatically](../../reporting-services/accessing-the-wmi-provider-programmatically.md).|Script de Visual Basic|  
  
### <a name="sharepoint-integrated-mode"></a>Modo integrado de SharePoint  
 En modo de SharePoint, Reporting Services es una aplicación de servicio de la arquitectura de SharePoint y se administra directamente a través de SharePoint  
  
|Herramienta|Description|Cómo obtener acceso|  
|----------|-----------------|-------------------|  
|Administración central de SharePoint|Use la Administración central de SharePoint para crear, consultar, y administrar las aplicaciones de servicio compartidas para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Para obtener más información, vea [Configuración y administración de un servidor de informes &#40;modo de SharePoint de Reporting Services&#41;](../../reporting-services/report-server-sharepoint/configuration-and-administration-of-a-report-server.md).|Explorador para la dirección URL del sitio de SharePoint para administración central|  
|Cmdlets de PowerShell|Use cmdlets de PowerShell para crear, consultar y administrar las aplicaciones de servicio compartido para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> Para obtener más información, vea [Cmdlets de PowerShell para el modo de SharePoint de Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).|Shell de administración de SharePoint 2010|  
  
## <a name="tools-for-report-content-management"></a>Herramientas para la administración de contenido del informe  
 Hay disponible un conjunto de herramientas gráficas y de scripting para administrar el contenido en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Las herramientas que se usan dependen del modo de implementación del servidor de informes.  
  
|Herramienta|Description|Cómo obtener acceso|  
|----------|-----------------|-------------------|  
|Dirección URL del servicio web del servidor de informes|Use esta herramienta para examinar el contenido del catálogo de informes en un panel de navegación genérico del elemento.<br /><br /> Para obtener más información, vea [Report Server Web Service](../../reporting-services/report-server-web-service/report-server-web-service.md).|Browser|  
|Portal web|**(Solo modo nativo)** Use esta herramienta para administrar una única instancia del servidor de informes desde una ubicación remota con una conexión HTTP. Puede hacer lo siguiente:<br /><br /> Ver, buscar, imprimir y suscribirse a informes.<br /><br /> Crear, proteger y mantener la jerarquía de carpetas para organizar elementos en el servidor.<br /><br /> Configurar una seguridad basada en roles que determine el acceso a elementos y operaciones.<br /><br /> Configurar propiedades de ejecución del informe, historial del informe y parámetros del informe.<br /><br /> Crear modelos de informe que se conectan a un origen de datos de Microsoft SQL Server Analysis Services o a un origen de datos relacionales de SQL Server y recuperan los datos.<br /><br /> Establecer la seguridad de los elementos del modelo para permitir el acceso a entidades concretas del modelo o asignar entidades a informes click-through predefinidos creados previamente.<br /><br /> Crear programaciones compartidas y orígenes de datos compartidos para que las programaciones y las conexiones de orígenes de datos sean más fáciles de administrar.<br /><br /> Crear suscripciones controladas por datos que distribuyen informes en una lista de destinatarios extensa.<br /><br /> Crear informes vinculados para volverlos a utilizar y cambiar la finalidad de un informe existente de distintas maneras.<br /><br /> Iniciar el Generador de informes para crear informes que se pueden guardar y ejecutar en el servidor de informes. Para más información, vea [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md).| Browser  
|Utilidad RS|Esta herramienta es un host de script que se puede usar para llevar a cabo operaciones de script. Utilice esta herramienta para ejecutar scripts de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que copian datos entre distintas bases de datos del servidor de informes, publican informes, crean elementos en una base de datos del servidor de informes, etc. Para más información, vea [Utilidades del símbolo del sistema del servidor de informes &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md).|Símbolo del sistema|  
  
## <a name="see-also"></a>Ver también  
 [Servidor de informes de Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [Conceptos de Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [Reporting Services &#40;SSRS&#41;](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
