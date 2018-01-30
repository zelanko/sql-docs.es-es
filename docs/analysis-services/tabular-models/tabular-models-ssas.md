---
title: Los modelos tabulares | Documentos de Microsoft
ms.custom: 
ms.date: 01/29/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: edeea89c1d767364f4f087d0f4b2e6d566895c52
ms.sourcegitcommit: c77a8ac1ab372927c09bf241d486e96881b61ac9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="tabular-models"></a>Modelos tabulares
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Los modelos tabulares son bases de datos de Analysis Services que se ejecutan en memoria o en el modo DirectQuery, acceso a datos directamente desde los orígenes de datos relacionales de back-end.  
  
 In-Memory es el valor predeterminado. Utiliza algoritmos avanzados de compresión y el procesador de consultas multiproceso, el motor de análisis ofrece un acceso rápido a datos y objetos del modelo tabular mediante la notificación de las aplicaciones cliente, como Power BI y Excel.  
  
 DirectQuery es un modo de consulta alternativo para los modelos que son demasiado grandes para caber en la memoria o cuando la volatilidad de los datos impide una estrategia de procesamiento razonable. En esta versión, DirectQuery logra una paridad mayor con modelos en memoria mediante la compatibilidad con orígenes de datos adicionales, la capacidad para manejar tablas calculadas y columnas de un modelo DirectQuery, la seguridad de nivel de fila a través de expresiones de DAX que llegan a la base de datos back-end y las optimizaciones de consultas que producen un rendimiento más rápido que en versiones anteriores.
  
 Los modelos tabulares se crean en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mediante la plantilla de proyecto de modelo tabular que proporciona una superficie de diseño para crear un modelo, tablas, relaciones y expresiones DAX. Puede importar datos de varios orígenes y luego enriquecer el modelo agregando relaciones, columnas y tablas calculadas, medidas, KPI, jerarquías y traducciones.  
  
 Los modelos se pueden implementar en los servicios de análisis de Azure o una instancia de SQL Server Analysis Services configurado para el modo de servidor Tabular. Los modelos tabulares implementados pueden administrarse en SQL Server Management Studio, al igual que los modelos multidimensionales. También se pueden crear particiones de los mismos para optimizar el procesamiento y protegerlos en el nivel de fila usando la seguridad basada en roles.  
  
## <a name="in-this-section"></a>En esta sección  
 [Soluciones de modelos tabulares](../../analysis-services/tabular-models/tabular-model-solutions-ssas-tabular.md) -temas de esta sección describen la creación e implementación de soluciones de modelos tabulares.
  
 [Las bases de datos de modelo tabular](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md) -temas de esta sección describen la administración de soluciones de modelos tabulares implementada.
  
 [Acceso a datos de modelo tabular](../../analysis-services/tabular-models/tabular-model-data-access.md) -temas de esta sección describen los conecta a implementar soluciones de modelos tabulares.
  
## <a name="see-also"></a>Vea también  
 [Novedades de Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Comparar soluciones tabulares y multidimensionales](../../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)   
 [Herramientas y aplicaciones utilizadas en Analysis Services](../../analysis-services/tools-and-applications-used-in-analysis-services.md)   
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
