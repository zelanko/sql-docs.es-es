---
title: Tarea Consulta de minería de datos| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dataminingquerytask.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6bb3cea630401f92395e2ca4416c03bcd870c881
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433582"
---
# <a name="data-mining-query-task"></a>Data Mining Query Task
  La tarea Consulta de minería de datos ejecuta consultas de predicción basadas en modelos de minería de datos integrados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La consulta de predicción crea una predicción para datos nuevos a partir de modelos de minería de datos. Por ejemplo, una consulta de predicción puede predecir cuántos barcos de vela es probable vender durante los meses de verano, así como generar una lista de clientes que podrían estar interesados en comprar uno.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona tareas que realizan otras operaciones de Business Intelligence, como ejecutar instrucciones del lenguaje de definición de datos (DDL) y procesar objetos de análisis.  
  
 Para obtener más información sobre otras tareas de Business Intelligence, haga clic en uno de los temas siguientes:  
  
-   [Tarea Ejecutar DDL de Analysis Services](analysis-services-execute-ddl-task.md)  
  
-   [Tarea de procesamiento de Analysis Services](analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>Consultas de predicción  
 La consulta es una instrucción de Extensiones de minería de datos (DMX). El lenguaje DMX es una extensión del lenguaje SQL que permite trabajar con modelos de minería de datos. Para más información sobre cómo usar el lenguaje DMX, vea [Referencia de Extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference).  
  
 La tarea puede consultar múltiples modelos de minería de datos generados a partir de la misma estructura de minería de datos. Un modelo de minería de datos se construye mediante uno de los algoritmos de minería de datos proporcionados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La estructura de minería de datos a la que hace referencia la tarea Consulta de minería de datos puede incluir múltiples modelos de minería de datos generados con algoritmos diferentes. Para más información, vea [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/mining-structures-analysis-services-data-mining) y [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining).  
  
 La consulta de predicción ejecutada por la tarea Consulta de minería de datos devuelve como resultado una única fila o un conjunto de datos. Una consulta que devuelve una sola fila se denomina consulta de singleton. Por ejemplo, la consulta que predice cuántos barcos de vela se venderán en los meses de verano produce como resultado un número. Para obtener más información acerca de las consultas de predicción que devuelven una única fila, vea [interfaces de consulta de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-query-tools).  
  
 Los resultados de la consulta se almacenan en tablas. Si ya existe una tabla con el nombre especificado en la tarea Consulta de minería de datos, la tarea puede crear la nueva tabla anexando un número al nombre o sobrescribir el contenido de la tabla existente.  
  
 Si los resultados incluyen anidamientos, se quita información de estructura jerárquica de los resultados antes de guardarlos. La eliminación de información de estructura jerárquica de los resultados convierte un conjunto de resultados anidados en una tabla. Por ejemplo, al quitar información de estructura jerárquica de un resultado anidado con una columna **Customer** y una columna anidada **Product** , se agregan filas a la columna **Customer** para crear una tabla que incluya los datos de productos de cada cliente. Así, por ejemplo, un cliente con tres productos diferentes se convierte en una tabla con tres filas; y cada fila incluirá los datos del cliente y uno de los productos. Si se omite la palabra clave FLATTENED, la tabla solo contendrá la columna **Customer** y una única fila por cliente. Para más información, vea [SELECT &#40;DMX&#41;](/sql/dmx/select-dmx).  
  
## <a name="configuration-of-the-data-mining-query-task"></a>Configuración de la tarea Consulta de minería de datos  
 La tarea Consulta de minería de datos requiere dos conexiones. La primera conexión es un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se conecta a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene la estructura de minería de datos y el modelo de minería de datos. La segunda conexión es un administrador de conexiones OLE DB que se conecta a la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que contiene la tabla en la que escribe la tarea. Para obtener más información, consulte [Analysis Services Connection Manager](../connection-manager/analysis-services-connection-manager.md) y [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en uno de los temas siguientes:  
  
-   [Editor de la tarea Consulta de minería de datos &#40;pestaña Modelo de minería de datos&#41;](../data-mining-query-task-editor-mining-model-tab.md)  
  
-   [Editor de la tarea Consulta de minería de datos &#40;pestaña Consulta&#41;](../data-mining-query-task-editor-query-tab.md)  
  
-   [Editor de la tarea Consulta de minería de datos &#40;pestaña Salida&#41;](../data-mining-query-task-editor-output-tab.md)  
  
> [!NOTE]  
>  El Editor de la tarea Consulta de minería de datos no tiene página Expresiones. Utilice en su lugar la ventana **Propiedades** para tener acceso a las herramientas de creación y administración de expresiones de propiedades para las propiedades de la tarea Consulta de minería de datos.  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>Configuración mediante programación de la tarea Consulta de minería de datos  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en uno de los temas siguientes:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
  
