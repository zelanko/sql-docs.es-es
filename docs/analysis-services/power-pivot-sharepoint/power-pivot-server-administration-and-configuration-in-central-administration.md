---
title: Power Pivot Server Administration y configuración en Administración Central | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e14e6068bc5d6538eab1ec13c3a3cc37ed34fb61
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="power-pivot-server-administration-and-configuration-in-central-administration"></a>Administración y configuración del servidor de Power Pivot en Administración central
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] mediante Administración central de SharePoint.  
  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint, primero debe configurarse. Después de instalar [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint mediante el programa de instalación de SQL Server, puede configurarlo con cualquiera de los enfoques siguientes:  
  
-   [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] o herramienta de configuración de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint 2013  
  
-   Administración central de SharePoint  
  
-   cmdlets de PowerShell  
  
 Los tres métodos proporcionan un servidor totalmente configurado.  
  
 Esta sección incluye las tareas para configurar el software utilizando Administración central. Como mínimo, debe realizar las tres tareas de configuración necesarias indicadas en la siguiente lista.  
  
> [!IMPORTANT]  
>  En el caso de SharePoint 2010, es necesario instalar SharePoint 2010 Service Pack 1 (SP1) antes de configurar [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint o una granja de SharePoint que use un servidor de bases de datos de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] . Si no ha instalado todavía el Service Pack, hágalo ahora antes de empezar la configuración del servidor.  
  
## <a name="benefits-of-configuring-power-pivot-for-sharepoint-using-central-administration"></a>Ventajas de configurar Power Pivot para SharePoint mediante Administración central  
 Administración central de SharePoint es la aplicación administrativa de una granja de SharePoint. Si es administrador de la granja, quizá prefiera utilizar una herramienta familiar al agregar una instancia de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] para SharePoint a la granja.  
  
 A diferencia de las Herramientas de configuración de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] o de los cmdlets de PowerShell, Administración central proporciona páginas que especifican completamente todas las opciones que puede establecer al configurar una aplicación o un servidor. Otros métodos condensan el flujo de trabajo de configuración en un menor número de pasos, o requieren conocimientos previos de cómo configurar un servidor de SharePoint mediante PowerShell.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Configuración de Power Pivot mediante Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)  
  
 [Herramientas de configuración de Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md)  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Vínculo|Tipo|Descripción de la tarea|  
|----------|----------|----------------------|  
|[Implementar las soluciones de Power Pivot en SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)|Obligatorio|Este paso instala los archivos de solución que agregan archivos de programa y páginas de aplicación en la granja y a las colecciones de sitios.|  
|[Creación y configuración de una aplicación de servicio PowerPivot en Administración central](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)|Obligatorio|En este paso se aprovisiona al servicio de sistema de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .|  
|[Activar la integración de características de PowerPivot para colecciones de sitios en Administración central](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md)|Obligatorio|En este paso se activan las características de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] en el nivel de la colección de sitios.|  
|[Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services](../../analysis-services/power-pivot-sharepoint/add-msolap-5-as-a-trusted-data-provider-in-excel-services.md)|Necesario|Este paso agrega el proveedor OLE DB de Analysis Services como proveedor de confianza en Excel Services.|  
|[Actualización de datos Power Pivot con SharePoint 2010](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)|Se recomienda|La actualización de datos es opcional, pero se recomienda. Permite programar actualizaciones desatendidas de los datos de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] en los libros de Excel publicados.|  
|[Configurar la cuenta de actualización de datos desatendida de PowerPivot (PowerPivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493)|Se recomienda|Este paso proporciona una cuenta especial que se puede utilizar para ejecutar trabajos de actualización de datos del servidor.|  
|[Configurar la recolección de datos de uso para &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)|Opcional|La recopilación de datos de uso está configurada de forma predeterminada. Puede utilizar estos pasos para modificar la configuración predeterminada.|  
|[Configuración de una actualización de datos dedicada o del procesamiento de solo consultas (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/5e027605-1086-4941-bb01-f315df8f829b)|Opcional|Una instancia de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] se puede destinar solo a los trabajos de actualización de datos o a las consultas. Además, puede modificar la configuración predeterminada de los trabajos paralelos de actualización de datos.|  
|[Configuración de las cuentas de servicio Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)|Opcional|Explica cómo actualizar las contraseñas o cambiar las cuentas de servicio.|  
|[Conectar una aplicación de servicio PowerPivot a una aplicación web de SharePoint en Administración central](../../analysis-services/power-pivot-sharepoint/connect-power-pivot-service-app-to-sharepoint-web-app-in-ca.md)|Opcional|Explica cómo modificar las asociaciones de servicio.|  
|[Crear una ubicación de confianza para los sitios PowerPivot en Administración central](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md)|Opcional|Explica cómo agregar la Galería de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] como una ubicación de confianza.|  
|[Configurar y ver archivos de registro de SharePoint y el registro de diagnósticos &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md)|Opcional|El registro de eventos está configurado de forma predeterminada. Puede utilizar estos pasos para modificar la configuración predeterminada.|  
|[Configuración de las reglas de mantenimiento de PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md)|Opcional|Las reglas de estado de servidor están configuradas de forma predeterminada. Puede utilizar estos pasos para modificar algunas de las configuraciones predeterminadas.|  
|[Creación y personalización de la Galería de PowerPivot](../../analysis-services/power-pivot-sharepoint/create-and-customize-power-pivot-gallery.md)|Opcional|Para las instalaciones que configure manualmente, este procedimiento explica cómo crear una biblioteca de la Galería de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que muestre imágenes en miniatura de los libros de [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] que contiene.|  
|[Agregar un tipo de contenido de conexión de modelo semántico de BI a una biblioteca &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md)|Opcional|Explica cómo ampliar una biblioteca de documentos para admitir la creación de archivos de conexión de modelo semántico de BI.|  
  
## <a name="see-also"></a>Vea también  
 [Instalación de Power Pivot para SharePoint 2010](http://msdn.microsoft.com/en-us/8d47dde7-c941-4280-a934-e2fe3f9a938f)   
 [Referencia de las opciones de configuración &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Recuperación ante desastres de PowerPivot para SharePoint](http://go.microsoft.com/fwlink/p/?LinkId=389570)  
  
  
