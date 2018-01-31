---
title: "Tarea Consulta de minería de datos| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataminingquerytask.f1
- sql13.dts.designer.dmquerytask.miningmodel.f1
- sql13.dts.designer.dmquerytask.query.f1
- sql13.dts.designer.dmquerytask.output.f1
helpviewer_keywords:
- prediction queries [Integration Services]
- Data Mining Query task [Integration Services]
ms.assetid: f489348c-2008-4f66-8c2c-c07c3029439a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8ffadcd36d1df013d8e5a9a9aeb3f85d4056c27
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="data-mining-query-task"></a>Data Mining Query Task
  La tarea Consulta de minería de datos ejecuta consultas de predicción basadas en modelos de minería de datos integrados en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La consulta de predicción crea una predicción para datos nuevos a partir de modelos de minería de datos. Por ejemplo, una consulta de predicción puede predecir cuántos barcos de vela es probable vender durante los meses de verano, así como generar una lista de clientes que podrían estar interesados en comprar uno.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona tareas que realizan otras operaciones de Business Intelligence, como ejecutar instrucciones del lenguaje de definición de datos (DDL) y procesar objetos de análisis.  
  
 Para obtener más información sobre otras tareas de Business Intelligence, haga clic en uno de los temas siguientes:  
  
-   [Tarea Ejecutar DDL de Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Tarea Procesamiento de Analysis Services](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
## <a name="prediction-queries"></a>Consultas de predicción  
 La consulta es una instrucción de Extensiones de minería de datos (DMX). El lenguaje DMX es una extensión del lenguaje SQL que permite trabajar con modelos de minería de datos. Para más información sobre cómo usar el lenguaje DMX, vea [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md).  
  
 La tarea puede consultar múltiples modelos de minería de datos generados a partir de la misma estructura de minería de datos. Un modelo de minería de datos se construye mediante uno de los algoritmos de minería de datos proporcionados por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La estructura de minería de datos a la que hace referencia la tarea Consulta de minería de datos puede incluir múltiples modelos de minería de datos generados con algoritmos diferentes. Para más información, vea [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md) y [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
 La consulta de predicción ejecutada por la tarea Consulta de minería de datos devuelve como resultado una única fila o un conjunto de datos. Una consulta que devuelve una sola fila se denomina consulta de singleton. Por ejemplo, la consulta que predice cuántos barcos de vela se venderán en los meses de verano produce como resultado un número. Para más información sobre las consultas de predicción que devuelven una única fila, vea [Herramientas de consulta de minería de datos](../../analysis-services/data-mining/data-mining-query-tools.md).  
  
 Los resultados de la consulta se almacenan en tablas. Si ya existe una tabla con el nombre especificado en la tarea Consulta de minería de datos, la tarea puede crear la nueva tabla anexando un número al nombre o sobrescribir el contenido de la tabla existente.  
  
 Si los resultados incluyen anidamientos, se quita información de estructura jerárquica de los resultados antes de guardarlos. La eliminación de información de estructura jerárquica de los resultados convierte un conjunto de resultados anidados en una tabla. Por ejemplo, al quitar información de estructura jerárquica de un resultado anidado con una columna **Customer** y una columna anidada **Product** , se agregan filas a la columna **Customer** para crear una tabla que incluya los datos de productos de cada cliente. Así, por ejemplo, un cliente con tres productos diferentes se convierte en una tabla con tres filas; y cada fila incluirá los datos del cliente y uno de los productos. Si se omite la palabra clave FLATTENED, la tabla solo contendrá la columna **Customer** y una única fila por cliente. Para más información, vea [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md).  
  
## <a name="configuration-of-the-data-mining-query-task"></a>Configuración de la tarea Consulta de minería de datos  
 La tarea Consulta de minería de datos requiere dos conexiones. La primera conexión es un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se conecta a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene la estructura de minería de datos y el modelo de minería de datos. La segunda conexión es un administrador de conexiones OLE DB que se conecta a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla en la que escribe la tarea. Para obtener más información, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md) y [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
> [!NOTE]  
>  El Editor de la tarea Consulta de minería de datos no tiene página Expresiones. Utilice en su lugar la ventana **Propiedades** para tener acceso a las herramientas de creación y administración de expresiones de propiedades para las propiedades de la tarea Consulta de minería de datos.  
  
 Para obtener más información sobre cómo establecer estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](http://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-data-mining-query-task"></a>Configuración mediante programación de la tarea Consulta de minería de datos  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en uno de los temas siguientes:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.DMQueryTask.DMQueryTask>  
  
## <a name="data-mining-query-task-editor-mining-model-tab"></a>Editor de la tarea Consulta de minería de datos (pestaña Modelo de minería de datos)
  Utilice la pestaña **Modelo de minería de datos** del cuadro de diálogo **Tarea Consulta de minería de datos** para especificar la estructura y el modelo de minería de datos que se van a utilizar.  
  
 Para obtener información sobre cómo implementar la minería de datos en paquetes, vea [Tarea Consulta de minería de datos](../../integration-services/control-flow/data-mining-query-task.md) y [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md).  
  
### <a name="general-options"></a>Opciones generales  
 **Nombre**  
 Escriba un nombre único para la tarea Consulta de minería de datos. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Consulta de minería de datos.  
  
### <a name="mining-model-tab-options"></a>Opciones de la pestaña Modelo de minería de datos  
 **Conexión**  
 Seleccione un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la lista, o bien haga clic en **Nuevo** para crear un administrador de conexiones.  
  
 **Temas relacionados:**  [Administrador de conexiones de Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md)  
  
 **Nueva**  
 Permite crear un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **Temas relacionados:** [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Estructura de minería de datos**  
 Seleccione una estructura de minería de datos de la lista.  
  
 **Modelos de minería de datos**  
 Seleccione un modelo de minería de datos que se haya generado en la estructura de minería de datos seleccionada.  

## <a name="data-mining-query-task-editor-query-tab"></a>Editor de la tarea Consulta de minería de datos (pestaña Consulta)
  Use la pestaña **Consulta** del cuadro de diálogo **Tarea Consulta de minería de datos** para crear consultas de predicción según un modelo de minería de datos. En este cuadro de diálogo también puede enlazar parámetros y conjuntos de resultados con variables.  
  
 Para obtener información sobre cómo implementar la minería de datos en paquetes, vea [Tarea Consulta de minería de datos](../../integration-services/control-flow/data-mining-query-task.md) y [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md).  
  
### <a name="general-options"></a>Opciones generales  
 **Nombre**  
 Escriba un nombre único para la tarea Consulta de minería de datos. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Consulta de minería de datos.  
  
### <a name="build-query-tab-options"></a>Opciones de la pestaña Generar consulta  
 **Consulta de minería de datos**  
 Escriba una consulta de minería de datos.  
  
 **Temas relacionados:** [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../../dmx/data-mining-extensions-dmx-reference.md)  
  
 **Generar nueva consulta**  
 Cree la consulta de minería de datos con una herramienta gráfica.  
  
 **Temas relacionados:** [Data Mining Query](../../integration-services/control-flow/data-mining-query.md)  
  
### <a name="parameter-mapping-tab-options"></a>Opciones de la pestaña Asignación de parámetros  
 **Nombre de parámetro**  
 Opcionalmente, actualice el nombre del parámetro. Para asignar el parámetro a una variable, seleccione una variable de la lista **Nombre de variable** .  
  
 **Nombre de variable**  
 Seleccione una variable de la lista para asignarla al parámetro.  
  
 **Agregar**  
 Agregue un parámetro a la lista.  
  
 **Quitar**  
 Seleccione un parámetro y haga clic en **Quitar**.  
  
### <a name="result-set-tab-options"></a>Opciones de la pestaña Conjunto de resultados  
 **Nombre del resultado**  
 Opcionalmente, actualice el nombre del conjunto de resultados. Para asignar el resultado a una variable, seleccione una variable de la lista **Nombre de variable** .  
  
 Para agregar un resultado, haga clic en **Agregar**y escriba un nombre único para el resultado.  
  
 **Nombre de variable**  
 Seleccione una variable de la lista para asignarla al conjunto de resultados.  
  
 **Tipo de resultado**  
 Indique si desea devolver una fila única o un conjunto de resultados completo.  
  
 **Agregar**  
 Agregue un conjunto de resultados a la lista.  
  
 **Quitar**  
 Seleccione un resultado y haga clic en **Quitar**.  
## <a name="data-mining-query-task-editor-output-tab"></a>Editor de la tarea Consulta de minería de datos (pestaña Salida)
  Use la pestaña **Salida** del cuadro de diálogo **Editor de la tarea Consulta de minería de datos** para especificar el destino de la consulta de predicción.  
  
 Para obtener información sobre cómo implementar minería de datos en paquetes, vea [Tarea Consulta de minería de datos](../../integration-services/control-flow/data-mining-query-task.md) y [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md).  
  
### <a name="general-options"></a>Opciones generales  
 **Nombre**  
 Escriba un nombre único para la tarea Consulta de minería de datos. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea Consulta de minería de datos.  
  
### <a name="output-tab-options"></a>Opciones de la pestaña Salida  
 **Conexión**  
 Seleccione un administrador de conexiones de la lista o haga clic en **Nuevo** para crear uno.  
  
 **Nueva**  
 Cree un administrador de conexiones nuevo. Solo se pueden usar los tipos de administrador de conexiones ADO.NET y OLE DB.  
  
 **Tabla de salida**  
 Especifique la tabla en la que la consulta de predicción escribe los resultados.  
  
 **Quitar y volver a crear la tabla de salida**  
 Indica si la consulta de predicción debe sobrescribir el contenido de la tabla de destino quitando y volviendo a crear la tabla.  
  
