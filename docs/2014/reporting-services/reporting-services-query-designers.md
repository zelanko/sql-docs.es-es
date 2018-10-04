---
title: Diseñadores de consultas de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- query designers [Reporting Services]
ms.assetid: 07efd3f1-804f-45f7-b62a-3e727a3d9835
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e8a2fabc77b4b2ca5d8a27b83c29c233148032e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219502"
---
# <a name="reporting-services-query-designers"></a>Diseñadores de consultas de Reporting Services
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona diseñadores de consultas gráfico y basado en texto para ayudarle a crear consultas para cada tipo de origen de datos en el informe.  
  
 Algunos orígenes de datos admiten diseñadores gráficos que permiten generar las consultas de forma interactiva. Otros orígenes de datos usan un diseñador de consultas basado en texto. Con un diseñador gráfico de consultas, puede arrastrar los elementos de metadatos que representan los datos subyacentes de un origen de datos a la superficie de diseño de la consulta. Con un diseñador de consultas basado en texto, puede escribir el texto de los comandos en un panel de consulta. Para cambiar de un diseñador gráfico de consultas a un diseñador de consultas basado en texto, haga clic en el icono del diseñador de consultas basado en texto en la barra de herramientas.  
  
 Las extensiones de datos de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instaladas en el cliente o en el servidor de informes determinan los tipos de origen de datos disponibles en el informe. Para obtener más información, consulte [RSReportDesigner Configuration File](report-server/rsreportdesigner-configuration-file.md) y [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md).  
  
 Una extensión de procesamiento de datos y el diseñador de consultas asociado pueden diferir en el soporte de orígenes de datos de las maneras siguientes:  
  
-   **El tipo de diseñador de consultas.** Por ejemplo, un origen de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite ambos tipos de diseñadores de consultas.  
  
-   **La variación del lenguaje de consulta.** Por ejemplo, la sintaxis de un lenguaje de consulta como [!INCLUDE[tsql](../includes/tsql-md.md)] puede variar según el tipo de origen de datos. La sintaxis de los comandos de consulta del lenguaje [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] difiere ligeramente de la del lenguaje SQL de Oracle.  
  
-   **La compatibilidad con la parte de esquema de un nombre de objeto de base de datos.** Si un origen de datos usa esquemas como parte del identificador del objeto de base de datos, el nombre del esquema se debe proporcionar como parte de la consulta para todos los nombres que no usen el esquema predeterminado. Por ejemplo, `SELECT FirstName, LastName FROM [Person].[Person]`.  
  
-   **La compatibilidad con los parámetros de consulta.** Los proveedores de datos varían en lo que respecta a la compatibilidad para los parámetros. Algunos proveedores de datos admiten parámetros con nombre (por ejemplo, `SELECT Col1, Col2 FROM Table WHERE <parameter identifier><parameter name> = <value>`). Algunos proveedores de datos admiten parámetros sin nombre (por ejemplo, `SELECT Col1, Col2 FROM Table WHERE <column name> = ?`). El identificador de parámetros puede variar según el proveedor de datos; Por ejemplo, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utiliza la "arroba" (@) símbolos, Oracle usa los dos puntos (:). Algunos proveedores de datos no admiten parámetros.  
  
-   **La capacidad de importar consultas.** Por ejemplo, para un origen de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , puede importar una consulta desde un archivo de definición de informe (.rdl) o un archivo .sql.  
  
## <a name="query-designers"></a>Diseñadores de consultas  
 En los temas siguientes se describe la interfaz de usuario para cada diseñador de consultas.  
  
-   [Interfaz de usuario del diseñador de consultas MDX de Analysis Services](report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
-   [Interfaz de usuario del diseñador de consultas DMX de Analysis Services](report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
-   [Interfaz de usuario del diseñador gráfico de consultas](report-data/graphical-query-designer-user-interface.md)  
  
-   [Interfaz de usuario del diseñador de consultas relacionales](../../2014/reporting-services/relational-query-designer-user-interface.md)  
  
-   [Interfaz de usuario del diseñador de consultas de Hyperion Essbase](report-data/hyperion-essbase-query-designer-user-interface.md)  
  
-   [Interfaz de usuario del diseñador de consultas de modelo de informe](report-data/report-model-query-designer-user-interface.md)  
  
-   [Interfaz de usuario del diseñador de consultas SAP NetWeaver BI](report-data/sap-netweaver-bi-query-designer-user-interface.md)  
  
-   [Diseñador de consultas de lista de SharePoint](../../2014/reporting-services/sharepoint-list-query-designer.md)  
  
-   [Interfaz de usuario del diseñador de consultas basado en texto](../../2014/reporting-services/text-based-query-designer-user-interface.md)  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md)   
 [Las extensiones de procesamiento de datos y proveedores de datos de .NET Framework &#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)   
 [Extensiones &#40;SSRS&#41;](extensions-ssrs.md)  
  
  
