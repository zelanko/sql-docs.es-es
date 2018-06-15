---
title: Minería de datos (SSAS) | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7468074eb8a18dd9448e558cadebdc9f07ffc2cb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34014822"
---
# <a name="data-mining-ssas"></a>Minería de datos (SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha sido un líder en el análisis predictivo desde la versión en el año 2000 al proporcionar la minería de datos en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La combinación de la minería de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona una plataforma integrada para el análisis predictivo en la que se incluye la limpieza de los datos, la preparación, el aprendizaje automático y la generación de informes. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] En la minería de datos se incluyen varios algoritmos estándar, como los modelos de clústeres EM y mediana-K, redes neuronales, regresión logística y regresión lineal, árboles de decisión y clasificadores de Bayes naive. Todos los modelos tienen visualizaciones integradas para ayudarle a desarrollar, restringir y evaluar los modelos.  Integrar la minería de datos en una solución de inteligencia empresarial le ayudará a tomar decisiones inteligentes sobre problemas complejos.  
  
## <a name="benefits-of-data-mining"></a>Ventajas de la minería de datos  
 La minería de datos (también denominado análisis predictivo y aprendizaje automático) usa principios estadísticos documentados para detectar patrones en los datos. La aplicación de los algoritmos de minería de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a los datos le permitirá predecir tendencias, identificar patrones, crear reglas y recomendaciones, analizar la secuencia de eventos en conjuntos de datos complejos y obtener nuevos puntos de vista.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la minería de datos es eficaz y accesible, y está integrada con las herramientas preferidas de los usuarios para el análisis y la creación de informes.  
  
## <a name="key-data-mining-features"></a>Características clave de la minería de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Minería de datos proporciona las siguientes características para las soluciones integradas de minería de datos:  
  
-   Varios orígenes de datos: puede usar cualquier origen de datos tabulares para la minería de datos, incluidas hojas de cálculo y archivos de texto. También puede minar con facilidad cubos OLAP creados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Sin embargo, no se pueden usar datos de una base de datos en memoria.  
  
-   Características integradas de limpieza de datos, administración de datos y generación de informes: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona herramientas para la generación de perfiles y la limpieza de los datos. Puede crear procesos ETL para limpiar datos al preparar el modelado y, además, ssISnoversion permite repetir el aprendizaje y actualizar los modelos fácilmente.  
  
-   Varios algoritmos personalizables: además de proporcionar algoritmos como la agrupación en clústeres, las redes neuronales y los árboles de decisión, la minería de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le permite desarrollar sus propios complementos con algoritmos personalizados.  
  
-   Infraestructura de prueba del modelo: pruebe los modelos y los conjuntos de datos usando herramientas estadísticas tan importantes como la validación cruzada, las matrices de clasificación, los gráficos de mejora respecto al modelo predictivo y los gráficos de dispersión. Cree y administre fácilmente conjuntos de prueba y entrenamiento.  
  
-   Creación de consultas y obtención de detalles: la minería de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona el lenguaje DMX para integrar las consultas de predicción en las aplicaciones. También puede recuperar estadísticas detalladas y patrones de los modelos, y obtener detalles de datos de casos.  
  
-   Herramientas de cliente: además de los estudios de desarrollo y diseño proporcionados por SQL Server, puede usar los Complementos de minería de datos para Excel para crear, consultar y examinar los modelos. O bien crear clientes personalizados, incluidos servicios web.  
  
-   Compatibilidad con el lenguaje de scripting y API administrada: todos los objetos de minería de datos son completamente programables. El scripting es posible mediante MDX, XMLA o las extensiones de PowerShell para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Use el lenguaje DMX (Extensiones de minería de datos) para crear rápidamente consultas y scripts.  
  
-   Seguridad e implementación: proporciona seguridad basada en roles a través de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], incluidos permisos distintos para la obtención de detalles del modelo y los datos de la estructura. Fácil implementación de modelos en otros servidores, de forma que los usuarios puedan tener acceso a los patrones o realizar predicciones.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas de esta sección presentan las características principales de la minería de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las tareas relacionadas.  
  
-   [Conceptos de minería de datos](../../analysis-services/data-mining/data-mining-concepts.md)  
  
-   [Algoritmos de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [Estructuras de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
-   [Modelos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
-   [Prueba y validación & #40; minería de datos & #41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
-   [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)  
  
-   [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md)  
  
-   [Herramientas de minería de datos](../../analysis-services/data-mining/data-mining-tools.md)  
  
-   [Arquitectura de minería de datos](../../analysis-services/data-mining/data-mining-architecture.md)  
  
-   [Información general de Seguridad &#40;minería de datos&#41;](../../analysis-services/data-mining/security-overview-data-mining.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
