---
title: Tabular (nivel de compatibilidad 1200) de modelado | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b0b8d60c6c365d48f8eccc46cbc9a3b0f5222ff5
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38054692"
---
# <a name="tabular-modeling-1200-compatibility-level"></a>Modelado tabular (nivel de compatibilidad 1200)
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Este tutorial proporciona lecciones sobre cómo crear un modelo tabular de Analysis Services en el [nivel de compatibilidad 1200](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) utilizando [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)e implementar el modelo en Analysis Services servidor local o en Azure.  
 
Si usa SQL Server 2017 o Azure Analysis Services, y desea crear el modelo en la compatibilidad de 1400 nivel, utilice el [(nivel de compatibilidad 1400) de modelos tabulares](tutorial-tabular-1400/as-adventure-works-tutorial.md). Esta versión actualizada usa la característica moderna de obtención de datos para conectarse e importar datos de origen, usa el lenguaje M configuración de particiones e incluye lecciones complementarias adicionales.

> [!IMPORTANT]
> Debe crear los modelos tabulares en el nivel de compatibilidad más reciente compatible con el servidor. Modelos de nivel de compatibilidad con versiones posteriores ofrecen un rendimiento mejorado, características adicionales y se actualizarán más sin problemas a los niveles de compatibilidad con versiones futuras.
 
  
## <a name="what-you-learn"></a>¿Qué aprenderá   
  
-   Cómo crear un nuevo proyecto de modelo tabular en SSDT.
  
-   Cómo importar datos de una base de datos relacional de SQL Server en un proyecto de modelo tabular.  
  
-   Cómo crear y administrar relaciones entre las tablas del modelo.  
  
-   Cómo crear y administrar cálculos, medidas e indicadores clave de rendimiento que ayuden a los usuarios a analizar los datos del modelo.  
  
-   Cómo crear y administrar perspectivas y jerarquías que ayudan a los usuarios más examinar fácilmente los datos del modelo proporcionando empresariales y los puntos de vista específicos de la aplicación.  
  
-   Cómo crear particiones de dividir los datos de tabla en piezas lógicas más pequeñas, que se pueden procesar independientemente de otras particiones.  
  
-   Cómo proteger los objetos y los datos del modelo creando roles con miembros de usuario.  
  
-   Cómo implementar un modelo tabular en Analysis Services server local o en Azure.  
  
## <a name="scenario"></a>Escenario  
En este tutorial se basa en Adventure Works Cycles, una compañía ficticia. Adventure Works es una empresa de fabricación multinacional dedicada que genera bicicletas, piezas y accesorios de mercados de Norteamérica, Europa y Asia. Con sede en Bothell, Washington, la compañía tiene a 500 trabajadores. Además, Adventure Works emplea varios equipos regionales de ventas a lo largo de su base de mercado.  
  
Para satisfacer mejor las necesidades de análisis de datos de los equipos de ventas y marketing, y de los directivos, le encargan que cree un modelo tabular para que los usuarios analicen datos de las ventas por Internet de la base de datos de ejemplo AdventureWorksDW.  
  
Para completar el tutorial, y el modelo tabular Ventas por Internet de Adventure Works, debe realizar una serie de lecciones. En cada lección es un número de tareas; es necesario para completar la lección completarlas todas en orden. Mientras que en una determinada lección puede haber varias tareas que obtienen un resultado similar, pero cómo completar cada tarea es ligeramente diferente. Esto consiste en demostrar que a menudo hay más de una manera para completar una tarea determinada y para ponerle conocimientos que ha adquirido en tareas anteriores.  
  
El propósito de las lecciones es guiarle a través de la creación de un modelo tabular básico que se ejecuta en modo en memoria mediante el uso de muchas de las características incluidas en SSDT. Como cada lección se basa en la anterior, debe completar las lecciones en orden. Una vez haya completado todas las lecciones, ha creado e implementado el modelo tabular de ejemplo Adventure Works Internet Sales en un servidor de Analysis Services.  
  
Este tutorial no proporciona lecciones ni información sobre cómo administrar una base de datos del modelo tabular implementado utilizando SQL Server Management Studio o una aplicación cliente de informes para conectarse a un modelo implementado con objeto de examinar los datos del modelo.  
  
## <a name="prerequisites"></a>Requisitos previos  
Para completar este tutorial, necesita los siguientes requisitos previos:  
  
-   La versión más reciente de [SSDT](../ssdt/download-sql-server-data-tools-ssdt.md).

-   La versión más reciente de SQL Server Management Studio. [Obtener la última versión](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). 
  
-   Una aplicación cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) o Excel.    
  
-   Una instancia de SQL Server con la base de datos de ejemplo Adventure Works DW. Esta base de datos de ejemplo incluye los datos necesarios para completar este tutorial. [Obtener la última versión](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  

-   Una Azure Analysis Services o SQL Server 2016 o posterior instancia de Analysis Services para implementar el modelo. [Registrarse para obtener una evaluación gratuita de Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/).
  
## <a name="lessons"></a>Lecciones  
Este tutorial incluye las siguientes lecciones:  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[Lección 1: Crear un nuevo proyecto de modelo tabular](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[Lección 2: Agregar datos](../analysis-services/lesson-2-add-data.md)|20 minutos|  
|[Lección 3: Marcar como tabla de fechas](../analysis-services/lesson-3-mark-as-date-table.md)|3 minutos|  
|[Lección 4: Creación de relaciones](../analysis-services/lesson-4-create-relationships.md)|10 minutos|  
|[Lección 5: Crear columnas calculadas](../analysis-services/lesson-5-create-calculated-columns.md)|15 minutos|
|[Lección 6: Crear medidas](../analysis-services/lesson-6-create-measures.md)|30 minutos|  
|[Lección 7: Crear indicadores clave de rendimiento](../analysis-services/lesson-7-create-key-performance-indicators.md)|15 minutos|  
|[Lección 8: Crear perspectivas](../analysis-services/lesson-8-create-perspectives.md)|5 minutos|  
|[Lección 9: Creación de jerarquías](../analysis-services/lesson-9-create-hierarchies.md)|20 minutos|  
|[Lección 10: Creación de particiones](../analysis-services/lesson-10-create-partitions.md)|15 minutos|  
|[Lección 11: Creación de Roles](../analysis-services/lesson-11-create-roles.md)|15 minutos|  
|[Lección 12: Analizar en Excel](../analysis-services/lesson-12-analyze-in-excel.md)|20 minutos| 
|[Lección 13: Implementar](../analysis-services/lesson-13-deploy.md)|5 minutos|  
  
## <a name="supplemental-lessons"></a>Lecciones complementarias  
Este tutorial también incluye [lecciones complementarias](http://msdn.microsoft.com/library/2018456f-b4a6-496c-89fb-043c62d8b82e). Los temas de esta sección no son necesarios para completar el tutorial, pero pueden ser útiles para comprender mejor las características avanzadas de creación de modelos tabulares.  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[Implementar seguridad dinámica utilizando filtros de filas](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)|30 minutos|  

  
## <a name="next-step"></a>Paso siguiente  
Para empezar el tutorial, vaya a la primera lección: [Lección 1: Crear un nuevo proyecto de modelo tabular](../analysis-services/lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

