---
title: El Administrador de informes (modo nativo de SSRS) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/26/2019
ms.openlocfilehash: 55581ae96660732ee01bf12fa37e1c5e8ac9634e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "64568382"
---
# <a name="report-manager--ssrs-native-mode"></a>Administrador de informes (Modo nativo de SSRS)
  El Administrador de informes es una herramienta basada en Web para el acceso a informes y su administración que se utiliza para administrar una única instancia de servidor de informes desde una ubicación remota a través de una conexión HTTP. También puede utilizar el Administrador de informes por su visor de informes y sus características de navegación. En este tema:  
  
-   [¿Qué es el Administrador de informes?](#bkmk_whatis_report_manager)  
  
-   [Inicio y Use el Administrador de informes](#bkmk_start_report_manager)  
  
-   [Descripciones de los iconos](#bkmk_icon_descriptions)  
  
##  <a name="bkmk_whatis_report_manager"></a> ¿Qué es el Administrador de informes?  
 Puede utilizar el Administrador de informes para realizar las siguientes tareas:  
  
-   Ver, buscar, imprimir y suscribirse a informes.  
  
-   Crear, proteger y mantener la jerarquía de carpetas para organizar elementos en el servidor.  
  
-   Configurar una seguridad basada en roles que determine el acceso a elementos y operaciones.  
  
-   Configurar propiedades de ejecución del informe, historial del informe y parámetros del informe.  
  
-   Crear modelos de informe que se conectan a datos y recuperan datos de un origen de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o de un origen de datos relacional de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Establezca la seguridad de los elementos del modelo para permitir el acceso a entidades concretas del modelo o asigne entidades a informes click-through predefinidos creados previamente.  
  
-   Crear programaciones compartidas y orígenes de datos compartidos para que las programaciones y las conexiones de orígenes de datos sean más fáciles de administrar.  
  
-   Crear suscripciones controladas por datos que distribuyen informes en una lista de destinatarios extensa.  
  
-   Crear informes vinculados para volverlos a utilizar y cambiar la finalidad de un informe existente de distintas maneras.  
  
-   Iniciar el Generador de informes para crear informes que se pueden guardar y ejecutar en el servidor de informes.  
  
 Puede utilizar el Administrador de informes para examinar las carpetas del servidor de informes o buscar informes concretos. Puede ver un informe, con sus propiedades generales, así como pegar copias del informe capturadas en el historial del informe. Dependiendo de los permisos que tenga, también podría suscribirse a informes para su entrega en una bandeja de entrada de correo electrónico o en una carpeta compartida del sistema de archivos.  
  
> [!NOTE]  
>  Para obtener información sobre las versiones y exploradores admitidos, consulte [planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
 El Administrador de informes solamente se utiliza para un servidor de informes que se ejecuta en modo nativo. No se admite para un servidor de informes que se configure para el modo integrado de SharePoint.  
  
 Algunas características del Administrador de informes solo están disponibles en determinadas ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 En una instalación nueva, solo los administradores locales tienen permisos suficientes para trabajar con el contenido y la configuración. Para conceder permisos a otros usuarios, un administrador local debe crear asignaciones de roles que proporcionen acceso al servidor de informes. Las tareas y las páginas de aplicación a las que un usuario puede obtener acceso posteriormente dependerán de las asignaciones de roles para dicho usuario. Para más información, consulte [Conceder a un usuario acceso a un servidor de informes &#40;Administrador de informes&#41;](security/grant-user-access-to-a-report-server.md).  
  
 Si está usando [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] o Windows Server 2008, debe configurar el Administrador de informes para la administración local. Para más información, vea [Configurar un servidor de informes en modo nativo para la administración local &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
##  <a name="bkmk_start_report_manager"></a> Inicio y Use el Administrador de informes  
 El Administrador de informes es una aplicación web que abre escribiendo la dirección URL del Administrador de informes en la barra de direcciones de una ventana de explorador. Al iniciar el Administrador de informes, las páginas, vínculos y opciones que se ven varían en función de los permisos que se tengan en el servidor de informes. Para realizar una tarea, debe estar asignado a un rol que incluya la tarea. Un usuario asignado a un rol con permisos totales tiene acceso al conjunto completo de menús y páginas de la aplicación disponibles para administrar un servidor de informes. Un usuario asignado a un rol con permisos para ver y ejecutar informes solo ve los menús y las páginas que admiten dichas actividades. Cada usuario puede tener distintas asignaciones de roles para distintos servidores de informes o, incluso, para los distintos informes y carpetas almacenados en un único servidor de informes.  
  
 Para obtener más información sobre los roles, consulte [Conceder permisos en un servidor de informes en modo nativo](security/granting-permissions-on-a-native-mode-report-server.md).  
  
> [!NOTE]  
>  Si está utilizando Windows Vista o Windows Server 2008, debe configurar el servidor de informes para la administración local antes de utilizar el Administrador de informes para administrar una instancia del servidor de informes local. Para obtener instrucciones sobre cómo configurar el servidor, consulte [configurar un servidor de informes de modo nativo para la administración Local &#40;SSRS&#41;](report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="start-report-manager"></a>Iniciar el Administrador de informes  
  
#### <a name="to-start-report-manager-from-a-browser"></a>Para iniciar el Administrador de informes desde un explorador  
  
1.  Abra [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Explorer 7.0 o posterior.  
  
2.  En la barra de direcciones del explorador web, escriba la dirección URL del Administrador de informes.  
  
    -   De forma predeterminada, la dirección URL es `http://[ComputerName]/reports`.  
  
    -   El servidor de informes se puede configurar para usar un puerto concreto. Por ejemplo, `http:// [ComputerName]:80/reports` o `http:// [ComputerName]:8080/reports`.  
  
## <a name="configuring-report-manager"></a>Configurar el Administrador de informes  
 La configuración del Administrador de informes consiste en definir una dirección URL para la aplicación. Se requiere configuración adicional si la implementación incluye la ejecución del Administrador de informes en otro equipo.  
  
 Puede personalizar el Administrador de informes de maneras muy limitadas. Por ejemplo, puede modificar el título de la aplicación en la página Configuración del sitio. Si es un programador web, puede modificar las hojas de estilo que contienen la información del estilo que utiliza el Administrador de informes. Como el Administrador de informes no se diseñó específicamente para admitir personalización, debe analizar cuidadosamente cualquier modificación que realice. Si el Administrador de informes no satisface sus necesidades, puede desarrollar un visor de informes personalizado o configurar elementos Web de SharePoint para buscar y ver los informes en un sitio de SharePoint. Para obtener más información, vea [Configurar el Administrador de informes &#40;modo nativo&#41;](report-server/configure-web-portal.md).  
  
##  <a name="bkmk_icon_descriptions"></a> Descripciones de los iconos  
 En la tabla siguiente se describen los iconos que se usan en el Administrador de informes. Para obtener más información acerca de los iconos que aparecen en la barra de herramientas de informe, vea [Visor HTML y la barra de herramientas de informe](html-viewer-and-the-report-toolbar.md).  
  
|Icono|Descripción|Acción|  
|----------|-----------------|------------|  
|![Icono de informe](media/hlp-16doc.gif "Icono de informe")|Informe|Haga clic en el icono de informe o el nombre del mismo para abrir el informe. El informe se abre en una ventana aparte.|  
|![Icono de modelo](media/model-icon.gif "Icono de modelo")|Modelo de informe|Haga clic en el icono de modelo de informe para abrir las páginas de propiedad del modelo.|  
|![Icono de informe vinculado](media/hlp-16linked.gif "Icono de informe vinculado")|Informe vinculado|Haga clic en el icono o en el nombre del informe para abrir el informe vinculado. El informe se abre en una ventana aparte.|  
|![Icono de carpeta](media/hlp-16folder.gif "Icono de carpeta")|Carpeta|Haga clic en el icono de carpeta o en el nombre de la misma para abrir la carpeta.|  
|![Icono de suscripción](media/hlp-16subscription.gif "icono de suscripción")|Suscripción|Haga clic en un icono de suscripción o en una descripción para editar una suscripción.|  
|![Icono de suscripción controlada por datos](media/hlp-16subscriptiondd.gif "icono de suscripción controlada por datos")|Suscripción controlada por datos|Haga clic en un icono de suscripción controlada por datos o en una descripción para editar una suscripción.|  
|![Icono de recurso genérico](media/hlp-16file.gif "Icono de recurso genérico")|Resource|Haga clic en el icono de recurso o en el nombre del mismo para abrir el recurso. El recurso se abre en una ventana aparte.|  
|![Icono de origen de datos compartido](media/hlp-16datasource.png "Icono de origen de datos compartido")|Elemento de origen de datos compartido|Haga clic en un icono de origen de datos compartido para abrir las páginas de propiedades, la lista de informes y una lista de suscripción del origen de datos.|  
|![Icono de la página de propiedades](media/hlp-16prop.gif "icono de la página de propiedades")|Página de propiedades|Haga clic en el icono de propiedades para obtener acceso a páginas adicionales donde establecer valores de propiedades y seguridad.|  
  
## <a name="see-also"></a>Vea también

- [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](install-windows/configure-a-url-ssrs-configuration-manager.md)
- [Planeamiento para Reporting Services y compatibilidad con exploradores de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)
- [Generador de informes &#40;SSRS&#41;](tools/report-builder-authoring-environment-ssrs.md)
- - [Herramientas de Reporting Services](tools/reporting-services-tools.md)
- [Administración de contenido del servidor de informes &#40;Modo nativo de SSRS&#41;](report-server/report-server-content-management-ssrs-native-mode.md)  
[Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)