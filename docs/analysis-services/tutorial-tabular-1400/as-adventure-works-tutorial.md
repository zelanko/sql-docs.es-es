---
title: Tutorial de Analysis Services Adventure Works Internet Sales (1400) | Microsoft Docs
ms.date: 05/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 39d4c0e19d89438aa08ff2f7ead24184196d5412
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503284"
---
# <a name="adventure-works-internet-sales-tutorial-1400"></a>Tutorial de Adventure Works Internet Sales (1400)

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Este tutorial proporciona lecciones sobre cómo crear e implementar un modelo tabular en el [nivel de compatibilidad 1400](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md). Si está familiarizado con Analysis Services y el modelado tabular, completar este tutorial es la forma más rápida para obtener información sobre cómo crear e implementar un modelo tabular básico mediante Visual Studio. Una vez que tenga los requisitos previos de forma local, debe tener dos o tres horas en completarse.  
  
## <a name="what-you-learn"></a>¿Qué aprenderá   
  
-   Cómo crear un nuevo proyecto de modelo tabular en el **nivel de compatibilidad 1400** en Visual Studio con SSDT.
  
-   Cómo importar datos desde una base de datos relacional en una base de datos del área de trabajo de proyecto de modelo tabular.  
  
-   Cómo crear y administrar relaciones entre las tablas del modelo.  
  
-   Cómo crear columnas calculadas, medidas e indicadores de rendimiento de clave que ayudan a los usuarios a analizar métricas empresariales fundamentales.  
  
-   Cómo crear y administrar perspectivas y jerarquías que ayudan a los usuarios más examinar fácilmente los datos del modelo proporcionando empresariales y los puntos de vista específicos de la aplicación.  
  
-   Cómo crear particiones que dividan los datos de la tabla en piezas lógicas más pequeñas que se puedan procesar independientemente de otras particiones.  
  
-   Cómo proteger los objetos y los datos del modelo creando roles con miembros de usuario.  
  
-   Cómo implementar un modelo tabular en un **Azure Analysis Services** server o **SQL Server 2017 Analysis Services** server mediante SSDT.  
  
## <a name="prerequisites"></a>Requisitos previos  

Para completar este tutorial, necesitará:  
  
-   Un servidor de Azure Analysis Services o un servidor de SQL Server 2017 Analysis Services en modo Tabular. Regístrese para obtener una [evaluación de Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) y [crear un servidor](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server) o descargar una segunda oportunidad [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).

-   Un [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal) con el **base de datos de ejemplo AdventureWorksDW**, o un almacenamiento de datos local SQL Server con un [base de datos de ejemplo AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). Al instalar una base de datos AdventureWorksDW en un almacén de datos local SQL Server, use la versión de base de datos de ejemplo que se corresponde con la versión del servidor. 

    **Importante:** Si instala la base de datos de ejemplo para un almacenamiento de datos local SQL Server e implementa el modelo en un servidor de Azure Analysis Services, un [puerta de enlace de datos local](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) es necesario.

-   La versión más reciente de [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx). O bien, si ya tiene Visual Studio 2017, puede descargar e instalar [proyectos de Microsoft Analysis Services](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) paquete (VSIX). Para este tutorial, las referencias a Visual Studio y SSDT son sinónimos. 

-   La versión más reciente de [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Una aplicación cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) o Excel. 

## <a name="scenario"></a>Escenario  

En este tutorial se basa en Adventure Works Cycles, una compañía ficticia. Adventure Works es una empresa de fabricación gran multinacional que produce y distribuye bicicletas, piezas y accesorios de mercados de Norteamérica, Europa y Asia. La compañía tiene a 500 trabajadores. Además, Adventure Works emplea varios equipos regionales de ventas a lo largo de su base de mercado. El proyecto consiste en crear un modelo tabular para que los usuarios de ventas y marketing analicen datos de ventas por Internet en la base de datos AdventureWorksDW.  
  
Para completar el tutorial, debe realizar varias lecciones. En cada lección, hay tareas. Es necesario para completar la lección completarlas todas en orden. Mientras que en una determinada lección puede haber varias tareas que obtienen un resultado similar, pero cómo completar cada tarea es ligeramente diferente. Este método se muestra a menudo hay más de una manera para completar una tarea y para ponerle conocimientos que ha adquirido en tareas y lecciones anteriores.  
  
El propósito de las lecciones es guiarle a través de la creación de un modelo tabular básico mediante el uso de muchas de las características incluidas en SSDT. Como cada lección se basa en la anterior, debe completar las lecciones en orden.
  
En este tutorial no proporciona lecciones sobre cómo administrar un servidor en Azure portal, la administración de un servidor o base de datos mediante SSMS o mediante una aplicación cliente para examinar los datos de modelo. 


## <a name="lessons"></a>Lecciones  

Este tutorial incluye las siguientes lecciones:  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[1: crear un nuevo proyecto de modelo tabular](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
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

Estas lecciones no son necesarias para completar el tutorial, pero pueden ser útil para una mejor comprensión avanzadas de modelos tabulares características de creación.  
  
|Lección|Tiempo estimado para completar la lección|  
|----------|------------------------------|  
|[Filas de detalles](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10 minutos|
|[Seguridad dinámica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30 minutos|
|[Jerarquías desiguales](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20 minutos| 

  
## <a name="next-steps"></a>Pasos siguientes  

Para empezar, vea [lección 1: Cree un nuevo proyecto de modelo tabular](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

