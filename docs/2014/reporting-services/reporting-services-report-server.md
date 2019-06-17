---
title: Servidor de informes de servicios de informes | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], extensions
- report servers [Reporting Services], about report server
- rendering extensions [Reporting Services], about extensions
- extensions [Reporting Services], about extensions
- storing data [Reporting Services]
- report servers [Reporting Services]
- data processing extensions [Reporting Services], about extensions
- delivery extensions [Reporting Services], about extensions
- data storage [Reporting Services]
- components [Reporting Services], report server
- report processing [Reporting Services], extensions
- Web service [Reporting Services], report server
- storage [Reporting Services]
ms.assetid: 88ed5b97-1d28-4980-80e4-b36761f3c03a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f7a16507855e5f17674fc76f7238e3e6b32a6d16
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102818"
---
# <a name="reporting-services-report-server"></a>Servidor de informes de Reporting Services
  En este tema se ofrece información general del servidor de informes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , el componente central de una instalación de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Está compuesto por un par de motores de procesamiento, además de una serie de extensiones con finalidades especiales que administran la autenticación, el procesamiento de datos, la representación y las operaciones de entrega. Un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se ejecuta en uno de dos modos de implementación: modo nativo o modo de SharePoint. Consulte la sección [Comparación de características de SharePoint en modo nativo](#bkmk_featuresupport) para obtener una comparación de las características.  
  
 **Instalación:** Para obtener información sobre [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalación, consulte lo siguiente:  
  
-   [Instalar el servidor de informes en modo nativo de Reporting Services](install-windows/install-reporting-services-native-mode-report-server.md)  
  
-   [Instalar las características SQL Server BI con SharePoint &#40;PowerPivot y Reporting Services&#41;](../../2014/sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
  
 **Windows Azure**: Para obtener información sobre cómo usar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] con Microsoft Azure Virtual Machines, consulte la información siguiente.  
  
-   [Business Intelligence de SQL Server en Máquinas virtuales de Windows Azure](https://msdn.microsoft.com//library/windowsazure/jj992719.aspx).  
  
-   [Usar PowerShell para crear una máquina virtual de Windows Azure con un servidor de informes en modo nativo](https://msdn.microsoft.com/library/windowsazure/dn449661.aspx).  
  
##  <a name="bkmk_top"></a> En este tema  
  
-   [Información general de los modos de servidor de informes](#bkmk_overview)  
  
-   [Comparación de características de SharePoint y modo nativo](#bkmk_featuresupport)  
  
-   [Modo nativo](#bkmk_nativemode)  
  
-   [Modo nativo con elementos Web de SharePoint](#bkmk_nativewithwebparts)  
  
-   [Modo de SharePoint](#bkmk_sharepointmode)  
  
-   [Procesos, el proceso de entrega y programación de informes](#bkmk_reportprocessor)  
  
-   [Base de datos del servidor de informes](#bkmk_reportdatabase)  
  
-   [Autenticación, representación, datos y las extensiones de entrega](#bkmk_authentication)  
  
-   [Tareas relacionadas](#bkmk_relatedtasks)  
  
##  <a name="bkmk_overview"></a> Información general de los modos de servidor de informes  
 Los motores de procesamiento (procesadores) son el núcleo del servidor de informes. Los procesadores admiten la integridad del sistema de informes y no se pueden modificar ni ampliar. Las extensiones son también procesadores, pero realizan funciones muy específicas. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] incluye una o varias extensiones predeterminadas para cada tipo de extensión admitida. Puede agregar extensiones personalizadas a un servidor de informes. Ello permite extender un servidor de informes para que admita características que requieren adaptaciones. Ejemplos de funcionalidad personalizada pueden ser la compatibilidad con tecnologías de inicio de sesión único, la salida de informes en formatos de aplicación no controlados por las extensiones de representación predeterminadas, y la entrega de informes a una impresora o aplicación.  
  
 Una instancia de servidor de informes único se define como el conjunto completo de procesadores y extensiones que proporcionan el procesamiento de un extremo a otro, desde el control de la solicitud inicial a la presentación de un informe acabado. A través de sus subcomponentes, el servidor de informes procesa solicitudes de informes y permite que los informes estén disponibles para el acceso a petición o la distribución programada.  
  
 Por lo que respecta a su funcionalidad, los servidores de informes permiten crear, representar y entregar informes en una gran variedad de orígenes de datos, así como de esquemas de autenticación y autorización extensibles. Además, los servidores de informes contienen las bases de datos del servidor de informes que almacenan informes publicados, orígenes de datos compartidos, conjuntos de datos compartidos, elementos de informes, programaciones compartidas, suscripciones, archivos de origen de definición de informes, definiciones de modelos, informes compilados, instantáneas, parámetros y otros recursos. Los servidores de informes permiten además realizar tareas de administración para configurar el servidor de informes a fin de procesar las solicitudes de informes y mantener los historiales de instantáneas, así como administrar los permisos de los informes, los orígenes de datos, los conjuntos de datos y las suscripciones.  
  
 Un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] admite dos modos de implementación de las instancias del servidor de informes:  
  
-   **Modo nativo**: incluido el modo nativo con elementos web de SharePoint, donde un servidor de informes se ejecuta como un servidor de aplicaciones que proporciona todas las capacidades de procesamiento y administración exclusivamente a través de los componentes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Para configurar un servidor de informes en modo nativo se usa el administrador de configuración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y SQL Server Management Studio.  
  
-   **Modo de SharePoint**: donde un servidor de informes se instala como parte de una granja de servidores de SharePoint.  Implemente y configure el modo de SharePoint mediante comandos de PowerShell o páginas de administración de contenido de SharePoint.  
  
 En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , no se puede cambiar un servidor de informes de un modo a otro. Si desea cambiar el tipo de servidor de informes que usa su entorno, debe instalar el modo que desee y, a continuación, copiar o mover los elementos de informe o la base de datos del servidor de informes de la versión anterior a la nueva. Este proceso se conoce normalmente como "migración". Los pasos necesarios para la migración dependen del modo al que se realice la migración y la versión desde la que se migre. Para obtener más información, vea [Upgrade and Migrate Reporting Services](install-windows/upgrade-and-migrate-reporting-services.md).  
  
##  <a name="bkmk_featuresupport"></a> Comparación de características de SharePoint y modo nativo  
  
|Componente o característica|Modo nativo|Modo SharePoint|  
|--------------------------|-----------------|---------------------|  
|**Direcciones URL**|Sí|El direccionamiento de direcciones URL es distinto en el modo integrado de SharePoint. Las direcciones URL de SharePoint se utilizan para hacer referencia a informes, modelos de informe, orígenes de datos compartidos y recursos. No se utiliza la jerarquía de carpetas del servidor de informes. Si tiene aplicaciones personalizadas que dependen del acceso de direcciones URL como las admitidas en un servidor de informes en modo nativo, esa funcionalidad ya no funcionará cuando el servidor de informes se configure para la integración de SharePoint.<br /><br /> Para más información sobre el acceso URL, vea [Referencia de parámetros de acceso URL](url-access-parameter-reference.md).|  
|**Extensiones de seguridad personalizadas**|Sí|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en el servidor de informes. El servidor de informes incluye una extensión de seguridad para fines especiales que se utiliza siempre que se configura un servidor de informes para que se ejecute en el modo integrado de SharePoint. Esta extensión de seguridad es un componente interno que se requiere para las operaciones integradas.|  
|**Administrador de configuración**|Sí|**\*\* Importante \*\*** El Administrador de configuración no se puede usar para administrar un servidor de informes en modo de SharePoint. En su lugar, utilice Administración central de SharePoint.|  
|**Administrador de informes**|Sí|El Administrador de informes no se puede usar para administrar el modo de SharePoint. Use las páginas de aplicación de SharePoint. Para más información, vea [Aplicaciones de servicio y servicio de SharePoint de Reporting Services](../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md).|  
|**Informes vinculados**|Sí|No.|  
|**Mis informes**|Sí|No|  
|**Mis suscripciones** y métodos de procesamiento por lotes.|Sí|No|  
|**Alertas de datos**|Sin|Sí|  
|**Power View**|Sin|Sí<br /><br /> Requiere Silverlight en el explorador cliente. Para obtener más información sobre los requisitos del explorador, vea [planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)|  
|**Informes .RDL**|Sí|Sí<br /><br /> Los informes .RDL pueden ejecutarse en servidores de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo nativo o en modo de SharePoint.|  
|**Informes .RDLX**|No|Sí<br /><br /> Los informes .RDLX de Power View solo pueden ejecutarse en servidores de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo de SharePoint.|  
|**Credenciales de token de usuario de SharePoint para la extensión de lista de SharePoint**|Sin|Sí|  
|**Zonas de AAM para implementaciones con conexión a Internet**|No|Sí|  
|**Copias de seguridad y recuperación de SharePoint**|Sin|Sí|  
|**Compatibilidad con registros de ULS**|Sin|Sí|  
  
##  <a name="bkmk_nativemode"></a> Modo nativo  
 En el modo nativo, un servidor de informes es un servidor de aplicaciones independiente que proporciona todas las operaciones de visualización, administración, procesamiento y entrega de informes y modelos de informe. Se trata del modo predeterminado para las instancias del servidor de informes. Puede instalar un servidor de informes en modo nativo que se configure durante la instalación o puede configurarlo para las operaciones en modo nativo una vez completado el programa de instalación.  
  
 En el diagrama siguiente se muestra la arquitectura de tres niveles de una implementación en modo nativo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Muestra la base de datos del servidor de informes y los orígenes de datos en el nivel de datos, los componentes del servidor de informes en el nivel intermedio y las aplicaciones cliente y herramientas integradas o personalizadas en el nivel de presentación. Presenta el flujo de solicitudes y datos entre componentes del servidor y los componentes que envían y recuperan contenido de un almacén de datos.  
  
 ![Arquitectura de Reporting Services](media/reporting-serv-arch.gif "Arquitectura de Reporting Services")  
  
 El servidor de informes se implementa como un servicio de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows, denominado "servicio del servidor de informes", que hospeda un servicio web, el procesamiento en segundo plano y otras operaciones. En la aplicación de consola Servicios, el servicio se muestra como SQL Server Reporting Services (MSSQLSERVER).  
  
 Los programadores de otros fabricantes pueden crear extensiones adicionales para reemplazar o ampliar la capacidad de procesamiento del servidor de informes. Para obtener más información acerca de las interfaces de programación disponibles para los desarrolladores de aplicaciones, vea la [Referencia técnica](../../2014/reporting-services/technical-reference-ssrs.md).  
  
###  <a name="bkmk_nativewithwebparts"></a> Modo nativo con elementos Web de SharePoint  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona dos elementos Web que puede instalar y registrar en una instancia de [!INCLUDE[winSPServ](../includes/winspserv-md.md)] 2.0 o posterior, o SharePoint Portal Server 2003 o posterior. Desde un sitio de SharePoint, puede utilizar los elementos web para buscar y ver informes almacenados y procesados en el servidor de informes que se ejecuta en modo nativo. Estos elementos web se incluyeron en versiones anteriores de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
##  <a name="bkmk_sharepointmode"></a> Modo de SharePoint  
 En el modo de SharePoint, un servidor de informes se debe ejecutar en una granja de servidores de SharePoint. Las características de administración, representación y procesamiento del servidor de informes se representan mediante un servidor de aplicaciones de SharePoint que ejecuta el servicio compartido [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y una o varias aplicaciones de servicio [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Un sitio de SharePoint proporciona el acceso front-end al contenido y las operaciones del servidor de informes.  
  
 El modo de SharePoint requiere:  
  
-   [!INCLUDE[SPF2010](../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../includes/sps2010-md.md)].  
  
-   Una versión adecuada del Complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para Productos de SharePoint 2010.  
  
-   Un servidor de aplicaciones de SharePoint con el servicio compartido [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalado y al menos una aplicación de servicio [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
 En la ilustración siguiente se muestra un entorno de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo de SharePoint.  
  
 ![Arquitectura funcional de SSRS SharePoint](media/rs-sharepoint-architecture.gif "Arquitectura funcional de SSRS SharePoint")  
  
||Descripción|  
|-|-----------------|  
|**(1)**|Varios servidores web o front-end web (WFE). El complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] debe instalarse en cada servidor web cuyas características de aplicaciones web desea usar, por ejemplo, la visualización de informes o páginas de administración de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para tareas como administrar los orígenes de datos o las suscripciones.|  
|**(2)**|El complemento instala los extremos SOAP y las direcciones URL para que los clientes se comuniquen con los servidores de aplicaciones a través de un proxy de servicio de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|  
|**(3)**|Los servidores de aplicaciones ejecutan el servicio compartido [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . La escala del procesamiento de informes se administra como parte de la granja de SharePoint y agregando el servicio [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] a servidores de aplicaciones adicionales.|  
|**(4)**|Se puede crear más de una aplicación de servicio de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] con diferentes configuraciones, incluidos los permisos, el correo electrónico, el proxy y las suscripciones.|  
|**(5)**|Los informes, orígenes de datos, y otros elementos se almacenan en las bases de datos de contenido de SharePoint.|  
|**(6)**|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] crean tres bases de datos para las características de alertas de datos, temporales y el servidor de informes. Las opciones de configuración que se aplican a todas las aplicaciones de servicio de SSRS se almacenan en el archivo **RSReportserver.config** .|  
  
##  <a name="bkmk_reportprocessor"></a> Procesos, el proceso de entrega y programación de informes  
 El servidor de informes incluye dos motores de procesamiento que realizan el procesamiento de informes previo e intermedio, así como operaciones programadas y de entrega. El Procesador de informes recupera la definición o el modelo de informe, combina información de diseño con datos de la extensión de procesamiento de datos y representa el informe en el formato solicitado. El proceso de entrega y programación procesa los informes desencadenados a partir de una programación y los entrega a los destinos.  
  
##  <a name="bkmk_reportdatabase"></a> Base de datos de servidor de informes  
 El servidor de informes es un servidor sin estado que almacena todas las propiedades, objetos y metadatos de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Los datos almacenados incluyen informes publicados, informes compilados, modelos de informe y la jerarquía de carpetas que proporciona el direccionamiento de todos los elementos que administra el servidor de informes. Una base de datos del servidor de informes puede proporcionar almacenamiento interno para una única instalación de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] o para varios servidores de informes que formen parte de la implementación escalada. Si configura un servidor de informes para ejecutarse en una implementación más amplia de un producto o tecnología de SharePoint, el servidor de informes usa las bases de datos de SharePoint además de la base de datos del servidor de informes. Para más información sobre los almacenes de datos usados en la instalación de Reporting Services, vea [Base de datos del servidor de informes &#40;Modo nativo de SSRS&#41;](report-server/report-server-database-ssrs-native-mode.md).  
  
##  <a name="bkmk_authentication"></a> Autenticación, representación, datos y las extensiones de entrega  
 El servidor de informes admite los siguientes tipos de extensiones: extensiones de autenticación, extensiones de procesamiento de datos, extensiones de procesamiento de informes, extensiones de representación y extensiones de entrega. Un servidor de informes requiere al menos una extensión de autenticación, una extensión de procesamiento de datos y una extensión de representación. Las extensiones de procesamiento de informes personalizadas y de entregas son opcionales, pero necesarias si desea admitir controles personalizados o de distribución de informes.  
  
 Reporting Services proporciona extensiones predeterminadas para que se puedan utilizar todas las características de servidor sin tener que desarrollar componentes personalizados. En la tabla siguiente se describen las extensiones predeterminadas que contribuyen a una instancia del servidor de informes completa con la funcionalidad lista para su uso:  
  
|Tipo|Default|  
|----------|-------------|  
|Autenticación|Una instancia del servidor de informes predeterminada admite la autenticación de Windows, incluso las características de suplantación y delegación si están habilitadas en el dominio.|  
|Procesamiento de datos|Una instancia del servidor de informes predeterminada incluye extensiones de procesamiento de datos para orígenes de datos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, Hyperion Essbase, SAPBW, OLE DB, Almacenamiento de datos paralelo y ODBC.|  
|Representación|Una instancia del servidor de informes predeterminada incluye extensiones de representación para HTML, Excel, CSV, XML, Image, Word, lista SharePoint y PDF.|  
|Entrega|Una instancia de servidor de informes predeterminada contiene una extensión de entrega por correo electrónico y una extensión de entrega a recursos compartidos de archivos. Si el servidor de informes se configura para la integración de SharePoint, puede utilizar una extensión de entrega que guarde los informes en una biblioteca de SharePoint.|  
  
> [!NOTE]  
>  Reporting Services incluye un completo conjunto de herramientas y aplicaciones que se pueden utilizar para administrar el servidor, crear contenido y poner el contenido a disposición de los usuarios de la organización.  
  
##  <a name="bkmk_relatedtasks"></a> Tareas relacionadas  
 Los temas siguientes proporcionan información adicional sobre cómo instalar, usar y mantener un servidor de informes:  
  
|Tarea|Vínculo|  
|----------|----------|  
|Revisar los requisitos de hardware y software.|[Hardware and Software Requirements for Reporting Services in SharePoint Mode](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md).|  
|Instalar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en modo de SharePoint.|[Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)|  
|Si es un programador web o tiene experiencia creando hojas de estilos en cascada, puede modificar los estilos predeterminados bajo su responsabilidad para cambiar los colores, las fuentes y el diseño de la barra de herramientas o el Administrador de informes. En esta versión no se documentan las hojas de estilos predeterminadas ni las instrucciones para modificarlas.|[Personalizar hojas de estilos para el Visor HTML y el Administrador de informes](../../2014/reporting-services/customize-style-sheets-for-html-viewer-and-report-manager.md)|  
|Los desarrolladores web que están familiarizados con estilos HTML y las hojas de estilos en cascada (CSS) pueden usar la información de este tema para determinar qué archivos se pueden modificar para personalizar el aspecto del Administrador de informes.|[Configurar el Administrador de informes para pasar cookies de autenticación personalizadas](security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)|  
|Explica cómo ajustar la configuración de memoria para el servicio web del servidor de informes y el servicio de Windows.|[Configurar la memoria disponible para las aplicaciones del servidor de informes](report-server/configure-available-memory-for-report-server-applications.md)|  
|Explica los pasos recomendados para configurar el servidor de informes para la administración remota.|[Configurar un servidor de informes para la administración remota](report-server/configure-a-report-server-for-remote-administration.md)|  
|Proporciona instrucciones para configurar la disponibilidad de **Mis informes** en una instancia del servidor de informes nativo.|[Habilitar y deshabilitar Mis informes](report-server/enable-and-disable-my-reports.md)|  
|Proporciona las instrucciones para configurar el control RSClientPrint que proporciona la funcionalidad de impresión desde dentro de los exploradores admitidos. Para obtener más información sobre los requisitos del explorador, vea [planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).|[Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](report-server/enable-and-disable-client-side-printing-for-reporting-services.md)|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](extensions/reporting-services-extensions.md)   
 [Herramientas de Reporting Services](tools/reporting-services-tools.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Base de datos del servidor de informes &#40;Modo nativo de SSRS&#41;](report-server/report-server-database-ssrs-native-mode.md)   
 [Implementar una extensión de seguridad](extensions/security-extension/implementing-a-security-extension.md)   
 [Implementar una extensión de procesamiento de datos](extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Cómo administrar SSRS con PowerShell](https://sqlbelle.wordpress.com/2015/08/17/automate-ssrs-report-generation-using-powershell/)  
  
  
