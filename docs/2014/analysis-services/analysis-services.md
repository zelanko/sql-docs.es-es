---
title: SQL Server 2014 Analysis Services (SQL Server 2014 Analysis Services) Microsoft Docs
ms.custom: ''
ms.date: 04/06/2020
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 986356e6ebf7697bf0b425553f6803659a0fc5cb
ms.sourcegitcommit: 8f99d15c5b23d9f3c08a77e2b8bea5772f570493
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/07/2020
ms.locfileid: "80760303"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 Analysis Services es un motor de datos analíticos que se utiliza en soluciones de soporte de decisiones e inteligencia empresarial (BI), que proporciona los datos analíticos para informes empresariales y aplicaciones cliente como Excel, informes de Reporting ServicesReporting Services y otras herramientas de BI de terceros. 

## <a name="about-sql-server-analysis-services-documentation"></a>Acerca de la documentación de SQL Server Analysis Services

La documentación está separada por versión. Actualmente se encuentra en la documentación de SQL Server 2014 Analysis Services.

- Para obtener más información acerca de SQL Server 2012 y [versiones anteriores,](https://docs.microsoft.com/previous-versions/sql/)consulte documentación de versiones anteriores de SQL Server .
- Para obtener más información acerca de SQL Server 2014, consulte [Libros en pantalla para SQL Server 2014](../2014-toc/index.yml)
- Para obtener más información acerca de SQL Server 2016 y versiones posteriores, vea documentación de [Analysis ServicesAnalysis Services](https://docs.microsoft.com/analysis-services/).
- Para obtener más información sobre Azure Analysis Services, consulte [Documentación de Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/).

## <a name="analysis-services-workflow"></a>Flujo de trabajo de Analysis ServicesAnalysis Services

Un flujo de trabajo típico incluye la creación de un modelo de datos OLAP o tabular, la implementación del modelo como base de datos en una instancia de servidor, el proceso de la base de datos para cargarla con datos y, a continuación, asignar permisos para permitir el acceso a los datos. Cuando esté listo, se puede obtener acceso a este modelo de datos con varios fines desde cualquier aplicación cliente que admita [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como origen de datos.  
  
 Para crear un modelo, use SQL Server Data Tools (consulte [Herramientas y aplicaciones utilizadas en Analysis ServicesAnalysis Services](tools-and-applications-used-in-analysis-services.md)), eligiendo una plantilla de proyecto Tabular o Multidimensional y Minería de datos. La plantilla de proyecto contiene las carpetas de todos los objetos necesarios en un modelo. Puede utilizar asistentes para crear todos los elementos básicos, como orígenes de datos, vistas de origen de datos, dimensiones, cubos y roles.  
  
 Los modelos se rellenan con datos procedentes de sistemas de datos externos, normalmente almacenamientos de datos hospedados en un motor de base de datos relacional de SQL Server o de Oracle (los modelos tabulares admiten tipos de orígenes de datos adicionales). Los modelos especifican objetos de consulta, como los cubos, pero también especifican las dimensiones que se pueden usar en varios cubos, cálculos y KPI que encapsulan la lógica del negocio, así como interacciones, como los comportamientos en navegación y obtención de detalles.  
  
 Para usar un modelo, se implementa en una instancia de servidor que ejecuta bases de datos en un modo de servidor determinado, lo que pone los datos a disposición de los usuarios autorizados que se conectan a través de Excel u otras aplicaciones.  
  
 Puede instalar una instancia en uno de los tres modos de servidor:  
  
-   Como instancia tabular, ejecutando modelos tabulares.  
  
-   Como una instancia multidimensional y de minería de datos, ejecutando cubos OLAP y modelos de minería de datos (es el valor predeterminado).  
  
-   Como PowerPivot para SharePoint, ejecutando modelos de datos PowerPivot y de Excel en SharePoint (PowerPivot para SharePoint es un motor de datos de nivel intermedio que carga, consulta y actualiza modelos de datos hospedados en SharePoint).  
  
 El mismo motor de datos; tres formas de usarlo. Tenga en cuenta que los modos de servidor se establecen durante la instalación y no se pueden cambiar posteriormente. Debe instalar una nueva instancia si necesita otro modo diferente.  
  
 La documentación fundacional de Analysis Services se organiza en las secciones que corresponden al tipo de proyecto que se está generando. Elija uno de los siguientes vínculos para obtener más información acerca de cada área de características o modo.  
  
 **Explorar contenido por área**  
 ![Icono](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") de carpeta de archivos [pequeños comparando soluciones tabulares y multidimensionales &#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 Administración de ![instancias](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") de Small File Folder [Analysis Services Analysis Services](instances/analysis-services-instance-management.md)  
  
 ![Small File Folder Icon](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") [Tabular Modeling &#40;SSAS Tabular&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![Icono](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") de carpeta de archivos [pequeños Modelado multidimensional &#40;sSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Ique de](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") datos de carpetas de archivos pequeños [&#40;&#41;SSAS](data-mining/data-mining-ssas.md)  
  
 ![Icono](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") de carpeta de archivos [pequeñopowerPivot para SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  Las características de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] varían según la edición. Los modelos multidimensional y de minería de datos están disponibles en la edición Standard, pero con menos características que en ediciones superiores. Los modelos tabulares y PowerPivot para SharePoint son características premium y no están disponibles en una licencia de la edición Standard. Para obtener más información, vea [Características admitidas por las ediciones de SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tutoriales de Analysis ServicesAnalysis Services &#40;&#41;SSAS](analysis-services-tutorials-ssas.md)   
 [Instalación para SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guía del desarrollador &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [Centro de recursos de SQL Server](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
