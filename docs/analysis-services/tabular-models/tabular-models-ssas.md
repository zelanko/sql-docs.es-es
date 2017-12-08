---
title: Los modelos tabulares (SSAS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 1d770b114a708301f884de76d7c6a4cc39227195
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="tabular-modeling-ssas"></a>Modelos tabulares (SSAS)
  Los modelos tabulares son bases de datos de Analysis Services que se ejecutan en memoria o en el modo DirectQuery, de tal forma que se accede a los datos directamente desde los orígenes de datos relacionales de back-end.  
  
 In-Memory es el valor predeterminado. Gracias a los algoritmos de compresión avanzados y al procesador de consultas multiproceso, el motor analítico en memoria ofrece un acceso rápido a los objetos y los datos de los modelos tabulares para aplicaciones cliente de informes como Microsoft Excel y Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
 DirectQuery es un modo de consulta alternativo para los modelos que son demasiado grandes para caber en la memoria o cuando la volatilidad de los datos impide una estrategia de procesamiento razonable. En esta versión, DirectQuery logra una paridad mayor con modelos en memoria mediante la compatibilidad con orígenes de datos adicionales, la capacidad para manejar tablas calculadas y columnas de un modelo DirectQuery, la seguridad de nivel de fila a través de expresiones de DAX que llegan a la base de datos back-end y las optimizaciones de consultas que producen un rendimiento más rápido que en versiones anteriores.
  
 Los modelos tabulares se crean en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mediante la plantilla de proyecto de modelo tabular que proporciona una superficie de diseño para crear un modelo, tablas, relaciones y expresiones DAX. Puede importar datos de varios orígenes y luego enriquecer el modelo agregando relaciones, columnas y tablas calculadas, medidas, KPI, jerarquías y traducciones.  
  
 Los modelos se pueden implementar en una instancia de Analysis Services configurada para el modo de servidor tabular, donde las aplicaciones cliente de informes pueden conectarse con ellos. Los modelos implementados se pueden administrar en SQL Server Management Studio del mismo modo que los modelos multidimensionales. También se pueden crear particiones de los mismos para optimizar el procesamiento y protegerlos en el nivel de fila usando la seguridad basada en roles.  
  
## <a name="in-this-section"></a>En esta sección  
 [Soluciones de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md): en los temas de esta sección se explica la creación e implementación de soluciones de modelos tabulares.
  
 [Bases de datos de modelo tabular &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md): en los temas de esta sección se explica la administración de soluciones de modelos tabulares implementadas.
  
 [Acceso a datos de modelos tabulares](../../analysis-services/tabular-models/tabular-model-data-access.md): en los temas de esta sección se explica la conexión a soluciones de modelos tabulares implementadas.
  
## <a name="see-also"></a>Vea también  
 [Novedades de Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Comparar soluciones tabulares y multidimensionales &#40;SSAS&#41;](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Herramientas y aplicaciones utilizadas en Analysis Services](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [Modo DirectQuery &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
