---
title: "(Nivel de compatibilidad de 1200) de creación de modelos tabulares | Documentos de Microsoft"
ms.custom: 
ms.date: 02/10/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
keywords:
- Analysis Services
- Modelo tabular
- Tutorial
- SSAS
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 3bf21d3debd7c24ea7b2e5ddcea56392e0f33400
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="tabular-modeling-1200-compatibility-level"></a>Modelado tabular (nivel de compatibilidad 1200)
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Este tutorial ofrece lecciones sobre cómo crear un modelo tabular de Analysis Services en el [nivel de compatibilidad 1200](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) utilizando [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)e implementar el modelo en Analysis Services servidor local o en Azure.  
 
Si usas 2017 de SQL Server o Analysis Services de Azure y desea crear el modelo en la compatibilidad de 1400 nivel, use la [Azure Analysis Services - tutorial de Adventure Works](https://review.docs.microsoft.com/azure/analysis-services/tutorials/aas-adventure-works-tutorial?branch=master). Esta versión actualizada utiliza la característica de obtener datos de nuevo y moderna para conectarse e importar datos de origen y usa el lenguaje de M para configurar las particiones.
 
  
## <a name="what-you-learn"></a>¿Qué aprenderá   
  
-   Cómo crear un nuevo proyecto de modelo tabular en SSDT.
  
-   Cómo importar datos de una base de datos relacional de SQL Server en un proyecto de modelo tabular.  
  
-   Cómo crear y administrar relaciones entre las tablas del modelo.  
  
-   Cómo crear y administrar cálculos, medidas e indicadores clave de rendimiento que ayuden a los usuarios a analizar los datos del modelo.  
  
-   Cómo crear y administrar perspectivas y jerarquías que ayudan a los usuarios más examinar fácilmente los datos del modelo proporcionando funciones empresariales y puntos de vista específicos de la aplicación.  
  
-   Cómo crear particiones que dividan los datos de la tabla en piezas lógicas más pequeñas que se puedan procesar independientemente de otras particiones.  
  
-   Cómo proteger los objetos y los datos del modelo creando roles con miembros de usuario.  
  
-   Cómo implementar un modelo tabular con un servidor Analysis Services en local o en Azure.  
  
## <a name="scenario"></a>Escenario  
Este tutorial se basa en Adventure Works Cycles, una compañía ficticia. Adventure Works es una empresa de gran empresa multinacional de fabricación y distribución de bicicletas de metal y de materiales compuestos en los mercados de Norteamérica, Europa y Asia. Con sede en Bothell, Washington, la compañía tiene a 500 trabajadores. Además, Adventure Works emplea varios equipos de ventas regionales en toda su base de mercado.  
  
Para satisfacer mejor las necesidades de análisis de datos de los equipos de ventas y marketing, y de los directivos, le encargan que cree un modelo tabular para que los usuarios analicen datos de las ventas por Internet de la base de datos de ejemplo AdventureWorksDW.  
  
Para completar el tutorial, y el modelo tabular Ventas por Internet de Adventure Works, debe realizar una serie de lecciones. En cada lección es una serie de tareas; es necesario para completar la lección completar cada tarea en orden. Mientras que en una determinada lección puede haber varias tareas que llevan a cabo un resultado similar, pero cómo completar cada tarea es ligeramente diferente. Esto sirve para mostrar que a menudo es más de una manera que se va a completar una tarea determinada como desafío práctica los conocimientos que ha aprendido en las tareas anteriores.  
  
El propósito de las lecciones es guiarle por la creación de un modelo tabular básico que se ejecuta en modo en memoria usando muchas de las características incluidas en SSDT. Como cada lección se basa en la anterior, debe completar las lecciones en orden. Una vez que haya completado todas las lecciones, ha creado e implementado el modelo tabular de ejemplo Adventure Works Internet Sales en un servidor de Analysis Services.  
  
Este tutorial no proporciona lecciones ni información sobre cómo administrar una base de datos del modelo tabular implementado utilizando SQL Server Management Studio o una aplicación cliente de informes para conectarse a un modelo implementado con objeto de examinar los datos del modelo.  
  
## <a name="prerequisites"></a>Requisitos previos  
Para completar este tutorial, necesitará los siguientes requisitos previos:  
  
-   La versión más reciente de [SSDT](../ssdt/download-sql-server-data-tools-ssdt.md).

-   La versión más reciente de SQL Server Management Studio. [Obtener la última versión](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). 
  
-   Una aplicación cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) o Excel.    
  
-   Una instancia de SQL Server con la base de datos de ejemplo Adventure Works DW. Esta base de datos de ejemplo incluye los datos necesarios para completar este tutorial. [Obtener la última versión](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  

-   Un Azure Analysis Services o SQL Server 2016 o posterior instancia de Analysis Services para implementar su modelo. [Registrarse para obtener una evaluación gratuita de Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/).
  
## <a name="lessons"></a>Lecciones  
Este tutorial incluye las siguientes lecciones:  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[Lección 1: Crear un nuevo proyecto de modelo tabular](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[Lección 2: Agregar datos](../analysis-services/lesson-2-add-data.md)|20 minutos|  
|[Lección 3: Marcar como tabla de fechas](../analysis-services/lesson-3-mark-as-date-table.md)|3 minutos|  
|[Lección 4: Crear relaciones](../analysis-services/lesson-4-create-relationships.md)|10 minutos|  
|[Lección 5: Crear columnas calculadas](../analysis-services/lesson-5-create-calculated-columns.md)|15 minutos|
|[Lección 6: Crear medidas](../analysis-services/lesson-6-create-measures.md)|30 minutos|  
|[Lección 7: Crear indicadores clave de rendimiento](../analysis-services/lesson-7-create-key-performance-indicators.md)|15 minutos|  
|[Lección 8: Crear perspectivas](../analysis-services/lesson-8-create-perspectives.md)|5 minutos|  
|[Lección 9: Crear jerarquías](../analysis-services/lesson-9-create-hierarchies.md)|20 minutos|  
|[Lección 10: Crear particiones](../analysis-services/lesson-10-create-partitions.md)|15 minutos|  
|[Lección 11: Crear Roles](../analysis-services/lesson-11-create-roles.md)|15 minutos|  
|[Lección 12: Analizar en Excel](../analysis-services/lesson-12-analyze-in-excel.md)|20 minutos| 
|[Lección 13: Implementar](../analysis-services/lesson-13-deploy.md)|5 minutos|  
  
## <a name="supplemental-lessons"></a>Lecciones complementarias  
Este tutorial también incluye [lecciones complementarias](http://msdn.microsoft.com/library/2018456f-b4a6-496c-89fb-043c62d8b82e). Los temas de esta sección no son necesarios para completar el tutorial, pero pueden ser útiles para comprender mejor las características avanzadas de creación de modelos tabulares.  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[Implementar seguridad dinámica utilizando filtros de filas](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)|30 minutos|  

  
## <a name="next-step"></a>Paso siguiente  
Para empezar el tutorial, vaya a la primera lección: [Lección 1: Crear un nuevo proyecto de modelo tabular](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

