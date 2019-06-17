---
title: Administración de servidor de PowerPivot y la configuración en Administración Central | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2cdbfdc5-45a9-4000-a03d-318cc7ac8fe9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de72001ced1b7e2690f90b2de4c59bb35aca6ce4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071113"
---
# <a name="powerpivot-server-administration-and-configuration-in-central-administration"></a>Administración y configuración del servidor PowerPivot en Administración central
  Los administradores de aplicaciones de servicios de SharePoint llevan a cabo la administración y configuración de servidores PowerPivot mediante Administración central de SharePoint.  
  
 Para poder utilizar PowerPivot para SharePoint, debe configurarse. Después de instalar PowerPivot para SharePoint mediante el programa de instalación de SQL Server, puede configurarlo con cualquiera de los enfoques siguientes:  
  
-   Herramienta de configuración de PowerPivot o herramienta de configuración de PowerPivot para SharePoint 2013  
  
-   Administración central de SharePoint  
  
-   cmdlets de PowerShell  
  
 Los tres métodos proporcionan un servidor totalmente configurado.  
  
 Esta sección incluye las tareas para configurar el software utilizando Administración central. Como mínimo, debe realizar las tres tareas de configuración necesarias indicadas en la siguiente lista.  
  
> [!IMPORTANT]  
>  En el caso de SharePoint 2010, debe instalarse SharePoint 2010 Service Pack 1 (SP1) antes de configurar PowerPivot para SharePoint o una granja de SharePoint que use un servidor de bases de datos de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Si no ha instalado todavía el Service Pack, hágalo ahora antes de empezar la configuración del servidor.  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-central-administration"></a>Ventajas de configurar PowerPivot para SharePoint utilizando Administración central  
 Administración central de SharePoint es la aplicación administrativa de una granja de SharePoint. Si es administrador de la granja, quizá prefiera utilizar una herramienta familiar al agregar una instancia de PowerPivot para SharePoint a la granja.  
  
 A diferencia de las Herramientas de configuración de PowerPivot o de los cmdlets de PowerShell, Administración central proporciona las páginas que especifican completamente todas las opciones que puede establecer al configurar una aplicación o un servidor. Otros métodos condensan el flujo de trabajo de configuración en un menor número de pasos, o requieren conocimientos previos de cómo configurar un servidor de SharePoint mediante PowerShell.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Configuración de PowerPivot mediante Windows PowerShell](power-pivot-configuration-using-windows-powershell.md)  
  
 [Herramientas de configuración de PowerPivot](power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Vínculo|Tipo|Descripción de la tarea|  
|----------|----------|----------------------|  
|[Implementar soluciones de PowerPivot para SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)|Obligatorio|Este paso instala los archivos de solución que agregan archivos de programa y páginas de aplicación en la granja y a las colecciones de sitios.|  
|[Crear y configurar una aplicación de servicio PowerPivot en Administración Central](create-and-configure-power-pivot-service-application-in-ca.md)|Obligatorio|Este paso proporciona el Servicio de sistema de PowerPivot.|  
|[Activar la integración de características de PowerPivot para colecciones de sitios en Administración Central](activate-power-pivot-integration-for-site-collections-in-ca.md)|Obligatorio|Este paso activa las características de PowerPivot en el nivel de colección de sitios.|  
|[Adición de MSOLAP.5 como proveedor de datos de confianza en Excel Services](add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|Obligatorio|Este paso agrega el proveedor OLE DB de Analysis Services como proveedor de confianza en Excel Services.|  
|[Actualización de datos PowerPivot con SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)|Se recomienda|La actualización de datos es opcional, pero se recomienda. Permite programar actualizaciones desatendidas de los datos de PowerPivot en los libros de Excel publicados.|  
|[Configurar PowerPivot cuenta de actualización de datos desatendida &#40;PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)|Se recomienda|Este paso proporciona una cuenta especial que se puede utilizar para ejecutar trabajos de actualización de datos del servidor.|  
|[Configurar la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|Opcional|La recopilación de datos de uso está configurada de forma predeterminada. Puede utilizar estos pasos para modificar la configuración predeterminada.|  
|[Configurar la actualización de datos dedicada o procesamiento de una sola consulta &#40;PowerPivot para SharePoint&#41;](../configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)|Opcional|Una instancia de PowerPivot se puede destinar solo a los trabajos o a las consultas de actualización de datos. Además, puede modificar la configuración predeterminada de los trabajos paralelos de actualización de datos.|  
|[Configurar las cuentas de servicio PowerPivot](configure-power-pivot-service-accounts.md)|Opcional|Explica cómo actualizar las contraseñas o cambiar las cuentas de servicio.|  
|[Conectar una aplicación de servicio PowerPivot a una aplicación Web de SharePoint en Administración Central](connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|Opcional|Explica cómo modificar las asociaciones de servicio.|  
|[Crear una ubicación de confianza para sitios PowerPivot en Administración Central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|Opcional|Describe cómo agregar la galería de PowerPivot como una ubicación de confianza.|  
|[Configurar y ver los archivos de registro de SharePoint y el registro de diagnóstico &#40;PowerPivot para SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md)|Opcional|El registro de eventos está configurado de forma predeterminada. Puede utilizar estos pasos para modificar la configuración predeterminada.|  
|[Configurar reglas de mantenimiento de PowerPivot:](configure-power-pivot-health-rules.md)|Opcional|Las reglas de estado de servidor están configuradas de forma predeterminada. Puede utilizar estos pasos para modificar algunas de las configuraciones predeterminadas.|  
|[Crear y personalizar la Galería de PowerPivot](create-and-customize-power-pivot-gallery.md)|Opcional|Para las instalaciones que configure manualmente, este procedimiento explica cómo crear una biblioteca de la Galería de PowerPivot que muestre imágenes en miniatura de los libros PowerPivot que contiene.|  
|[Agregar un tipo de contenido de la conexión de modelo semántico de BI a una biblioteca &#40;PowerPivot para SharePoint&#41;](add-bi-semantic-model-connection-content-type-to-library.md)|Opcional|Explica cómo ampliar una biblioteca de documentos para admitir la creación de archivos de conexión de modelo semántico de BI.|  
  
## <a name="see-also"></a>Vea también  
 [PowerPivot para SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Referencia de las opciones configuración &#40;PowerPivot para SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Recuperación ante desastres de PowerPivot para SharePoint](https://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
