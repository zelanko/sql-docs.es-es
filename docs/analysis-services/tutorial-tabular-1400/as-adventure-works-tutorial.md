---
title: Tutorial de Analysis Services Adventure Works (1400) | Documentos de Microsoft
description: Presenta el tutorial de Adventure Works de Analysis Services
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 10ceeb85ee97162fb753e84d997d105edb3cf9a4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="tabular-modeling-1400-compatibility-level"></a>Modelado tabular (nivel de compatibilidad de 1400)

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Este tutorial ofrece lecciones sobre cómo crear e implementar un modelo tabular en el [nivel de compatibilidad de 1400](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md). Si está familiarizado con Analysis Services y creación de modelos tabular, completar este tutorial es la forma más rápida de obtener información sobre cómo crear e implementar un modelo tabular básico mediante Visual Studio. Una vez que tenga los requisitos previos de forma local, debe tomar dos o tres horas en completarse.  
  
## <a name="what-you-learn"></a>¿Qué aprenderá   
  
-   Cómo crear un nuevo proyecto de modelo tabular en el **nivel de compatibilidad de 1400** en Visual Studio con SSDT.
  
-   Cómo importar datos desde una base de datos relacional en una base de datos del área de trabajo de proyecto de modelo tabular.  
  
-   Cómo crear y administrar relaciones entre las tablas del modelo.  
  
-   Cómo crear columnas calculadas, medidas e indicadores clave de rendimiento que ayudan a los usuarios analizar métricas empresariales críticas.  
  
-   Cómo crear y administrar perspectivas y jerarquías que ayudan a los usuarios más examinar fácilmente los datos del modelo proporcionando funciones empresariales y puntos de vista específicos de la aplicación.  
  
-   Cómo crear particiones que dividan los datos de la tabla en piezas lógicas más pequeñas que se puedan procesar independientemente de otras particiones.  
  
-   Cómo proteger los objetos y los datos del modelo creando roles con miembros de usuario.  
  
-   Cómo implementar un modelo tabular en un **Azure Analysis Services** server o **2017 Analysis Services de SQL Server** servidor mediante SSDT.  
  
## <a name="prerequisites"></a>Requisitos previos  

Para completar este tutorial, necesitará:  
  
-   Un servidor de Analysis Services de Azure o un servidor de SQL Server de 2017 Analysis Services en modo Tabular. Registrarse para obtener una segunda [prueba de Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) y [crear un servidor](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server) o descargar una segunda [2017 Developer Edition de SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).

-   Un [almacenamiento de datos de SQL Azure](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal) con el **base de datos de ejemplo AdventureWorksDW**, o un almacenamiento de datos local SQL Server con un [base de datos de ejemplo AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). Al instalar una base de datos AdventureWorksDW a un almacenamiento de datos local SQL Server, use la versión de base de ejemplo que se corresponde con la versión del servidor. 

    **Importante:** si instalar la base de datos de ejemplo a un almacenamiento de datos local SQL Server e implementar el modelo a un servidor de Analysis Services de Azure, un [puerta de enlace de datos local](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) es necesario.

-   La versión más reciente de [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx). O bien, si ya tiene Visual Studio de 2017, puede descargar e instalar [proyectos de Microsoft Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) paquete (VSIX). Para este tutorial, las referencias a SSDT y Visual Studio son sinónimas. 

-   La versión más reciente de [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Una aplicación cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) o Excel. 

## <a name="scenario"></a>Escenario  

Este tutorial se basa en Adventure Works Cycles, una compañía ficticia. Adventure Works es una empresa de fabricación multinacional dedicada y distribución de bicicletas, partes y accesorios para los mercados de Norteamérica, Europa y Asia. La compañía tiene a 500 trabajadores. Además, Adventure Works emplea varios equipos de ventas regionales en toda su base de mercado. El proyecto consiste en crear un modelo tabular para que los usuarios de ventas y marketing analizar datos de la base de datos AdventureWorksDW ventas por Internet.  
  
Para completar el tutorial, debe completar varias lecciones. En cada lección hay tareas. Es necesario para completar la lección completar cada tarea en orden. Mientras que en una determinada lección puede haber varias tareas que llevan a cabo un resultado similar, pero cómo completar cada tarea es ligeramente diferente. Este método se muestra a menudo hay más de una manera que se va a completar una tarea como desafío práctica los conocimientos que ha aprendido en tareas y lecciones anteriores.  
  
El propósito de las lecciones es guiarle por la creación de un modelo tabular básico mediante el uso de muchas de las características incluidas en SSDT. Como cada lección se basa en la anterior, debe completar las lecciones en orden.
  
Este tutorial no proporciona lecciones sobre cómo administrar un servidor en el portal de Azure, administración de un servidor o base de datos con SSMS o mediante una aplicación cliente para examinar los datos de modelo. 


## <a name="lessons"></a>Lecciones  

Este tutorial incluye las siguientes lecciones:  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[1 - crear un nuevo proyecto de modelo tabular](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[2 - Obtener datos](../tutorial-tabular-1400/as-lesson-2-get-data.md)|10 minutos|  
|[3 - Marcar como tabla de fechas](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)|3 minutos|  
|[4 - Crear relaciones](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)|10 minutos|  
|[5 - Crear columnas calculadas](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)|15 minutos|
|[6 - Crear medidas](../tutorial-tabular-1400/as-lesson-6-create-measures.md)|30 minutos|  
|[7 - crear indicadores clave de rendimiento (KPI)](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)|15 minutos|  
|[8 - Crear perspectivas](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)|5 minutos|  
|[9 - Crear jerarquías](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)|20 minutos|  
|[10 - Crear particiones](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)|15 minutos|  
|[11 - Crear roles](../tutorial-tabular-1400/as-lesson-11-create-roles.md)|15 minutos|  
|[12 - Analizar en Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)|5 minutos| 
|[13 - Implementar](../tutorial-tabular-1400/as-lesson-13-deploy.md)|5 minutos|  
  
## <a name="supplemental-lessons"></a>Lecciones complementarias  

Estas lecciones no son necesarias para completar este tutorial, pero pueden resultar útil para una mejor comprensión tabulares avanzadas del modelo características de creación.  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[Filas de detalles](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 minutos|
|[Seguridad dinámica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 minutos|
|[Jerarquías desiguales](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 minutos| 

  
## <a name="next-steps"></a>Pasos siguientes  

Para empezar, vea [lección 1: crear un nuevo proyecto de modelo tabular](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

