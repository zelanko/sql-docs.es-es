---
title: Portal web (modo nativo de SSRS) | Microsoft Docs
ms.custom: 
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
ms.assetid: 7349e626-6ed5-4d21-b05f-cf042ad9ad70
caps.latest.revision: "15"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Active
ms.openlocfilehash: e11550048a916088124c63a21a55d57056fba855
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="web-portal-ssrs-native-mode"></a>Portal web (modo nativo de SSRS)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

El portal web de Reporting Services es una experiencia basada en la Web que permite ver informes, informes móviles y KPI, así como navegar por los elementos que se encuentran en la instancia del servidor de informes. También puede usar el portal web para administrar una única instancia del servidor de informes.

![ssRSPortal](../reporting-services/media/ssrsportal.png)

## <a name="what-is-the-web-portal"></a>¿Qué es el portal web?

Puede usar el portal web para realizar las siguientes tareas:

- Ver, buscar e imprimir informes, así como suscribirse a ellos.

- Crear, proteger y mantener la jerarquía de carpetas para organizar elementos en el servidor.

- Configurar una seguridad basada en roles que determine el acceso a elementos y operaciones.

- Configurar las propiedades de ejecución, el historial y los parámetros del informe.

- Crear programaciones compartidas y orígenes de datos compartidos para que las programaciones y las conexiones de orígenes de datos sean más fáciles de administrar.

- Crear suscripciones controladas por datos que distribuyan informes a una lista de destinatarios extensa.

- Crear informes vinculados para reutilizarlos y cambiar la finalidad de un informe existente de varias formas.

- Descargar herramientas comunes como Generador de informes y Publicador de informes móviles.

- [Crear KPI](../reporting-services/working-with-kpis-in-reporting-services.md).

- Enviar comentarios o solicitar nuevas características.

Puede usar el portal web para examinar las carpetas del servidor de informes o buscar informes concretos. Puede ver un informe, sus propiedades generales y copias anteriores de este que se almacenan en el historial de informes. Dependiendo de los permisos que tenga, también podría suscribirse a informes para su entrega en una bandeja de entrada de correo electrónico o en una carpeta compartida del sistema de archivos.

> [!NOTE]
> Para obtener información sobre los exploradores y versiones compatibles, vea [Compatibilidad del explorador de Reporting Services y Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md).

El portal web solo se usa para un servidor de informes que se ejecuta en modo nativo. No se admite para un servidor de informes que se configure para el modo integrado de SharePoint.

Algunas características del portal web solo están disponibles en determinadas ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion.md)]. Para obtener más información, vea [Características de Reporting Services compatibles con las ediciones de SQL Server 2016](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

En una instalación nueva, solo los administradores locales tienen permisos suficientes para trabajar con el contenido y la configuración. Para conceder permisos a otros usuarios, un administrador local debe crear asignaciones de roles que proporcionen acceso al servidor de informes. Las tareas y las páginas de aplicación a las que un usuario puede obtener acceso posteriormente dependerán de las asignaciones de roles para dicho usuario. Para obtener más información, consulte [Conceder acceso de usuario a un servidor de informes](security/grant-user-access-to-a-report-server-report-manager.md).

> [!NOTE]
> Si va a examinar el portal web en la máquina local donde se ejecuta el servidor, aparecerá un mensaje que le indica que no tiene permiso para ver esta carpeta. Esto se debe al control de acceso universal (UAC) y a que no está ejecutando el explorador como administrador. No puede ejecutar Edge como administrador. Tendrá que utilizar Internet Explorer. Puede acceder al servidor de forma remota o iniciar Internet Explorer como administrador e ir al portal web. Si desea usar el portal web de forma remota, debe conceder a su cuenta de derechos de administrador de contenido para la carpeta.  

## <a name="start-and-use-the-web-portal"></a>Inicio y uso del portal web

El portal web es una aplicación web que abre al escribir la URL del [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] en la barra de direcciones de la ventana del explorador. Al iniciar el [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)], las páginas, los vínculos y las opciones que se ven varían en función de los permisos que se tengan en el servidor de informes. Para realizar una tarea, debe estar asignado a un rol que incluya la tarea.  Un usuario asignado a un rol con permisos totales tiene acceso al conjunto completo de menús y páginas de la aplicación disponibles para administrar un servidor de informes. Un usuario asignado a un rol con permisos para ver y ejecutar informes solo ve los menús y las páginas que admiten dichas actividades. Cada usuario puede tener distintas asignaciones de roles para distintos servidores de informes o, incluso, para los distintos informes y carpetas almacenados en un único servidor de informes.

Para obtener más información sobre los roles, consulte [Conceder permisos en un servidor de informes en modo nativo](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).

### <a name="start-the-web-portal"></a>Inicio del portal web

Para iniciar el portal web desde un explorador, siga estos pasos:

1. Abra el explorador web. Para ver una lista de los exploradores web compatibles, consulte [Planear la compatibilidad del explorador de Reporting Services y Power View (Reporting Services 2014)](../reporting-services/browser-support-for-reporting-services-and-power-view.md).

2. En la barra de direcciones del explorador web, escriba la URL del portal web.

    De manera predeterminada, la URL es *http://[nombreDeEquipo]/reports*.

    El servidor de informes se puede configurar para usar un puerto concreto. Por ejemplo, *http://[nombreDeEquipo]:80/reports* o *http://[nombreDeEquipo]:8080/reports*.

## <a name="grouping-by-categories"></a>Agrupación por categorías

El portal web agrupará los elementos en distintas categorías. Las categorías disponibles son las siguientes:

- KPI
- Mobile Reports (Informes móviles)
- Paginated Reports (Informes paginados)
- Power BI Desktop Reports (Informes de Power BI Desktop)
- Excel Workbooks (Libros de Excel)
- Conjuntos de datos
- Orígenes de datos
- Recursos

Puede controlar lo que se muestra si selecciona **Vista** en la esquina superior derecha. Si selecciona Mostrar oculto, esos elementos se mostrarán en un color más claro.

![ssRSWebPortal-view](../reporting-services/media/ssrswebportal-view.png)

![ssRSWebPortal-hidden](../reporting-services/media/ssrswebportal-hidden.png)

### <a name="power-bi-desktop-reports-and-excel-workbooks"></a>Informes de Power BI Desktop y libros de Excel

Puede cargar, organizar y administrar los permisos para los informes de Power BI Desktop y libros de Excel. Se agruparán juntos en el portal web.

![ssRSWebPortal-view-pbi-and-excel](../reporting-services/media/ssrswebportal-view-pbi-and-excel.png)

Los archivos se almacenan en Reporting Services, como sucede con otros archivos de recursos. Si selecciona uno de estos elementos, se descargará localmente en su escritorio. Puede guardar los cambios que ha efectuado volviendo a cargarlos al servidor de informes.

## <a name="search-for-items"></a>Búsqueda de elementos

Puede escribir un término de búsqueda y podrá ver todos los elementos a los que tenga acceso. Los resultados se categorizan en KPI, informes, conjuntos de datos y otros elementos. Después, puede interactuar con los resultados y agregarlos a sus favoritos.

![ssRSWebPortal-Search](../reporting-services/media/ssrswebportal-search.png)

## <a name="web-portal-tasks"></a>Tareas del portal web

[Personalización de marca del portal web](../reporting-services/branding-the-web-portal.md)

[Trabajar con KPI](../reporting-services/working-with-kpis-in-reporting-services.md)

[Uso de los conjuntos de datos compartidos (portal web)](../reporting-services/work-with-shared-datasets-web-portal.md)

## <a name="see-also"></a>Vea también

[Creación y publicación de informes móviles con el Publicador de informes móviles de SQL Server](../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
[Configurar una dirección URL (Administrador de configuración de SSRS)](../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
[Herramientas de Reporting Services](../reporting-services/tools/reporting-services-tools.md)  
[Compatibilidad del explorador de Reporting Services y Power View](../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Características de Reporting Services compatibles con las ediciones de SQL Server 2016](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
