---
title: SQL Server 2014 Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
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
ms.openlocfilehash: a5117ec8fd1eae9438569289b05f465fe7616d96
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887457"
---
# <a name="sql-server-2014-analysis-services"></a>SQL Server 2014 Analysis Services

  SQL Server 2014 Analysis Services es un motor de datos analíticos que se usa en las soluciones de inteligencia empresarial (BI) y ayuda a la toma de decisiones, y proporciona los datos analíticos para informes empresariales y aplicaciones cliente como Excel, informes Reporting Services y otros herramientas de BI de terceros. 

## <a name="about-sql-server-analysis-services-documentation"></a>Acerca de SQL Server Analysis Services documentación

La documentación está separada por la versión. Actualmente está en SQL Server 2014 Analysis Services documentación.

- Para obtener más información sobre SQL Server 2012 y versiones anteriores, consulte [SQL Server documentación de versiones anteriores](https://docs.microsoft.com/previous-versions/sql/).
- Para obtener más información acerca de SQL Server 2014, vea los [libros en pantalla de SQL Server 2014](../2014-toc/books-online-for-sql-server-2014.md)
- Para obtener más información sobre SQL Server 2016 y versiones posteriores, consulte la [documentación de Microsoft SQL](https://docs.microsoft.com/sql/).
- Para obtener más información sobre Azure Analysis Services, consulte la [documentación de Azure Analysis Services](https://docs.microsoft.com/en-us/azure/analysis-services/).

## <a name="analysis-services-workflow"></a>Analysis Services flujo de trabajo

Un flujo de trabajo típico incluye la creación de un modelo de datos OLAP o tabular, implementar el modelo como una base de datos en una instancia de servidor, procesar la base de datos para cargarla con datos y, a continuación, asignar permisos para permitir el acceso a datos. Cuando esté listo, se puede obtener acceso a este modelo de datos con varios fines desde cualquier aplicación cliente que admita [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como origen de datos.  
  
 Para crear un modelo, use SQL Server Data Tools (vea [herramientas y aplicaciones utilizadas en Analysis Services](tools-and-applications-used-in-analysis-services.md)) y elija una plantilla de proyecto tabular o multidimensional y de minería de datos. La plantilla de proyecto contiene las carpetas de todos los objetos necesarios en un modelo. Puede utilizar asistentes para crear todos los elementos básicos, como orígenes de datos, vistas de origen de datos, dimensiones, cubos y roles.  
  
 Los modelos se rellenan con datos procedentes de sistemas de datos externos, normalmente almacenamientos de datos hospedados en un motor de base de datos relacional de SQL Server o de Oracle (los modelos tabulares admiten tipos de orígenes de datos adicionales). Los modelos especifican objetos de consulta, como los cubos, pero también especifican las dimensiones que se pueden usar en varios cubos, cálculos y KPI que encapsulan la lógica del negocio, así como interacciones, como los comportamientos en navegación y obtención de detalles.  
  
 Para usar un modelo, se implementa en una instancia del servidor que ejecuta bases de datos en un modo de servidor determinado, lo que hace que los datos estén disponibles para los usuarios autorizados que se conectan a través de Excel u otras aplicaciones.  
  
 Puede instalar una instancia de en uno de los tres modos de servidor:  
  
-   Como instancia tabular, ejecutando modelos tabulares.  
  
-   Como una instancia multidimensional y de minería de datos, ejecutando cubos OLAP y modelos de minería de datos (es el valor predeterminado).  
  
-   Como PowerPivot para SharePoint, ejecutando modelos de datos PowerPivot y de Excel en SharePoint (PowerPivot para SharePoint es un motor de datos de nivel intermedio que carga, consulta y actualiza modelos de datos hospedados en SharePoint).  
  
 El mismo motor de datos; tres formas de usarlo. Tenga en cuenta que los modos de servidor se establecen durante la instalación y no se pueden cambiar posteriormente. Debe instalar una nueva instancia si necesita otro modo diferente.  
  
 La documentación fundacional de Analysis Services se organiza en las secciones que corresponden al tipo de proyecto que se está generando. Elija uno de los siguientes vínculos para obtener más información acerca de cada área de características o modo.  
  
 **Examinar contenido por área**  
 ![Icono pequeño de carpeta de archivos](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") [Comparación de las soluciones &#40;tabulares y multidimensionales SSAS&#41; ](comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") [Administración de instancias de Analysis Services](instances/analysis-services-instance-management.md)  
  
 ![Icono pequeño de carpeta de archivos](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") [Modelado &#40;tabular&#41; SSAS tabular](tabular-models/tabular-models-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") [Modelado &#40;multidimensional SSAS&#41; ](multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") [SSAS&#41; de &#40;minería de datos](data-mining/data-mining-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../../2014/integration-services/media/filefolder-small.gif "Icono pequeño de carpeta de archivos") [PowerPivot para SharePoint &#40;SSAS&#41; ](power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
> [!NOTE]  
>  Las características de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] varían según la edición. Los modelos multidimensional y de minería de datos están disponibles en la edición Standard, pero con menos características que en ediciones superiores. Los modelos tabulares y PowerPivot para SharePoint son características premium y no están disponibles en una licencia de la edición Standard. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales de &#40;Analysis Services SSAS&#41;](analysis-services-tutorials-ssas.md)   
 [Instalación de SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Guía &#40;del desarrollador Analysis Services&#41;](analysis-services-developer-documentation.md)   
 [SQL Server centro de recursos](https://go.microsoft.com/fwlink/?linkID=219676)   
 [SQLCat.com](https://go.microsoft.com/fwlink/?linkID=220963)  
  
  
