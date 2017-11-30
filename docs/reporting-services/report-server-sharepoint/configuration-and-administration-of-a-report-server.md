---
title: "Configuración y administración de un servidor de informes de SQL Server Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fe898a9401340f80884fa15f3ea1ce45108fbbc6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="configuration-and-administration-of-a-sql-server-reporting-services-report-server"></a>Configuración y administración de un servidor de informes de SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server Reporting Services es una plataforma de generación de informes basada en servidor que proporciona una gama completa de herramientas y servicios listos para usar que le ayudarán a crear, implementar y administrar informes para la organización, además de características de programación que le permitirán ampliar y personalizar la funcionalidad de los informes. Puede integrar su entorno de informes con un producto o tecnología de SharePoint para experimentar las ventajas de usar el entorno colaborativo proporcionado por los sitios de SharePoint.

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

Use las siguientes secciones como ayuda para entender los conceptos, los escenarios de implementación, los procedimientos y otras cuestiones para integrar el entorno de Reporting Services con un producto o tecnología de SharePoint:  
  
-   Opciones de menú en una biblioteca de documentos de SharePoint  
  
    -   [Administrador de alertas de datos para los usuarios de SharePoint](../../reporting-services/data-alert-manager-for-sharepoint-users.md)  
  
    -   [Crear y administrar suscripciones para servidores de informes en modo de SharePoint](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
    -   [Actualizar credenciales en orígenes de datos de informe desde un sitio de SharePoint](../../reporting-services/report-data/update-credentials-in-report-data-sources-from-a-sharepoint-site.md)  
  
    -   [Administrar conjuntos de datos compartidos](../../reporting-services/report-data/manage-shared-datasets.md)  
  
    -   [Establecer parámetros en un informe publicado &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md)  
  
    -   [Establecer opciones de procesamiento &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
    -   [Opciones de actualización de memoria caché &#40;Administrador de informes&#41;](http://msdn.microsoft.com/library/227da40c-6bd2-48ec-aa9c-50ce6c1ca3a6)  
  
-   [Características de la colección de sitios Reporting Services](../../reporting-services/report-server-sharepoint/site-collection-features-reporting-services.md)  
  
-   [Activar las características de integración del servidor de informes y Power View en SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)  
  
-   [Valores de configuración del sitio de Reporting Services y características del sitio &#40;modo de SharePoint&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)  
  
-   [Activar la característica de sincronización de archivos del servidor de informes en Administración central de SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  
  
-   [Agregue los tipos de contenido de Reporting Services a la biblioteca de SharePoint.](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md)  
  
-   [Informes en modo local frente al modo conectado en el Visor de informes &#40;Reporting Services en modo de SharePoint&#41;](../../reporting-services/report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)  
  
-   [Cargar documentos en una biblioteca de SharePoint &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
-   [Establecer opciones de procesamiento &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
 Para más información general sobre Reporting Services, vea [Reporting Services](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md) en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información sobre otros componentes, herramientas y recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea los [Libros en pantalla de SQL Server](../../sql-server/sql-server-technical-documentation.md).  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
