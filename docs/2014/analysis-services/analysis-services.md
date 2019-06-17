---
title: Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
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
ms.openlocfilehash: 241bb57ffd0ce05f1daa289cc7ae78c365a27cc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062340"
---
# <a name="analysis-services"></a>Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] es un motor de datos analíticos en línea que se usa en soluciones de ayuda a la toma de decisiones y Business Intelligence (BI), y proporciona los datos analíticos para informes empresariales y aplicaciones cliente como Excel, informes de Reporting Services y otras herramientas de BI de terceros. Un flujo de trabajo típico para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] incluye la creación de un modelo de datos OLAP o tabular, la implementación del modelo como base de datos en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], el procesamiento de la base de datos para cargarla con datos y, a continuación, la asignación de permisos para permitir el acceso a datos. Cuando esté listo, se puede obtener acceso a este modelo de datos con varios fines desde cualquier aplicación cliente que admita [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como origen de datos.  
  
 Para crear un modelo, use SQL Server Data Tools (vea [herramientas y aplicaciones utilizadas en Analysis Services](tools-and-applications-used-in-analysis-services.md)), elija una plantilla de proyecto Tabular o Multidimensional y minería de datos. La plantilla de proyecto contiene las carpetas de todos los objetos necesarios en un modelo. Puede utilizar asistentes para crear todos los elementos básicos, como orígenes de datos, vistas de origen de datos, dimensiones, cubos y roles.  
  
 Los modelos se rellenan con datos procedentes de sistemas de datos externos, normalmente almacenamientos de datos hospedados en un motor de base de datos relacional de SQL Server o de Oracle (los modelos tabulares admiten tipos de orígenes de datos adicionales). Los modelos especifican objetos de consulta, como los cubos, pero también especifican las dimensiones que se pueden usar en varios cubos, cálculos y KPI que encapsulan la lógica del negocio, así como interacciones, como los comportamientos en navegación y obtención de detalles.  
  
 Para usar un modelo, se implementa en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que ejecuta bases de datos en un modo de servidor determinado, haciendo que los datos estén disponibles para los usuarios autorizados que se conectan a través de Excel u otras aplicaciones.  
  
 Puede instalar una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en uno de estos tres modos de servidor:  
  
-   Como instancia tabular, ejecutando modelos tabulares.  
  
-   Como una instancia multidimensional y de minería de datos, ejecutando cubos OLAP y modelos de minería de datos (es el valor predeterminado).  
  
-   Como PowerPivot para SharePoint, ejecutando modelos de datos PowerPivot y de Excel en SharePoint (PowerPivot para SharePoint es un motor de datos de nivel intermedio que carga, consulta y actualiza modelos de datos hospedados en SharePoint).  
  
 El mismo motor de datos; tres formas de usarlo. Tenga en cuenta que los modos de servidor se establecen durante la instalación y no se pueden cambiar posteriormente. Debe instalar una nueva instancia si necesita otro modo diferente.  
  
 La documentación fundacional de Analysis Services se organiza en las secciones que corresponden al tipo de proyecto que se está generando. Elija uno de los siguientes vínculos para obtener más información acerca de cada área de características o modo.  
  
 **Examinar contenido por área**  
 ![Icono carpeta de archivos pequeños](../../2014/integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") [comparar soluciones tabulares y multidimensionales &#40;SSAS&#41;](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Icono carpeta de archivos pequeños](../../2014/integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") [administración de la instancia de Analysis Services](instances/analysis-services-instance-management.md)  
  
 ![Icono carpeta de archivos pequeños](../../2014/integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") [modelado Tabular &#40;Tabular de SSAS&#41;](tabular-models/tabular-models-ssas.md)  
  
 ![Icono carpeta de archivos pequeños](../../2014/integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") [modelado Multidimensional &#40;SSAS&#41;](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Icono carpeta de archivos pequeños](../../2014/integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") [minería de datos &#40;SSAS&#41;](data-mining/data-mining-ssas.md)  
  
 ![Icono carpeta de archivos pequeños](../../2014/integration-services/media/filefolder-small.gif "archivo pequeño icono de carpeta") [PowerPivot para SharePoint &#40;SSAS&#41;](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  Las características de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] varían según la edición. Los modelos multidimensional y de minería de datos están disponibles en la edición Standard, pero con menos características que en ediciones superiores. Los modelos tabulares y PowerPivot para SharePoint son características premium y no están disponibles en una licencia de la edición Standard. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales de Analysis Services &#40;SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [Instalación de SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guía del desarrollador &#40;Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [SQL Server Resource Center](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
