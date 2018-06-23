---
title: Tutorial DMX de predicción de Series de tiempo | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38ea7c03-4754-4e71-896a-f68cc2c98ce2
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2a9e3e5db1e0f21bfe3822d73fd0e3c0b456e250
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312203"
---
# <a name="time-series-prediction-dmx-tutorial"></a>Tutorial DMX de predicción de series temporales
  En este tutorial aprenderá a crear una estructura de minería de datos de serie temporal, creará tres series temporales personalizadas y, a continuación, realizará predicciones utilizando esos modelos.  
  
 Los modelos de minería de datos se basan en los datos incluidos en la base de datos de ejemplo [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], que almacena datos de la empresa ficticia [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] es una gran empresa multinacional de fabricación.  
  
## <a name="tutorial-scenario"></a>Escenario del tutorial  
 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] ha decidido utilizar la minería de datos para generar previsiones de ventas. Ya han creado algunos modelos de previsión regionales; Para obtener más información, consulte [lección 2: generar un escenario de previsión &#40;Tutorial intermedio de minería de datos&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md). Sin embargo, el departamento de ventas necesita poder actualizar periódicamente el modelo de minería de datos con nuevos datos de ventas. El departamento desea también personalizar los modelos para proporcionar previsiones diferentes.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona varias herramientas que pueden usarse para realizar esta tarea:  
  
-   El lenguaje de consulta Extensiones de minería de datos (DMX)  
  
-   El algoritmo de serie temporal de Microsoft  
  
-   El Editor de consultas de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]  
  
 El algoritmo de serie temporal de [!INCLUDE[msCoName](../includes/msconame-md.md)] crea modelos que se pueden utilizar para predecir datos relacionados con el tiempo. Extensiones de minería de datos (DMX) es un lenguaje de consulta proporcionado por [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que sirve para crear modelos de minería de datos y consultas de predicción.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 En este tutorial se presupone que ya está familiarizado con los objetos que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza para crear modelos de minería de datos. Si se ha no ha creado una estructura de minería de datos o el modelo de minería de datos mediante DMX, vea [Bike Buyer DMX Tutorial](../../2014/tutorials/bike-buyer-dmx-tutorial.md).  
  
 El tutorial está compuesto por las lecciones siguientes:  
  
 [Lección 1: Crear una serie temporal de modelo de minería de datos y la estructura de minería de datos](../../2014/tutorials/lesson-1-creating-a-time-series-mining-model-and-mining-structure.md)  
 En esta lección aprenderá a usar la instrucción `CREATE MINING MODEL` para agregar un nuevo modelo previsión y un modelo de minería de datos relacionado.  
  
 [Lección 2: Agregar modelos de minería de datos a la estructura de minería de datos de serie temporal](../../2014/tutorials/lesson-2-adding-mining-models-to-the-time-series-mining-structure.md)  
 En esta lección aprenderá a usar la instrucción ALTER MINING STRUCTURE para agregar nuevos modelos de minería de datos a la estructura de serie temporal. Aprenderá también a personalizar el algoritmo utilizado para analizar una serie temporal.  
  
 [Lección 3: Procesar la estructura y modelos de la serie temporal](../../2014/tutorials/lesson-3-processing-the-time-series-structure-and-models.md)  
 En esta lección aprenderá a entrenar los modelos utilizando la instrucción `INSERT INTO` y rellenando la estructura con datos de la base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)].  
  
 [Lección 4: Crear predicciones de serie temporal utilizando DMX](../../2014/tutorials/lesson-4-creating-time-series-predictions-using-dmx.md)  
 En esta lección aprenderá a crear predicciones de serie temporal.  
  
 [Lección 5: Extender la serie temporal de modelo](../../2014/tutorials/lesson-5-extending-the-time-series-model.md)  
 En esta lección aprenderá a utilizar el parámetro `EXTEND_MODEL_CASES` para actualizar el modelo con nuevos datos al realizar las predicciones.  
  
## <a name="requirements"></a>Requisitos  
 Antes de hacer este tutorial, asegúrese de que los siguientes componentes estén instalados:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   La base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]  
  
 Con el fin de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada. Para instalar las bases de datos de ejemplo oficiales para [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vaya a [ http://www.CodePlex.com/MSFTDBProdSamples ](http://go.microsoft.com/fwlink/?LinkId=88417) o en la página principal de Microsoft SQL Server Samples and Community Projects en la sección Microsoft SQL Server Product Samples. Haga clic en **Databases**y, a continuación en la pestaña **Releases** y seleccione las bases de datos que desee.  
  
> [!NOTE]  
>  Para consultar los tutoriales, se recomienda agregar los botones **Siguiente** y **Anterior** a la barra de herramientas del visor de documentos.  
  
## <a name="see-also"></a>Vea también  
 [Tutorial de minería de datos básicos](../../2014/tutorials/basic-data-mining-tutorial.md)   
 [Intermedio de Tutorial de minería de datos &#40;Analysis Services: minería de datos&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)  
  
  