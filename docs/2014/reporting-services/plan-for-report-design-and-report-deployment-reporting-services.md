---
title: Plan para implementación de informes (Reporting Services 2014) y el diseño de informe | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1c1e265e-52a2-4de3-96fd-ca4abae01c02
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: db11e53b9fb6efb50a7bb676798626f5886ff9e5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53362753"
---
# <a name="plan-for-report-design-and-report-deployment-reporting-services-2014"></a>Planear el diseño y la implementación de informes (Reporting Services 2014)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona varios enfoques para la creación e implementación de informes. Use este tema como ayuda para planear un entorno de creación de informes y un servidor de informes que operen juntos. En este tema se proporciona información general sobre la compatibilidad de definición de informe por componentes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Una definición de informe es un archivo XML que se escribe en lenguaje RDL (Report Definition Language) o RDLC (Report Definition Language for Clients). Cada definición de informe cumple una versión de esquema específica que aparece al comienzo del archivo.  
  
 Los archivos RDL se crean en el Diseñador de informes en los proyectos de [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] y en el Generador de informes 3.0. Los archivos RDLC se crean mediante los controles ReportViewer que se incluyen en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
 En este tema:  
  
-   [Versiones de esquema RDL](#bkmk_rdl_schema_versions)  
  
-   [Servidor de informes y compatibilidad con el esquema RDL](#bkmk_report_server_rdl_schema_support)  
  
-   [Compatibilidad con la implementación y creación de informes](#bkmk_report_authoring_and_deployment)  
  
-   [Controles ReportViewer](#bkmk_reportviewer)  
  
##  <a name="bkmk_rdl_schema_versions"></a> Versiones de esquema RDL  
 En la tabla siguiente se enumera cada versión de esquema disponible y la abreviatura que se usa de aquí en adelante:  
  
|Abreviatura|Versión de esquema|  
|------------------|--------------------|  
|RDL 2010|https://schemas.microsoft.com/sqlserver/reporting/2010/01/reportdefinition|  
|RDL 2008|https://schemas.microsoft.com/sqlserver/reporting/2008/01/reportdefinition|  
|RDL 2005<br /><br /> RDLC 2005|https://schemas.microsoft.com/sqlserver/reporting/2005/01/reportdefinition|  
|RDL 2000|https://schemas.microsoft.com/sqlserver/reporting/2003/10/reportdefinition|  
  
 Para obtener más información acerca de RDL y los esquemas RDL, vea lo siguiente:  
  
-   [Esquemas XML de Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=31850)  
  
-   [Especificación RDL de SQL Server](https://go.microsoft.com/fwlink/?linkid=116865)  
  
-   [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
 Para más información sobre los controles ReportViewer, vea [Controles ReportViewer (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx).  
  
##  <a name="bkmk_report_server_rdl_schema_support"></a> Compatibilidad del servidor de informes y el esquema RDL  
 Un archivo de definición de informe se puede implementar en un servidor de informes de [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] de las maneras siguientes:  
  
-   **Diseñador de informes:** Implemente un informe desde el Diseñador de informes de [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)].  
  
-   **Generador de informes:** Guarde un informe en el servidor de informes desde el Generador de informes.  
  
-   **Administrador de informes:** Cargue un informe en un servidor de informes en modo nativo desde el Administrador de informes.  
  
-   **SharePoint:** Cargue un informe en un sitio de SharePoint que esté configurado con un servidor de informes en modo de SharePoint.  
  
-   **Mediante programación:** Publique un informe mediante programación usando las interfaces de API SOAP en un servidor de informes. Para obtener más información, vea [Report Server Web Service](report-server-web-service/report-server-web-service.md).  
  
 En la tabla siguiente se indica la versión de esquema rdl admitida según la versión del servidor de informes.  
  
|Versión del servidor de informes|Versión de esquema RDL|  
|---------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> o bien<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> o bien<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|RDL 2010<br /><br /> RDL 2008<br /><br /> RDL 2005<br /><br /> RDL 2000|  
|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|RDL 2008<br /><br /> RDL 2005<br /><br /> RDL 2000|  
|[!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]|RDL 2005<br /><br /> RDL 2000|  
  
 Cuando se carga una definición de informe en el servidor de informes o se actualiza un servidor de informes que contiene informes, el servidor de informes conserva la definición de informe en el formato original. **Cuando se usa por primera vez**, el servidor de informes actualiza el informe en la base de datos del servidor de informes a un formato binario que se conserva para vistas posteriores. La definición de informe (.rdl) propiamente dicha no se actualiza.  
  
 Puede extraer del servidor de informes una copia de solo lectura del archivo de definición de informe (.rdl). En un servidor de informes en modo nativo, vaya al administrador de informes, seleccione el informe y haga clic en **Descargar**. En una implementación en modo de SharePoint, vaya a la biblioteca de documentos, seleccione el informe y haga clic en **Descargar una copia**.  
  
 Para actualizar la definición de informe, se debe abrir el informe en un entorno de creación de informes y guardarlo posteriormente.  
  
 Para más información sobre actualizaciones de informes y las versiones de esquema que se admiten, vea [Actualizar informes](install-windows/upgrade-reports.md).  
  
##  <a name="bkmk_report_authoring_and_deployment"></a> Compatibilidad de creación e implementación de informes  
 Los entornos de creación de informes son el Diseñador de informes en los proyectos de [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] y el Generador de informes. Los entornos de creación de informes proporcionan una gran variedad de características de compatibilidad para la actualización de informes, el diseño de informes, la presentación de vistas previas de informes en modo local, la presentación de vistas previas de informes en el servidor de informes y la implementación de informes.  
  
 En la tabla siguiente se muestra un resumen de características de compatibilidad para la creación e implementación de definiciones de informe para diferentes versiones de esquema:  
  
|Entorno de creación|Versión RDL creada|Versión RDL de implementación|Versiones de implementación en el servidor de informes|  
|---------------------------|--------------------------|------------------------|--------------------------------------|  
|Diseñador de informes de SQL Server 2014 Data Tools - Business Intelligence para Microsoft Visual Studio 2012, en el Centro de descarga de Microsoft.<br /><br /> O bien<br /><br /> Diseñador de informes de SQL Server 2012 Data Tools - Business Intelligence para Microsoft Visual Studio 2012, en el Centro de descarga de Microsoft.<br /><br /> o bien<br /><br /> Diseñador de informes de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Data Tools, incluido en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].|Crea RDL 2010. Al abrir RDL existente:<br /><br /> RDL 2000, actualizaciones a RDL 2010<br /><br /> RDL 2005, actualizaciones a RDL 2010<br /><br /> RDL 2008, actualizaciones a RDL 2010|RDL 2008<br /><br /> RDL 2010|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Diseñador de informes de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Business Intelligence Development Studio|Crea RDL 2010. Al abrir RDL existente:<br /><br /> RDL 2000, actualizaciones a RDL 2010<br /><br /> RDL 2005, actualizaciones a RDL 2010<br /><br /> RDL 2008, actualizaciones a RDL 2010|RDL 2008<br /><br /> RDL 2010|[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]|  
|Diseñador de informes de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Business Intelligence Development Studio|Crea RDL 2008. Al abrir RDL existente:<br /><br /> RDL 2000, actualizaciones a RDL 2008<br /><br /> RDL 2005, actualizaciones a RDL 2008|RDL 2008|[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]|  
|Generador de informes de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]|Crea RDL 2010. Al abrir RDL existente:<br /><br /> RDL 2000, actualizaciones a RDL 2010<br /><br /> RDL 2005, actualizaciones a RDL 2010<br /><br /> RDL 2008, actualizaciones a RDL 2010|RDL 2010|[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|  
|Diseñador de informes RDLC de Visual Studio|RDLC 2005|N/D|N/D|  
  
 Para obtener más información sobre [!INCLUDE[ss_dtbi_vs2013](../includes/ss-dtbi-vs2013-md.md)], vea lo siguiente  
  
-   [Implementación y compatibilidad de versiones en las herramientas de datos de SQL Server &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md)  
  
-   [Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843).  
  
##  <a name="bkmk_reportviewer"></a> Controles ReportViewer  
 Un control ReportViewer de [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] puede mostrar un informe .rdlc en el modo de vista previa local o, en modo remoto, el control puede mostrar un archivo .rdl hospedado en un servidor de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . En la tabla siguiente se muestra la lista de versiones RDL que admiten los controles ReportViewer para el procesamiento local (.rdlc). La compatibilidad con el lenguaje RDL de servidor se resume en la sección [Compatibilidad del servidor de informes y el esquema RDL](#bkmk_report_server_rdl_schema_support).  
  
|Control ReportViewer del producto|Versión de RDL para la vista previa local|  
|-------------------------------------|--------------------------------------|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2013<br /><br /> o bien<br /><br /> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2012<br /><br /> o bien<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]|RDL 2008|  
|[!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)]<br /><br /> o bien<br /><br /> [!INCLUDE[vsOrcas](../includes/vsorcas-md.md)]|RDL 2005|  
  
 Para obtener más información, vea:  
  
-   [Convertir archivos RDLC en archivos RDL](https://msdn.microsoft.com/library/ms252109.aspx)  
  
-   [Controles ReportViewer (Visual Studio)](https://msdn.microsoft.com/library/ms251671.aspx)  
  
-   [Agregar y configurar los controles ReportViewer](https://msdn.microsoft.com/library/ms252104.aspx)  
  
## <a name="see-also"></a>Vea también  
 [Informes, elementos de informe y definiciones de informe &#40;Generador de informes y SSRS&#41;](report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Herramientas de Reporting Services](tools/reporting-services-tools.md)   
 [Report Definition Language &#40;SSRS&#41;](reports/report-definition-language-ssrs.md)  
  
  
