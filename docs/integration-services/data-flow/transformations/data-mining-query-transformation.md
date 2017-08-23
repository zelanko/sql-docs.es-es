---
title: "Transformación consulta de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataminingquerytrans.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 544f0aaf11e83b9ba2fc0ae5150b85e537998c25
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="data-mining-query-transformation"></a>Consulta de minería de datos, transformación
  La transformación Consulta de minería de datos realiza consultas de predicción en modelos de minería de datos. Esta transformación contiene un generador de consultas para crear consultas de Extensiones de minería de datos (DMX). El generador de consultas permite crear instrucciones personalizadas para evaluar los datos de entrada de la transformación en un modelo de minería existente mediante el lenguaje DMX. Para más información, vea [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../../../dmx/data-mining-extensions-dmx-reference.md).  
  
 Una transformación puede ejecutar múltiples consultas de predicción si los modelos se generan a partir de la misma estructura de minería de datos. Para más información, vea [Herramientas de consulta de minería de datos](../../../analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>Configuración de la transformación Consulta de minería de datos  
 La transformación Consulta de minería de datos utiliza un administrador de conexiones de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para conectar con el proyecto de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contiene la estructura de minería y los modelos de minería. Para más información, consulte [Analysis Services Connection Manager](../../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Consulta de minería de datos** , haga clic en uno de los temas siguientes:  
  
-   [Editor de transformación Consulta de minería de datos &#40;pestaña Modelo de minería de datos&#41;](../../../integration-services/data-flow/transformations/data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [Editor de transformación Consulta de minería de datos &#40;pestaña Modelo de minería de datos&#41;](../../../integration-services/data-flow/transformations/data-mining-query-transformation-editor-mining-model-tab.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
