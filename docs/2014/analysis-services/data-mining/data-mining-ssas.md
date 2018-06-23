---
title: Minería de datos (SSAS) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], about data mining
ms.assetid: b1c912da-72f6-4d96-89c8-55a2c4f19e88
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b118f03580aeb0053203cd2535bafecd1649ccb4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199025"
---
# <a name="data-mining-ssas"></a>Minería de datos (SSAS)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona una plataforma integrada para las soluciones que incorporan la minería de datos. Puede usar datos relacionales o de cubo para crear soluciones de Business Intelligence con análisis predictivos.  
  
## <a name="benefits-of-data-mining"></a>Ventajas de la minería de datos  
 La minería de datos usa principios estadísticos contrastados para detectar patrones en los datos, ayudándole a tomar decisiones inteligentes sobre problemas complejos. La aplicación de los algoritmos de minería de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a los datos le permitirá predecir tendencias, identificar patrones, crear reglas y recomendaciones, analizar la secuencia de eventos en conjuntos de datos complejos y obtener nuevos puntos de vista.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la minería de datos es eficaz y accesible, y está integrada con las herramientas preferidas de los usuarios para el análisis y la creación de informes. Vea los vínculos de esta sección para obtener toda la información sobre la minería de datos que necesita para empezar.  
  
## <a name="key-data-mining-features"></a>Características clave de la minería de datos  
 SQL Server proporciona las siguientes características para las soluciones integradas de minería de datos:  
  
-   Varios orígenes de datos: no es necesario crear un almacenamiento de datos o un cubo OLAP para realizar la minería de datos. Puede usar datos tabulares de proveedores eternos, hojas de cálculo e incluso archivos de texto. También puede minar con facilidad cubos OLAP creados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Sin embargo, no se pueden usar datos de una base de datos en memoria.  
  
-   Limpieza de los datos integrados, administración de datos y ETL: Data Quality Services proporcionan herramientas avanzadas para la generación de perfiles y la limpieza de datos. Se puede usar Integration Services para generar procesos ETL de limpieza de datos, y también para tareas de creación, procesamiento, entrenamiento y actualización de modelos.  
  
-   Varios algoritmos personalizables: además de proporcionar algoritmos como la agrupación en clústeres, las redes neuronales y los árboles de decisión, la plataforma le permite desarrollar sus propios complementos con algoritmos personalizados.  
  
-   Infraestructura de prueba del modelo: pruebe los modelos y los conjuntos de datos usando herramientas estadísticas tan importantes como la validación cruzada, las matrices de clasificación, los gráficos de mejora respecto al modelo predictivo y los gráficos de dispersión. Cree y administre fácilmente conjuntos de prueba y entrenamiento.  
  
-   Consultas y obtención de detalles: cree consultas de predicción, recupere patrones y estadísticas de modelos, y obtenga información detallada de los datos de los casos.  
  
-   Herramientas de cliente: además de los estudios de desarrollo y diseño proporcionados por SQL Server, puede usar los Complementos de minería de datos para Excel para crear, consultar y examinar los modelos. O bien crear clientes personalizados, incluidos servicios web.  
  
-   Compatibilidad con el lenguaje de scripting y API administrada: todos los objetos de minería de datos son completamente programables. El scripting es posible mediante MDX, XMLA o las extensiones de PowerShell para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Use el lenguaje DMX (Extensiones de minería de datos) para crear rápidamente consultas y scripts.  
  
-   Seguridad e implementación: proporciona seguridad basada en roles a través de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], incluidos permisos distintos para la obtención de detalles del modelo y los datos de la estructura. Fácil implementación de modelos en otros servidores, de forma que los usuarios puedan tener acceso a los patrones o realizar predicciones.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas de esta sección presentan las características principales de la minería de datos de SQL Server y las tareas relacionadas.  
  
-   [Conceptos de minería de datos](data-mining-concepts.md)  
  
-   [Algoritmos de minería de datos &#40;Analysis Services: minería de datos&#41;](data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [Estructuras de minería de datos &#40;Analysis Services: minería de datos&#41;](mining-structures-analysis-services-data-mining.md)  
  
-   [Modelos de minería de datos &#40;Analysis Services: minería de datos&#41;](mining-models-analysis-services-data-mining.md)  
  
-   [Prueba y validación &#40;minería de datos&#41;](testing-and-validation-data-mining.md)  
  
-   [Consultas de minería de datos](data-mining-queries.md)  
  
-   [Soluciones de minería de datos](data-mining-solutions.md)  
  
-   [Herramientas de minería de datos](data-mining-tools.md)  
  
-   [Arquitectura de minería de datos](data-mining-architecture.md)  
  
-   [Información general sobre seguridad &#40;minería de datos&#41;](security-overview-data-mining.md)  
  
  