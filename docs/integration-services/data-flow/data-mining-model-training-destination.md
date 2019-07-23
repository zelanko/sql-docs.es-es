---
title: Destino de Entrenamiento del modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingmodeltrainingdest.f1
- sql13.dts.designer.dmmtrainingtransformation.connection.f1
- sql13.dts.designer.dmmtrainingtransformation.columns.f1
helpviewer_keywords:
- destinations [Integration Services], Data Mining Model Training
- Data Mining Model Training destination
- mining models [Analysis Services], training
- training mining models
ms.assetid: 6bc8cbe2-46af-4f7b-93d6-86779313c9d7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6a148af7be04bba6bdf5c16ca7e85e94f1a0de31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68049442"
---
# <a name="data-mining-model-training-destination"></a>entrenamiento del modelo de minería de datos, destino

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El destino de Entrenamiento del modelo de minería de datos entrena los modelos de minería de datos pasando los datos que recibe el destino por los algoritmos de modelos de minería de datos. Un destino puede entrenar varios modelos de minería de datos si los modelos se generan sobre la misma estructura de minería de datos. Para obtener más información, consulte [Mining Structure Columns](../../analysis-services/data-mining/mining-structure-columns.md) y [Mining Model Columns](../../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="configuration-of-the-data-mining-model-training-destination"></a>Configuración del destino de entrenamiento del modelo de minería de datos  
 Si una columna de nivel de caso de la estructura de destino y los modelos generados en la estructura tiene el tipo de contenido KEY TIME o KEY SEQUENCE, los datos de entrada se deben ordenar en esa columna. Por ejemplo, los modelos generados con el algoritmo de serie temporal de Microsoft usan el tipo de contenido KEY TIME. Si no se ordenan los datos de entrada, el procesamiento del modelo puede producir un error. Si los datos requieren que se ordenen, puede usar la transformación Ordenar en una etapa anterior del flujo de datos para ordenar los datos. Este requisito no se aplica a las columnas con el tipo de contenido KEY. Para obtener más información, vea [Tipos de contenido &#40;minería de datos&#41;](../../analysis-services/data-mining/content-types-data-mining.md) y [Transformación Ordenar](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
> [!NOTE]  
>  La entrada del destino de Entrenamiento del modelo de minería de datos se debe ordenar. Para ordenar los datos, puede incluir un destino de Ordenar en dirección ascendente desde el destino de Entrenamiento del modelo de minería de datos en el flujo de datos. Para más información, consulte [Sort Transformation](../../integration-services/data-flow/transformations/sort-transformation.md).  
  
 Este destino tiene una entrada y ninguna salida.  
  
 El destino de Entrenamiento del modelo de minería de datos usa un administrador de conexiones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para conectarse al proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene la estructura y los modelos de minería de datos que entrena el destino. Para más información, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas del destino de entrenamiento del modelo de minería de datos](../../integration-services/data-flow/data-mining-model-training-destination-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="data-mining-model-training-editor-connection-tab"></a>Editor de entrenamiento de modelos de minería de datos (pestaña Conexión)
  Utilice la página **Conexión** del cuadro de diálogo **Editor de entrenamiento de modelos de minería de datos** para seleccionar un modelo de minería de datos para entrenar.  
  
### <a name="options"></a>Opciones  
 **Administrador de conexiones**  
 Seleccione una conexión de la lista de conexiones existentes de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o bien cree una conexión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con el botón **Nueva** que se describe más adelante.  
  
 **Nueva**  
 Permite crear una conexión con el cuadro de diálogo **Agregar administrador de conexiones de Analysis Services** .  
  
 **Estructura de minería de datos**  
 Seleccione una estructura de la lista de estructuras de minería de datos disponibles, o bien haga clic en **Nuevo**para crear una estructura.  
  
 **Nueva**  
 Permite crear una estructura de minería de datos y un modelo de minería de datos con el **Asistente para minería de datos**.  
  
 **Modelos de minería de datos**  
 Vea la lista de modelos de minería de datos asociados a la estructura de minería de datos seleccionada.  
  
## <a name="data-mining-model-training-editor-columns-tab"></a>Editor de entrenamiento de modelos de minería de datos (pestaña Columnas)
  Utilice la página **Columnas** del cuadro de diálogo **Editor de entrenamiento de modelos de minería de datos** para asignar columnas de entrada a las columnas de la estructura de minería de datos.  
  
## <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Muestra la lista de columnas de entrada disponibles. Arrastre las columnas de entrada para asignarlas a las columnas de la estructura de minería de datos.  
  
 **Columnas de la estructura de minería de datos**  
 Muestra la lista de columnas de la estructura de minería de datos. Arrastre las columnas de la estructura de minería de datos para asignarlas a las columnas de entrada disponibles.  
  
 **Columna de entrada**  
 Muestra las columnas de entrada seleccionadas de la tabla anterior. Para cambiar o quitar una selección de asignación, utilice la lista de **Columnas de entrada disponibles**.  
  
 **Columnas de la estructura de minería de datos**  
 Muestra las columnas de destino disponibles, independientemente de si están asignadas o no.  
  
