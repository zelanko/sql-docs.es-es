---
title: Transformación Consulta de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytrans.f1
- sql13.dts.designer.dmquerytransformation.miningmodel.f1
- sql13.dts.designer.dmquerytransformation.query.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e3b6783969376b20921d960e79c8909b5fda4aa
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71291465"
---
# <a name="data-mining-query-transformation"></a>Consulta de minería de datos, transformación

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La transformación Consulta de minería de datos realiza consultas de predicción en modelos de minería de datos. Esta transformación contiene un generador de consultas para crear consultas de Extensiones de minería de datos (DMX). El generador de consultas permite crear instrucciones personalizadas para evaluar los datos de entrada de la transformación en un modelo de minería existente mediante el lenguaje DMX. Para más información, vea [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../../../dmx/data-mining-extensions-dmx-reference.md).  
  
 Una transformación puede ejecutar múltiples consultas de predicción si los modelos se generan a partir de la misma estructura de minería de datos. Para más información, vea [Herramientas de consulta de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools).  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>Configuración de la transformación Consulta de minería de datos  
 La transformación Consulta de minería de datos utiliza un administrador de conexiones de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] para conectar con el proyecto de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que contiene la estructura de minería y los modelos de minería. Para más información, consulte [Analysis Services Connection Manager](../../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="data-mining-query-transformation-editor-mining-model-tab"></a>Editor de transformación Consulta de minería de datos (pestaña Modelo de minería de datos)
  Use la pestaña **Modelo de minería de datos** del cuadro de diálogo **Editor de transformación Consulta de minería de datos** para seleccionar la estructura y los modelos de minería de datos.  
  
### <a name="options"></a>Opciones  
 **Connection**  
 Seleccione una conexión de Analysis Services existente mediante el cuadro de lista o cree una nueva conexión con el botón **Nuevo** que se describe a continuación.  
  
 **Nuevo**  
 Permite crear una conexión con el cuadro de diálogo **Agregar administrador de conexiones de Analysis Services** .  
  
 **Estructura de minería de datos**  
 Seleccione una opción de la lista de estructuras del modelo de minería de datos.  
  
 **Modelos de minería de datos**  
 Muestra la lista de modelos de minería de datos asociados con la estructura de minería de datos seleccionada.  
  
## <a name="data-mining-query-transformation-editor-query-tab"></a>Editor de transformación Consulta de minería de datos (pestaña Consulta)
  Utilice la pestaña **Consulta** del cuadro de diálogo **Editor de transformación Consulta de minería de datos** para crear una consulta de predicción.  
  
### <a name="options"></a>Opciones  
 **Consulta de minería de datos**  
 Escriba una consulta DMS (Extensiones de minería de datos) directamente en el cuadro de texto.  
  
 **Generar nueva consulta**  
 Haga clic en **Generar nueva consulta** para crear una consulta DMS (Extensiones de minería de datos) mediante el generador de consultas gráfico.  
  
