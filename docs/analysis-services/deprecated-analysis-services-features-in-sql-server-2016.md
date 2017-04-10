---
title: "Caracter&#237;sticas en desuso de Analysis Services en SQL Server 2016 | Microsoft Docs"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services, compatibilidad con versiones anteriores"
  - "SSAS, compatibilidad con versiones anteriores"
  - "SQL Server Analysis Services, compatibilidad con versiones anteriores"
  - "características en desuso [Analysis Services]"
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
caps.latest.revision: 52
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 52
---
# Caracter&#237;sticas en desuso de Analysis Services en SQL Server 2016
  Una *característica en desuso* es una característica que se eliminará del producto en una versión futura, pero que aún se admite y se incluye en la versión actual para mantener la compatibilidad con versiones anteriores. Normalmente, una característica en desuso se quita en una versión principal, dos versiones después del anuncio original. Por ejemplo, las características en desuso anunciadas en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] es probable que no se admitan en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 **No se admite en la próxima versión principal de SQL Server**  
  
|||  
|-|-|  
|**Categoría**|**Característica**|  
|Multidimensional|Particiones remotas|  
|Multidimensional|Grupos de medida vinculados remotos|  
|Multidimensional|Reescritura de dimensiones|  
|Multidimensional|Dimensiones vinculadas|  
  
 **No se admite en una versión futura de SQL Server**  
  
|||  
|-|-|  
|**Categoría**|**Característica**|  
|Multidimensional|Notificaciones de tabla de SQL Server para almacenamiento en caché automático.  <br />Lo que se va a sustituir es el uso del sondeo por el almacenamiento en caché automático. <br />Vea [Almacenamiento en caché automático &#40;dimensiones&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) y [Almacenamiento en caché automático &#40;particiones&#41;](../Topic/Proactive%20Caching%20\(Partitions\).md).|  
|Multidimensional|Cubos de sesión. No hay ninguna sustitución.|  
|Multidimensional|Cubos locales. No hay ninguna sustitución.|  
|Tabular|Los niveles de compatibilidad 1100 y 1103 del modelo tabular no se admitirán en futuras versiones. La sustitución es establecer los modelos en el nivel de compatibilidad 1200 y convertir las definiciones de modelo en metadatos tabulares. Consulte [Compatibility Level for Tabular models in Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|Herramientas|SQL Server Profiler para captura de seguimiento<br /><br /> La sustitución es usar el Generador de perfiles de eventos extendidos integrado en SQL Server Management Studio.  <br /> Consulte [Monitor Analysis Services with SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Herramientas|Server Profiler para reproducción de seguimiento <br />Sustitución. No hay ninguna sustitución.|  
|Objetos de administración de seguimiento y API de seguimiento|Objetos de Microsoft.AnalysisServices.Trace (contiene las API para los objetos Trace y Replay de Analysis Services). La sustitución abarca varias partes:<br /><br /> - Configuración de seguimiento: Microsoft.SqlServer.Management.XEvent<br />- Lectura de seguimiento: Microsoft.SqlServer.XEvent.Linq<br />- Reproducción de seguimiento: ninguna|  
  
> [!NOTE]  
>  Los anuncios de características anteriormente en desuso de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] siguen en vigor. Dado que todavía no se ha eliminado del producto el código que respalda esas características, muchas de ellas siguen estando presentes en esta versión. Aunque las características anteriormente en desuso podrían ser aún accesibles, se siguen considerando en desuso y se podrían eliminar físicamente del producto en cualquier momento durante la versión de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . Se recomienda evitar el uso de características en desuso en los nuevos modelos o aplicaciones basadas en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## Vea también  
 [Compatibilidad con versiones anteriores de Analysis Services](../analysis-services/analysis-services-backward-compatibility.md)   
 [Funcionalidad de Analysis Services suspendida en SQL Server 2016](../analysis-services/discontinued-analysis-services-functionality-in-sql-server-2016.md)  
  
  