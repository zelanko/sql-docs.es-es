---
title: "Creaci&#243;n de modelos tabulares (tutorial de Adventure Works) | Microsoft Docs"
ms.custom: ""
ms.date: "03/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
keywords: 
  - "Analysis Services"
  - "Modelo tabular"
  - "Tutorial"
  - "SSAS"
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: 40
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 35
---
# Creaci&#243;n de modelos tabulares (tutorial de Adventure Works)
En este tutorial se proporcionan lecciones sobre cómo crear un modelo tabular de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services mediante [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
  
## Lo que aprenderá  
En el transcurso de este tutorial, aprenderá lo siguiente:  
  
-   Cómo crear un proyecto de modelo tabular en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
-   Cómo importar datos de una base de datos relacional de SQL Server en un proyecto de modelo tabular.  
  
-   Cómo crear y administrar relaciones entre las tablas del modelo.  
  
-   Cómo crear y administrar cálculos, medidas e indicadores clave de rendimiento que ayuden a los usuarios a analizar los datos del modelo.  
  
-   Cómo crear y administrar perspectivas y jerarquías que ayuden a los usuarios a examinar más fácilmente los datos del modelo mediante puntos de vista específicos del negocio y de la aplicación.  
  
-   Cómo crear particiones que dividan los datos de la tabla en piezas lógicas más pequeñas que se puedan procesar independientemente de otras particiones.  
  
-   Cómo proteger los objetos y los datos del modelo creando roles con miembros de usuario.  
  
-   Cómo implementar un modelo tabular en un espacio aislado o en una instancia de producción de Analysis Services que se ejecuta en modo tabular.  
  
## Escenario  
Este tutorial se basa en [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)], una compañía ficticia. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] es una multinacional dedicada a la fabricación y distribución de bicicletas de metal y de metal compuesto en mercados de Norteamérica, Europa y Asia. Las oficinas centrales de [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] se encuentran en Bothell, Washington, donde la compañía tiene 500 trabajadores. Además, [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] tiene contratados a varios equipos de ventas regionales en toda su base de mercado.  
  
Para satisfacer mejor las necesidades de análisis de datos de los equipos de ventas y marketing, y de los directivos, le encargan que cree un modelo tabular para que los usuarios analicen datos de las ventas por Internet de la base de datos de ejemplo AdventureWorksDW.  
  
Para completar el tutorial, y el modelo tabular Ventas por Internet de Adventure Works, debe realizar una serie de lecciones. Dentro de cada lección hay varias tareas; la realización de cada tarea en orden es necesaria para completar la lección. Mientras que en una determinada lección puede haber varias tareas con las que se obtiene un resultado similar, el modo en que se completa cada tarea puede ser ligeramente diferente. Es decir, a menudo hay varias formas de completar una determinada tarea, y para su realización tendrá que poner en práctica los conocimientos que aprendió en tareas anteriores.  
  
El propósito de las lecciones es guiarle por la creación de un modelo tabular básico que se ejecute en modo en memoria usando muchas de las características incluidas en [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Como cada lección se basa en la anterior, debe completar las lecciones en orden. Cuando haya completado todas las lecciones, habrá creado e implementado el modelo tabular de ejemplo Venta por Internet de Adventure Works en un servidor de Análisis Services.  
  
Este tutorial no proporciona lecciones ni información sobre cómo administrar una base de datos del modelo tabular implementado utilizando SQL Server Management Studio o una aplicación cliente de informes para conectarse a un modelo implementado con objeto de examinar los datos del modelo.  
  
## Requisitos previos  
Para completar este tutorial, debe tener los siguientes requisitos previos instalados:  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Instancia de Analysis Services que se ejecuta en modo Tabular.  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. [Obtenga la versión más reciente.](https://msdn.microsoft.com/library/mt204009.aspx)  
  
-   Base de datos de ejemplo de Adventure Works DW 2014. Esta base de datos de ejemplo incluye los datos necesarios para completar este tutorial. Para descargar la base de datos de ejemplo, vaya a [http://go.microsoft.com/fwlink/?LinkID=335807](http://go.microsoft.com/fwlink/?LinkID=335807).  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 o posterior (para su uso con la característica Analizar en Excel de la lección 11).  
  
## Lecciones  
Este tutorial incluye las siguientes lecciones:  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[Lección 1: Crear un nuevo proyecto de modelo tabular](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[Lección 2: Agregar datos](../analysis-services/lesson-2-add-data.md)|20 minutos|  
|[Lección 3: Cambiar el nombre de las columnas](../analysis-services/lesson-3-rename-columns.md)|20 minutos|  
|[Lección 4: Marcar como tabla de fechas](../analysis-services/lesson-4-mark-as-date-table.md)|3 minutos|  
|[Lección 5: Crear relaciones](../analysis-services/lesson-5-create-relationships.md)|10 minutos|  
|[Lección 6: Crear columnas calculadas](../analysis-services/lesson-6-create-calculated-columns.md)|15 minutos|  
|[Lección 7: Crear medidas](../analysis-services/lesson-7-create-measures.md)|30 minutos|  
|[Lección 8: Crear indicadores clave de rendimiento](../analysis-services/lesson-8-create-key-performance-indicators.md)|15 minutos|  
|[Lección 9: Crear perspectivas](../Topic/Lesson%209:%20Create%20Perspectives.md)|5 minutos|  
|[Lección 10: Crear jerarquías](../analysis-services/lesson-10-create-hierarchies.md)|20 minutos|  
|[Lección 11: Crear particiones](../analysis-services/lesson-11-create-partitions.md)|15 minutos|  
|[Lección 12: Crear roles](../analysis-services/lesson-12-create-roles.md)|15 minutos|  
|[Lección 13: Analizar en Excel](../analysis-services/lesson-13-analyze-in-excel.md)|20 minutos|  
|[Lección 14: Implementar](../analysis-services/lesson-14-deploy.md)|5 minutos|  
  
## Lecciones complementarias  
Este tutorial también incluye [lecciones complementarias](../Topic/Supplemental%20Lessons.md). Los temas de esta sección no son necesarios para completar el tutorial, pero pueden ser útiles para comprender mejor las características avanzadas de creación de modelos tabulares.  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[Implementar seguridad dinámica utilizando filtros de filas](../analysis-services/implement-dynamic-security-by-using-row-filters.md)|30 minutos|  
|[Configurar las propiedades de notificación para informes de Power View](../analysis-services/configure-reporting-properties-for-power-view-reports.md)|30 minutos|  
  
## Paso siguiente  
Para empezar el tutorial, vaya a la primera lección: [Lección 1: Crear un nuevo proyecto de modelo tabular](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
  
  
