---
title: Compatibilidad con versiones anteriores de SQL Server 2016 Analysis Services | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4906f3aec097b0bbdf63187cd760aa17a450316a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="analysis-services-backward-compatibility-sql-server-2016"></a>Compatibilidad con versiones anteriores de Analysis Services (SQL Server 2016)
[!INCLUDE[ssas-appliesto-sql2016](../includes/ssas-appliesto-sql2016.md)]

Este artículo describe los cambios en la disponibilidad de las características y el comportamiento entre la versión actual y la versión anterior.

## <a name="deprecated-features"></a>Características desusadas
A *característica en desuso* se interrumpirá del producto en una versión futura, pero todavía admitido e incluido en la versión actual para mantener la compatibilidad con versiones anteriores. Se recomienda que suspender el uso de características en desuso en proyectos nuevos y existentes para mantener la compatibilidad con futuras versiones.
  
Las siguientes características están en desuso en esta versión:
  
|||  
|-|-|  
|**Modo/categoría**|**Característica**|  
|Multidimensional|Particiones remotas|  
|Multidimensional|Grupos de medida vinculados remotos|  
|Multidimensional|Reescritura de dimensiones|  
|Multidimensional|Dimensiones vinculadas|   
|Multidimensional|Notificaciones de tabla de SQL Server para almacenamiento en caché automático.  <br />Lo que se va a sustituir es el uso del sondeo por el almacenamiento en caché automático. <br />Vea [Almacenamiento en caché automático &#40;dimensiones&#41;](../analysis-services/multidimensional-models-olap-logical-dimension-objects/proactive-caching-dimensions.md) y [Almacenamiento en caché automático &#40;particiones&#41;](../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).|  
|Multidimensional|Cubos de sesión. No hay ninguna sustitución.|  
|Multidimensional|Cubos locales. No hay ninguna sustitución.|  
|Tabular|Los niveles de compatibilidad 1100 y 1103 del modelo tabular no se admitirán en futuras versiones. La sustitución es establecer los modelos en el nivel de compatibilidad 1200 o superior, convertir las definiciones de modelo en metadatos tabulares. Consulte [Nivel de compatibilidad para modelos tabulares de Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|Herramientas|SQL Server Profiler para captura de seguimiento<br /><br /> La sustitución es usar el Generador de perfiles de eventos extendidos integrado en SQL Server Management Studio.  <br /> Consulte [Supervisar Analysis Services con SQL Server Extended Events](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md).|  
|Herramientas|Server Profiler para reproducción de seguimiento <br />Sustitución. No hay ninguna sustitución.|  
|Objetos de administración de seguimiento y API de seguimiento|Objetos de Microsoft.AnalysisServices.Trace (contiene las API para los objetos Trace y Replay de Analysis Services). La sustitución abarca varias partes:<br /><br /> -Configuración de seguimiento: Microsoft.SqlServer.Management.XEvent<br />: Hacer seguimiento de lectura: Microsoft.SqlServer.XEvent.Linq<br />- Reproducción de seguimiento: ninguna|  
  
> [!NOTE]  
>  Los anuncios de características anteriormente en desuso de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] siguen en vigor. Dado que todavía no se ha eliminado del producto el código que respalda esas características, muchas de ellas siguen estando presentes en esta versión. Mientras características anteriormente en desuso podría ser accesible, se siguen considerando en desuso y podría estar físicamente quitado del producto en cualquier momento.  

## <a name="discontinued-features"></a>Características no incluidas
A *no incluye la característica* ha quedado obsoleta en la versión anterior. Puede continuar para incluirse en la versión actual, pero ya no se admite. Se pueden quitar características no incluidas en una futura versión completamente o actualizar.

Las siguientes características están en desuso en la versión anterior y ya no se admiten en esta versión.

|||  
|-|-|  
|**Característica**|**Sustitución o solución alternativa**|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Ninguno. Esta característica ha quedado obsoleta en SQL Server 2005.|  
|[CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|Ninguno. Esta característica ha quedado obsoleta en SQL Server 2005.|  
|Sugerencia del optimizador de consultas NON_EMPTY_BEHAVIOR|Ninguno. Esta característica ha quedado obsoleta en SQL Server 2008.|  
|Ensamblados COM|Ninguno. Esta característica ha quedado obsoleta en SQL Server 2008.|  
|Propiedad de celda intrínseca CELL_EVALUATION_LIST|Ninguno. Esta característica ha quedado obsoleta en SQL Server 2005.|  
  
> [!NOTE]  
>  Los anuncios de características anteriormente en desuso de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] siguen en vigor. Dado que todavía no se ha eliminado del producto el código que respalda esas características, muchas de ellas siguen estando presentes en esta versión. Mientras características anteriormente en desuso podría ser accesible, se siguen considerando en desuso y podría estar físicamente quitado del producto en cualquier momento.  

## <a name="breaking-changes"></a>Cambios importantes
Un *cambio brusco* hace que un modelo de datos, el código de aplicación o el script dejen de funcionar después de actualizar el modelo o el servidor.
  
### <a name="net-40-version-upgrade"></a>Actualización de la versión de .NET 4.0  
 Las bibliotecas de cliente de Analysis Services Management Objects (AMO), ADOMD.NET y el modelo de objeto Tabular (TOM) ahora orientados al runtime de .NET 4.0. Esto puede ser un cambio importante para las aplicaciones que tienen como destino .NET 3.5. Las aplicaciones que usan versiones más recientes de estos ensamblados ahora deben tener como destino .NET 4.0 o versiones posteriores.  
  
### <a name="amo-version-upgrade"></a>Actualización de la versión de AMO  
 Esta versión es una actualización de versión para [objetos de administración de Analysis Services &#40;AMO&#41; ](https://msdn.microsoft.com/library/mt436122.aspx) y es una novedad en determinadas circunstancias.  Los scripts y el código existentes que llaman a AMO seguirán ejecutándose como antes si actualiza desde una versión anterior. Sin embargo, si necesita *recompilar* la aplicación y se dirige a una instancia de SQL Server 2016 Analysis Services, debe agregar el siguiente espacio de nombres para que el código o el script operativa:  
  
```  
  
using Microsoft.AnalysisServices;  
using Microsoft.AnalysisServices.Core;  
  
```  
  
 El espacio de nombres [Microsoft.AnalysisServices.Core](https://msdn.microsoft.com/library/microsoft.analysisservices.core.aspx) ahora es necesario cada vez que se hace referencia al ensamblado Microsoft.AnalysisServices en el código. Los objetos que anteriormente solo se encontraban en el espacio de nombres **Microsoft.AnalysisServices** se mueven al espacio de nombres principal en esta versión si el objeto se usa de la misma forma en los escenarios tabulares y multidimensionales.  Por ejemplo, las API relacionadas con el servidor se reubican en el espacio de nombres principal.  
  
 Aunque ahora hay varios espacios de nombres, ambos existen en el mismo ensamblado (Microsoft.AnalysisServices.dll).  
  
### <a name="xevent-discover-changes"></a>Cambios en XEvent DISCOVER  
 Para admitir mejor XEvent detectar la transmisión por secuencias en SSMS para SQL Server 2016 Analysis Services, `DISCOVER_XEVENT_TRACE_DEFINITION` se reemplaza con los seguimientos de XEvent siguientes:  
  
-   DISCOVER_XEVENT_PACKAGES  
  
-   DISCOVER_XEVENT_OBJECT  
  
-   DISCOVER_XEVENT_OBJECT_COLUMNS  
  
-   DISCOVER_XEVENT_SESSION_TARGETS  

## <a name="behavior-changes"></a>Cambios de comportamiento
Un *cambio de comportamiento* afecta a cómo funcionan o interactúan las características en la versión actual en comparación con las versiones anteriores de SQL Server.
  
Las revisiones de valores predeterminados, la configuración manual necesaria para completar una actualización o restaurar la funcionalidad o una nueva implementación de una característica existente son ejemplos de cambio de comportamiento en el producto.
  
Aquí se enumeran los comportamientos de características que han cambiado en esta versión pero que no alteran un modelo existente o el código posterior a la actualización.
  
### <a name="analysis-services-in-sharepoint-mode"></a>Analysis Services en modo de SharePoint
 Ya no se requiere la ejecución del Asistente para configuración de PowerPivot como tarea posterior a la instalación. Esto es cierto para todas las versiones admitidas de SharePoint que cargar los modelos de SQL Server 2016 Analysis Services actual.
  
### <a name="directquery-mode-for-tabular-models"></a>Modo DirectQuery para los modelos tabulares
 *DirectQuery* es un modo de acceso a datos para los modelos tabulares, donde se realiza la ejecución de la consulta en una base de datos relacional de back-end y se recupera un conjunto de resultados en tiempo real. A menudo se usa para grandes conjuntos de datos que no caben en la memoria o cuando los datos son volátiles y quiere que los datos más recientes se devuelvan en las consultas en un modelo tabular.
  
 DirectQuery ha existido como un modo de acceso a datos en las últimas versiones. En SQL Server 2016 Analysis Services, la implementación se ha revisado un poco, suponiendo que el modelo tabular es el nivel de compatibilidad 1200 o superior. DirectQuery tiene menos restricciones que antes. También tiene propiedades de base de datos diferentes.
  
 Si usa DirectQuery en un modelo tabular existente, puede mantener el modelo en su nivel actual de compatibilidad de 1100 o 1103 y seguir usando DirectQuery implementado para esos niveles. Como alternativa, puede actualizar a 1200 o superior para beneficiarse de las mejoras realizadas en DirectQuery.
  
 No hay ninguna actualización en contexto de un modelo de DirectQuery porque la configuración de los niveles de compatibilidad más antiguos no tiene homólogos exactos en los niveles de compatibilidad 1200 y superior más reciente. Si tiene un modelo tabular existente que se ejecuta en el modo DirectQuery, debe abrir el modelo en SQL Server Data Tools, desactivar DirectQuery, establezca el **nivel de compatibilidad** propiedad a 1200 o superior y después volver a configurar la de DirectQuery Propiedades. Vea [Directquerymode](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md) para obtener más información.


## <a name="see-also"></a>Vea también
[Compatibilidad con versiones anteriores de Analysis Services (SQL Server 2017)](analysis-services-backward-compatibility-sql2017.md)
