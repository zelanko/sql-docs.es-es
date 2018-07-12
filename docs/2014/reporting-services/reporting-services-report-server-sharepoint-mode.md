---
title: Servidor de informes de Reporting Services (modo de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 10778ec9-5fe4-4b4e-89b0-ade1f06b781d
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4a41599128d6b0f9bbceaa47a30d851e312f39e3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37168136"
---
# <a name="reporting-services-report-server-sharepoint-mode"></a>Servidor de informes de Reporting Services (modo de SharePoint)
  Un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] configurado para el **modo de SharePoint** puede ejecutarse en una implementación de un producto de SharePoint. Un servidor de informes en modo de SharePoint puede usar las características de colaboración y administración de SharePoint para los informes y otros [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] tipos de contenido. El modo de SharePoint requiere la instalación de la versión apropiada del complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para los productos de SharePoint en los front-end web de SharePoint.  
  
 Para obtener información sobre la instalación y la configuración, vea lo siguiente:  
  
-   [Instalar el modo de SharePoint de Reporting Services para SharePoint 2013](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
-   [Instalar el modo de SharePoint de Reporting Services para SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
-   [Agregar un servidor de informes adicional a una granja &#40;escalada SSRS&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).  
  
 Para obtener información sobre cuáles son las novedades en esta versión, vea la sección 'SharePoint' en [What ' s New &#40;Reporting Services&#41;](../../2014/reporting-services/what-s-new-reporting-services.md).  
  
 **En este tema:**  
  
-   [Resumen de características](#bkmk_featuresum)  
  
-   [Modo conectado y modo local](#bkmk_connectedandlocal)  
  
-   [Características de SharePoint no admitidas](#bkmk_unsupportedsharepoint)  
  
-   [Combinaciones admitidas del complemento de SharePoint y el servidor de informes](#bkmk_supportedcombinations)  
  
-   [Componentes que proporcionan integración](#bkmk_components)  
  
-   [Consideraciones de idioma](#bkmk_language)  
  
-   [Tareas relacionadas](#bkmk_relatedtasks)  
  
##  <a name="bkmk_featuresum"></a> Resumen de características  
 Configurar un servidor de informes para que se ejecute en el modo integrado de SharePoint proporciona la siguiente funcionalidad adicional, que solo está disponible al implementar un servidor de informes en este modo:  
  
-   Uso de las características de administración de documentos y colaboración de SharePoint, incluidas las alertas. Un sitio de SharePoint proporciona un portal unificado para obtener acceso y administrar todos los elementos de informe en un único lugar.  
  
-   Uso de proveedores de autenticación y permisos de SharePoint para controlar el acceso a informes, modelos y otros elementos.  
  
-   Uso de topologías de implementación de SharePoint para distribuir informes a través de una conexión a Internet desde fuera del firewall. Un servidor de informes proporciona servicios de procesamiento de datos e informes en el contexto de una implementación de SharePoint de mayor tamaño configurada para el acceso a Internet.  
  
-   Administración de informes, modelos, orígenes de datos, programaciones e historial de informes en páginas de aplicación personalizadas en un sitio de SharePoint. Puede establecer propiedades, definir programaciones y suscripciones, y crear y administrar el historial de informes en un sitio de SharePoint del mismo modo que los crearía y administraría desde otras herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Publicación o carga de informes, modelos de informes, recursos y archivos de orígenes de datos compartidos en una biblioteca de SharePoint, incluido el Centro de informes de Office SharePoint Server.  
  
     Uso del Diseñador de informes, el Diseñador de modelos y el Generador de informes para crear informes y orígenes de datos que se van a publicar directamente en una biblioteca de SharePoint. También puede utilizar la acción Cargar de un sitio de SharePoint para agregar cualquier definición de informe y modelos de informe a una biblioteca de SharePoint.  
  
     Como el servidor de informes procesa las definiciones de informe de la misma forma, independientemente del modo de servidor que se utilice, los datos y el diseño de informe no se ven afectados por el modo de servidor. Cualquier informe que pueda ejecutarse en un servidor de informes en modo nativo podrá ejecutarse en un servidor de informes configurado para el modo integrado de SharePoint.  
  
-   Suscripción y entrega de informes a una biblioteca de SharePoint mediante el uso de una nueva extensión de entrega de SharePoint. También puede entregar informes a través de correo electrónico o en una carpeta compartida. Las extensiones de entrega del servidor de informes se utilizan para entregar informes. Puede crear suscripciones controladas por datos para la distribución de informes a gran escala utilizando datos del suscriptor consultados en tiempo de ejecución.  
  
-   Un elemento web Visor de informes que puede agregar a las páginas de SharePoint para ver un informe dentro de una aplicación web de SharePoint. El elemento web incluye características de navegación en páginas, búsqueda, impresión y exportación.  
  
-   Programación con un nuevo extremo SOAP para crear aplicaciones personalizadas que se integren con un sitio de SharePoint. También puede utilizar el proveedor de Instrumental de administración de Windows (WMI) actualizado para configurar mediante programación una instancia de servidor de informes que se ejecute en el modo integrado de SharePoint.  
  
-   Creación de informes de servicio de Microsoft Access en modo conectado.  
  
-   Zonas de AAM, implementaciones con conexión a Internet y tokens de usuario de SharePoint para listas de SharePoint.  
  
##  <a name="bkmk_connectedandlocal"></a> Modo conectado y modo local  
 La versión SQL Server 2008 R2 presentó un nuevo *modo local* para ver informes desde un servidor de SharePoint 2010 que tenga instalado el complemento Reporting Services de Microsoft SQL Server 2008 R2 o posterior para productos de SharePoint 2010.  
  
-   *Modo local*: modo Local permite que los informes se representen localmente desde la biblioteca de documentos de SharePoint, sin integración con un [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] servidor de informes. Se requiere el complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para los productos de SharePoint. No se requiere un servidor de informes [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. El complemento se puede instalar de varias formas diferentes, incluida la herramienta de preparación de productos de SharePoint 2010. Para obtener más información sobre el modo local, vea [Informes en modo local frente al Modo conectado en el Visor de informes &#40;Reporting Services en modo de SharePoint&#41; ](../../2014/reporting-services/local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md) y [dónde encontrar el complemento de Reporting Services para productos de SharePoint](install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  
  
-   *Modo conectado*: modo conectado es compatible con la integración de un [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] servidor de informes en la granja de SharePoint mediante Administración Central de SharePoint. La integración con un servidor de informes habilita la creación de informes completos; proporciona las características de colaboración de SharePoint 2010 y las características basadas en servidor de un servidor de informes: suscripciones, instantáneas y procesamiento basado en servidor.  
  
##  <a name="bkmk_unsupportedsharepoint"></a> Características de SharePoint no admitidas  
 No todas las características de SharePoint se encuentran disponibles para las operaciones integradas. La siguiente es una lista de las características de SharePoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no se integra directamente:  
  
-   Servicio de almacenamiento seguro.  
  
-   No puede utilizar la integración del Calendario de Outlook de SharePoint ni la programación de SharePoint para los archivos de servicios de informes en una biblioteca de documentos.  
  
-   Catálogo de datos profesionales de SharePoint.  
  
-   La personalización de SharePoint tampoco se admite en las páginas de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. La integración del servidor de informes no se admite si la aplicación web de SharePoint está habilitada para el acceso anónimo.  
  
-   SQL Server Reporting Services **no** admite el control de versiones de la biblioteca de documentos de SharePoint. Si guarda los elementos de informe en una biblioteca de documentos configurada con el “Historial de versiones del documento” habilitado, las características de Reporting Services no funcionarán correctamente y generarán errores en el registro de ULS. A continuación se presenta un ejemplo de un error en el registro de ULS:  
  
    -   “…Se ha deshabilitado un origen de datos asociado al informe”.  
  
     El historial de versiones de la biblioteca de documentos se configura en la página “Configuración de versiones” de “Configuración de biblioteca”.  
  
##  <a name="bkmk_supportedcombinations"></a> Combinaciones admitidas del complemento de SharePoint y el servidor de informes  
 No todas las características se admiten en todas las combinaciones de servidor de informes, complemento de Reporting Services para SharePoint y productos de SharePoint. Para obtener más información, consulte [admite combinaciones de SharePoint y servidor de Reporting Services y complemento &#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md)  
  
> [!NOTE]  
>  Se debe utilizar la versión correcta del complemento Reporting Services con la versión correspondiente de Productos de SharePoint.  
  
##  <a name="bkmk_components"></a> Componentes que proporcionan integración  
 Para combinar los servidores en una sola implementación, una instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se integra con una instancia de productos de SharePoint.  
  
 Se proporciona integración a través de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] complemento para productos de SharePoint. El complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] es un componente de distribución gratuita que se puede descargar e instalarse a continuación en un servidor en el que se ejecute la versión apropiada de SharePoint.  
  
> [!TIP]  
>  No todas las características se admiten en todas las combinaciones de servidor de informes, complemento de Reporting Services para SharePoint y productos de SharePoint. Para obtener más información, vea [admite combinaciones de SharePoint y servidor de Reporting Services y complemento &#40;SQL Server 2014&#41;](install-windows/supported-combinations-of-sharepoint-and-reporting-services-server.md).  
  
-   En SharePoint, el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona el punto de conexión de proxy ReportServer, un elemento Web Visor de informes, complemento y páginas de aplicación para que pueda ver, almacenan y administración el contenido del servidor de informes en un sitio de SharePoint o granja de servidores.  
  
-   En [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona archivos de programa actualizados, un punto de conexión SOAP y las extensiones personalizadas de seguridad y la entrega. El servidor de informes debe configurarse para que se ejecute en el modo integrado de SharePoint, dedicado en exclusiva a admitir el acceso a informes y la entrega a través del sitio de SharePoint.  
  
 Una vez instalado el complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en SharePoint y configurados los dos servidores para la integración, puede cargar o publicar los tipos de contenido del servidor de informes en una biblioteca de SharePoint y, a continuación, ver y administrar esos documentos desde un sitio de SharePoint. Cargar o publicar el contenido de un servidor de informes es un primer paso importante; las páginas y el elemento web están disponibles cuando se seleccionan definiciones de informe (.rdl), modelos de informe (.smdl) y orígenes de datos compartidos (.rsds) en un sitio de SharePoint.  
  
##  <a name="bkmk_language"></a> Consideraciones de idioma  
 [!INCLUDE[SPF2010](../includes/spf2010-md.md)] y [!INCLUDE[SPS2010](../includes/sps2010-md.md)] productos están disponibles en muchos más idiomas que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 Cuando configure un servidor de informes para que se ejecute en una implementación de un producto de SharePoint, es probable que vea una combinación de idiomas. La interfaz de usuario, la documentación y los mensajes se mostrarán en los siguientes idiomas:  
  
-   Todas las páginas de aplicación, herramientas, errores, advertencias y mensajes que se originen a partir de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se mostrarán en el idioma utilizado por la instancia de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en uno de los idiomas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Las páginas de aplicación que abra en un sitio de SharePoint, el elemento web Visor de informes y el Generador de informes aparecerán en uno de los idiomas compatibles en el Complemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Para ver la lista de idiomas compatibles, vaya a la página de [descargas de SQL Server](http://msdn.microsoft.com/sql/downloads/) y busque la página de descarga del Complemento [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
-   Los sitios de SharePoint, la Administración central de SharePoint, la Ayuda en pantalla y los mensajes están disponibles en los idiomas compatibles con los productos Office Server.  
  
 Si el idioma de su producto de SharePoint o la tecnología difiere del idioma del servidor de informes, [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] intentará usar el idioma de la misma familia de idiomas que ofrece la coincidencia más cercana. Si no hay ningún idioma sustituto que se aproxime, el servidor de informes utilizará el inglés.  
  
##  <a name="bkmk_relatedtasks"></a> Tareas relacionadas  
 En la tabla siguiente se resumen las tareas relacionadas con un servidor de informes en modo de SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] :  
  
|**Tarea**|**Vínculo**|  
|--------------|--------------|  
|Pasos detallados para instalar y configurar [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en el modo de SharePoint.|[Instalar Reporting Services SharePoint Mode for SharePoint 2010](../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md) y [agregar un servidor de informes adicional a una granja &#40;escalada SSRS&#41;](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md).|  
|Escalar horizontalmente su [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] implementación de SharePoint mediante la adición de servidores de informes adicionales.|[Agregar un servidor de informes adicional a una granja &#40;escalada SSRS&#41; ](install-windows/add-an-additional-report-server-to-a-farm-ssrs-scale-out.md) y [Deployment Topologies for SQL Server BI Features in SharePoint](../sql-server/install/deployment-topologies-for-sql-server-bi-features-in-sharepoint.md) .|  
|Agregue front-end web de SharePoint adicionales que tengan los componentes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalados para ver e imprimir elementos.|[Incorporación de un front-end web adicional de Reporting Services a una granja de servidores](install-windows/add-an-additional-reporting-services-web-front-end-to-a-farm.md)|  
|Configure el correo electrónico para las características de alerta y suscripción de datos de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].|[Configurar el correo electrónico para la aplicación de servicio de Reporting Services &#40;SharePoint 2010 y SharePoint 2013&#41;](install-windows/configure-e-mail-for-a-reporting-services-service-application.md)|  
|Información reciente sobre esta versión, incluida en TechNet Wiki.|[Sugerencias, trucos y solución de problemas de SQL Server 2012 Reporting Services](http://go.microsoft.com/fwlink/?LinkId=221297).|  
  
## <a name="see-also"></a>Vea también  
 [Instalar o desinstalar el complemento Servicios de informes para SharePoint &#40;SharePoint 2010 y SharePoint 2013&#41;](install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)   
 [Requisitos de hardware y Software para Reporting Services en modo de SharePoint](../../2014/sql-server/install/hardware-and-software-requirements-for-reporting-services-in-sharepoint-mode.md)   
 [Elemento de Web del Visor de informes en un sitio de SharePoint](../../2014/reporting-services/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Cuestionario: Configurar SSRS 2012 para la integración de SharePoint](http://go.microsoft.com/fwlink/?LinkId=306443)  
  
  
