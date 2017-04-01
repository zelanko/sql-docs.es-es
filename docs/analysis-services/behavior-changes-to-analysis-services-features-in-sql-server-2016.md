---
title: "Cambios de comportamiento en las caracter&#237;sticas de Analysis Services en SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# Cambios de comportamiento en las caracter&#237;sticas de Analysis Services en SQL Server 2016
  Un *cambio de comportamiento* afecta a cómo funcionan o interactúan las características en la versión actual en comparación con las versiones anteriores de SQL Server.  
  
 Las revisiones de valores predeterminados, la configuración manual necesaria para completar una actualización o restaurar la funcionalidad o una nueva implementación de una característica existente son ejemplos de cambio de comportamiento en el producto.  
  
 Aquí se enumeran los comportamientos de características que han cambiado en esta versión pero que no alteran un modelo existente o el código posterior a la actualización.  
  
> [!NOTE]  
>  A diferencia de un *cambio de comportamiento*, un *cambio drástico* es el que evita que un modelo de datos o aplicación integrada con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se ejecute después de actualizar un servidor, herramienta de cliente o modelo. Para ver la lista, visite [Cambios recientes en las características de Analysis Services en SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md).  
  
## Analysis Services en modo de SharePoint  
 Ya no se requiere la ejecución del Asistente para configuración de PowerPivot como tarea posterior a la instalación. Esto es válido para todas las versiones compatibles de SharePoint que cargan modelos de la versión actual de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
## Modo DirectQuery para los modelos tabulares  
 *DirectQuery* es un modo de acceso a datos para los modelos tabulares, donde se realiza la ejecución de la consulta en una base de datos relacional de back-end y se recupera un conjunto de resultados en tiempo real. A menudo se usa para grandes conjuntos de datos que no caben en la memoria o cuando los datos son volátiles y quiere que los datos más recientes se devuelvan en las consultas en un modelo tabular.  
  
 DirectQuery ha existido como un modo de acceso a datos en las últimas versiones. En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], la implementación se ha revisado un poco, suponiendo que el modelo tabular está en el nivel de compatibilidad 1200. DirectQuery tiene menos restricciones que antes. También tiene propiedades de base de datos diferentes.  
  
 Si usa DirectQuery en un modelo tabular existente, puede mantener el modelo en su nivel actual de compatibilidad de 1100 o 1103 y seguir usando DirectQuery implementado para esos niveles. Como alternativa, puede actualizar a 1200 para beneficiarse de las mejoras realizadas en DirectQuery en esta versión de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 No hay ninguna actualización local de un modelo de DirectQuery porque la configuración de niveles de compatibilidad anteriores no tiene homólogos exactos en el nivel de compatibilidad de 1200 más reciente. Si tiene un modelo tabular existente que se ejecuta en el modo DirectQuery, debe abrir el modelo en SQL Server Data Tools, desactivar DirectQuery, establecer la propiedad del **nivel de compatibilidad** en 1200 y después volver a configurar las propiedades de DirectQuery como se definen para los modelos tabulares de 1200. Obtenga más información en [Modo DirectQuery &#40;SSAS tabular&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).  
  
## Vea también  
 [Compatibilidad con versiones anteriores](../Topic/Backward%20Compatibility_deleted.md)   
 [Cambios recientes en las características de Analysis Services en SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md)   
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Descargar SQL Server Data Tools](https://msdn.microsoft.com/en-us/library/mt204009.aspx)  
  
  