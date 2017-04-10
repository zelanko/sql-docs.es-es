---
title: "Analysis Services | Microsoft Docs"
ms.date: "03/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
helpviewer_keywords: 
  - "Analysis Services, sobre Analysis Services: datos multidimensionales"
  - "SSAS"
  - "Analysis Services"
  - "SQL Server Analysis Services, acerca de Analysis Services: datos multidimensionales"
  - "SQL Server Analysis Services"
  - "datos multidimensionales [Analysis Services]"
  - "SSAS, acerca de Analysis Services: datos multidimensionales"
ms.assetid: 49d186f4-4b4d-4a5a-bb1a-e2699c64a731
caps.latest.revision: 60
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 60
---
# Analysis Services
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] es un motor de datos analíticos en línea que se usa en la ayuda para la toma de decisiones y en el análisis empresarial, y proporciona los datos analíticos para informes empresariales y aplicaciones cliente como Power BI, Excel, informes de Reporting Services y otras herramientas de visualización de datos.  
  
 Un flujo de trabajo típico para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] es crear un modelo de datos tabulares o multidimensionales, implementar el modelo como una base de datos en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , procesar la base de datos para cargarla con datos o metadatos, configurar la actualización de datos y asignar permisos para permitir que los usuarios finales puedan acceder a los datos. Cuando esté listo, se puede acceder a este modelo de datos semántico multiusos desde cualquier aplicación cliente que admita [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como origen de datos.  
  
 Los modelos se rellenan con datos procedentes de sistemas de datos externos, normalmente almacenamientos de datos hospedados en un motor de base de datos relacional de SQL Server o de Oracle (los modelos tabulares admiten tipos de orígenes de datos adicionales). Los modelos especifican objetos de consulta, como los cubos, pero también especifican las dimensiones que se pueden usar en varios cubos, cálculos y KPI que encapsulan la lógica del negocio, así como interacciones, como los comportamientos en navegación y obtención de detalles.  
 
## <a name="analysis-services-on-premises-and-in-the-cloud"></a>Analysis Services local y en la nube
Analysis Services está ahora disponible en la nube como un servicio de Azure. Actualmente en versión preliminar, Azure Analysis Services admite los modelos tabulares en el nivel de compatibilidad 1200. Se admiten todas las traducciones, particiones, seguridad de nivel de fila, relaciones bidireccionales y DirectQuery. Para obtener más información y probar esta función de forma gratuita, consulte [Azure Analysis Services](https://azure.microsoft.com/en-us/services/analysis-services/). 
  
## <a name="server-mode"></a>Modo de servidor  
 Al instalar Analysis Services con el programa de instalación de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , durante la configuración especificará un modo de servidor para esa instancia.  Cada modo tiene características únicas para una solución específica de Analysis Services.  
  
-   **Modo multidimensional y de minería de datos** : permite implementar construcciones de modelado OLAP (cubos, dimensiones, medidas).  
  
-   **Modo tabular** : permite implementar construcciones de modelado de datos relacionales en memoria (modelo, tablas, columnas).  
  
     Los modelos tabulares se pueden crear con el nivel de compatibilidad predeterminado (1200), con las características más recientes, o bien con el nivel de compatibilidad más antiguo (1103). Existen diferencias importantes entre los niveles de compatibilidad. Para obtener más información sobre cómo se comparan los niveles, consulte [Nivel de compatibilidad para modelos tabulares de Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
-   **Modo Power Pivot** : permite implementar modelos de datos de Excel y [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] en SharePoint ([!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint es un motor de datos de nivel intermedio que carga, consulta y actualiza modelos de datos hospedados en SharePoint).  
  
 Una instancia única se puede configurar con un solo modo y no se puede modificar posteriormente.  Puede instalar varias instancias con diferentes modos en el mismo servidor, pero necesitará ejecutar el programa de instalación y especificar los valores de configuración para cada instancia.  
  
 Las características de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] varían según la edición. Para obtener más información, consulte [Características compatibles con las ediciones de SQL Server 2016](../sql-server/características-compatibles-con-las-ediciones-de-sql-server-2016.md). 
  
## <a name="authoring-solutions"></a>Soluciones de creación  
 Para crear un modelo, use SQL Server Data Tools (vea [Herramientas y aplicaciones usadas en Analysis Services](../analysis-services/tools-and-applications-used-in-analysis-services.md)) y elija una plantilla de proyecto tabular o multidimensional y de minería de datos. La plantilla de proyecto contiene las carpetas de todos los objetos necesarios en un modelo. Puede usar asistentes para crear algunos de los elementos básicos, como orígenes de datos, vistas del origen de datos, dimensiones, cubos y roles.  
  
## <a name="documentation-by-area"></a>Documentación por área  
La documentación de Analysis Services se organiza en secciones, que se corresponden con el tipo de proyecto que vaya a crear. Elija uno de los siguientes vínculos para obtener más información acerca de cada área de características o modo.  
   
 ![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Novedades](../analysis-services/what-s-new-in-analysis-services.md)  
  
 ![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Comparar soluciones tabulares y multidimensionales](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Modelos tabulares](../analysis-services/tabular-models/tabular-models-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Modelos multidimensionales](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Minería de datos](../analysis-services/data-mining/data-mining-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos")[ PowerPivot para SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)  
  
 ![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Administración de una instancia de Analysis Services](../analysis-services/instances/analysis-services-instance-management.md)  
   
 ![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Tutoriales de Analysis Services](../analysis-services/analysis-services-tutorials-ssas.md)  
  
![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Documentación para desarrolladores de Analysis Services](https://msdn.microsoft.com/library/bb500153(SQL.130).aspx)  
 
![Icono pequeño de carpeta de archivos](../analysis-services/media/filefolder-small.png "Icono pequeño de carpeta de archivos") [Referencia técnica (SSAS)](../analysis-services/powershell/technical-reference-ssas.md)