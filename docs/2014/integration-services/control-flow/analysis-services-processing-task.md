---
title: Tarea Procesamiento de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 02023482a2f3537872b50ac70f8bfd68d2128e1b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379133"
---
# <a name="analysis-services-processing-task"></a>Procesamiento de Analysis Services, tarea
  La tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] procesa objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como modelos tabulares, cubos, dimensiones y modelos de minería de datos.  
  
 Al procesar modelos tabulares, tenga en cuenta lo siguiente:  
  
-   No puede realizar análisis de impacto en modelos tabulares.  
  
-   Algunas opciones de procesamiento para el modo tabular no están expuestas como, por ejemplo, el proceso de desfragmentación y el proceso de recálculo. Puede llevar a cabo estas funciones mediante la tarea Ejecutar DDL.  
  
-   Las opciones Procesar índice y Procesar actualización no son adecuadas para los modelos tabulares y no deben usarse.  
  
-   Los valores de las operaciones por lotes se omiten para los modelos tabulares.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye diversas tareas que realizan operaciones de Business Intelligence, como la ejecución de instrucciones del lenguaje de definición de datos (DDL) y consultas de predicción de minería de datos. Para obtener más información sobre tareas de Business Intelligence relacionadas, haga clic en uno de los temas siguientes:  
  
-   [Tarea Ejecutar DDL de Analysis Services](analysis-services-execute-ddl-task.md)  
  
-   [Tarea Consulta de minería de datos](data-mining-query-task.md)  
  
## <a name="object-processing"></a>Procesamiento de objetos  
 Pueden procesarse varios objetos a la vez. Cuando se procesan varios objetos, se definen valores de configuración que se aplicarán al procesamiento de todos los objetos del lote.  
  
 Los objetos de un lote pueden procesarse de manera secuencial o en paralelo. Si el lote no contiene objetos para los que el procesamiento secuencial sea importante, debe considerarse el procesamiento paralelo, ya que puede aumentar la velocidad de procesamiento. Si los objetos del lote se procesan en paralelo, se puede configurar la tarea de forma que determine automáticamente el número de objetos que se procesarán simultáneamente, aunque también se puede especificar manualmente este número. Si los objetos se procesan de forma secuencial, se puede establecer un atributo de transacción en el lote especificando todos los objetos de una transacción o utilizando una transacción independiente para cada objeto del lote.  
  
 Al procesar objetos de análisis, puede que también desee procesar los objetos que dependen de ellos. La tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye la opción de procesar los objetos dependientes, además de los seleccionados.  
  
 Normalmente, las tablas de dimensiones se procesan antes que las tablas de hechos. Puede producirse errores si intenta procesar las tablas de hechos antes que las tablas de dimensiones.  
  
 Esta tarea también permite configurar el control de errores en las claves de dimensión. Por ejemplo, la tarea puede omitir los errores o bien detenerse cuando se alcance un número especificado de errores. La tarea puede usar la configuración de errores predeterminada; también se puede definir una configuración de errores personalizada. En la configuración de errores personalizada, debe especificar el modo en que la tarea controla los errores, así como las condiciones de error. Por ejemplo, puede especificar que la tarea debe detenerse cuando se produzca el cuarto error o indicar cómo deben controlarse los valores **Null** en las claves. La configuración de errores personalizada puede incluir también la ruta de un archivo de registro de errores.  
  
> [!NOTE]  
>  La tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo puede procesar objetos de análisis creados mediante las herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Esta tarea se suele usar en combinación con una tarea de inserción masiva, que carga datos en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o con una tarea Flujo de datos que implementa un flujo de datos que carga datos en una tabla. Por ejemplo, la tarea Flujo de datos puede tener un flujo de datos que extraiga los datos de una base de datos transaccional en línea (OLTP) y los cargue en una tabla de hechos de un almacenamiento de datos, tras lo cual se realiza la llamada a la tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para que procese el cubo generado en el almacenamiento de datos.  
  
 La tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para conectarse a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para más información, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md).  
  
## <a name="error-handling"></a>Tratamiento de errores  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Configuración de la tarea Procesamiento de Analysis Services  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea de procesamiento de Analysis Services &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor de la tarea de procesamiento de Analysis Services &#40;página Analysis Services&#41;](../analysis-services-processing-task-editor-analysis-services-page.md)  
  
-   [Página Expresiones](../expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo configurar estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Configuración mediante programación de la tarea Procesamiento de Analysis Services  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en uno de los temas siguientes:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
  
