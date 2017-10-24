---
title: Analysis Services | Documentos de Microsoft
ms.date: 05/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- Analysis Services, about Analysis Services - Multidimensional Data
- SSAS
- Analysis Services
- SQL Server Analysis Services, about Analysis Services - Multidimensional Data
- SQL Server Analysis Services
- multidimensional data [Analysis Services]
- SSAS, about Analysis Services - Multidimensional Data
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8c3a514f91e9af8de54fdbd4d9ef851c72f1911e
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="what-is-analysis-services"></a>¿Qué es Analysis Services?
  Analysis Services es un motor de datos analíticos utilizado en la toma de decisiones y análisis de negocios, proporciona los datos analíticos para informes empresariales y aplicaciones cliente como Power BI, Excel, informes de Reporting Services y otras herramientas de visualización de datos.  
  
 Un flujo de trabajo típico incluye la creación de un modelo de datos multidimensional o tabular, implementar el modelo como una base de datos a una instancia de servidor de SQL Server Analysis Services o Azure Analysis Services local, configuración de procesamiento de datos periódico y asignar permisos para permitir el acceso a los datos por los usuarios finales. Cuando esté listo, el modelo de datos semántica son accesibles por cualquier aplicación de cliente compatible con Analysis Services como un origen de datos.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>Analysis Services local y en la nube
Analysis Services está ahora disponible en la nube como un servicio de Azure. Azure Analysis Services es compatible con los modelos tabulares en los niveles de compatibilidad 1200 y versiones posteriores. Se admiten todas las traducciones, particiones, seguridad de nivel de fila, relaciones bidireccionales y DirectQuery. Para obtener más información y probar esta función de forma gratuita, consulte [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/). 
  
## <a name="server-mode"></a>Modo de servidor  
 Al instalar Analysis Services mediante el programa de instalación de SQL Server, durante la configuración de especificar un modo de servidor para esa instancia.  Cada modo tiene características únicas para una solución específica de Analysis Services.   
  
-   **Modo tabular** : datos relacionales en memoria de implementar, modelado construcciones (modelo, tablas, columnas, medidas, jerarquías).  

-   **Modo multidimensional y de minería de datos** : permite implementar construcciones de modelado OLAP (cubos, dimensiones, medidas). 

-   **Power Pivot Mode** -implemente PowerPivot y Excel modelos de datos de SharePoint (PowerPivot para SharePoint es un motor de datos de nivel intermedio que carga, consulta y actualiza modelos de datos hospedados en SharePoint).  
  
 Una instancia única se puede configurar con un solo modo y no se puede modificar posteriormente.  Puede instalar varias instancias con diferentes modos en el mismo servidor, pero necesitará ejecutar el programa de instalación y especificar los valores de configuración para cada instancia. Para obtener información detallada y una comparación de características diferentes que se ofrecen en cada uno de los modos, consulte [comparar tabulares y multidimensionales](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md).
  
## <a name="authoring-and-managing-solutions"></a>Creación y administración de soluciones  
 Para crear un modelo e implementarlo en un servidor, use SQL Server Data Tools, la elección de plantilla de proyecto ya sea un Tabular o Multidimensional y minería de datos. La plantilla de proyecto contiene las carpetas de todos los objetos necesarios en un modelo. Diseñadores y asistentes para ayudarán a crear muchos de los elementos básicos, como la conexión con roles, relaciones, medidas y orígenes de datos. Una vez que la base de datos de modelo se implementa en un servidor, use SQL Server Management Studio (SSMS) para configurar el procesamiento de datos, supervisar y administrar el servidor y las bases de datos. Para obtener más información, consulte [herramientas y aplicaciones utilizadas en Analysis Services](../analysis-services/tools-and-applications-used-in-analysis-services.md). 
  
## <a name="documentation-by-area"></a>Documentación por área  
En general, la documentación de Azure Analysis Services se incluye con la documentación de Azure. Y documentación de SQL Server Analysis Services se incluye con la documentación de SQL. Sin embargo, al menos para los modelos tabulares, cómo crear e implementar sus proyectos es el mismo independientemente de qué plataforma está usando.  
   
*  [Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)
*  [Novedades en SQL Server Analysis Services](../analysis-services/what-s-new-in-analysis-services.md)   
*  [Comparar soluciones tabulares y multidimensionales](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
*  [Modelos tabulares](../analysis-services/tabular-models/tabular-models-ssas.md)  
*  [Modelos multidimensionales](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
*  [Minería de datos](../analysis-services/data-mining/data-mining-ssas.md)  
*  [PowerPivot para SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
*  [Administración de instancias](../analysis-services/instances/analysis-services-instance-management.md)    
*  [Tutoriales](../analysis-services/analysis-services-tutorials-ssas.md)   
*  [Documentación para desarrolladores](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
*  [Referencia técnica (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)

