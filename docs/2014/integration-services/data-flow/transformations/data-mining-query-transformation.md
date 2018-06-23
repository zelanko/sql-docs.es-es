---
title: Transformación Consulta de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.dataminingquerytrans.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8fbe99a681e2d91e61119adea5f7c48ef00fc8d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198476"
---
# <a name="data-mining-query-transformation"></a>Consulta de minería de datos, transformación
  La transformación Consulta de minería de datos realiza consultas de predicción en modelos de minería de datos. Esta transformación contiene un generador de consultas para crear consultas de Extensiones de minería de datos (DMX). El generador de consultas permite crear instrucciones personalizadas para evaluar los datos de entrada de la transformación en un modelo de minería existente mediante el lenguaje DMX. Para más información, vea [Referencia de Extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
 Una transformación puede ejecutar múltiples consultas de predicción si los modelos se generan a partir de la misma estructura de minería de datos. Para obtener más información, consulte [Interfaces de consultas de minería de datos](../../../analysis-services/data-mining/data-mining-query-tools.md).  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>Configuración de la transformación Consulta de minería de datos  
 La transformación Consulta de minería de datos utiliza un administrador de conexiones de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para conectar con el proyecto de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contiene la estructura de minería y los modelos de minería. Para más información, consulte [Analysis Services Connection Manager](../../connection-manager/analysis-services-connection-manager.md).  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Consulta de minería de datos** , haga clic en uno de los temas siguientes:  
  
-   [Editor de transformación de consulta de minería de datos &#40;pestaña modelo de minería de datos&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
-   [Editor de transformación de consulta de minería de datos &#40;pestaña modelo de minería de datos&#41;](../../data-mining-query-transformation-editor-mining-model-tab.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
  
