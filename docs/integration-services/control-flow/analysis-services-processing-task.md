---
title: Tarea Procesamiento de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.asprocessingtask.f1
- sql13.dts.designer.asprocessingtask.general.f1
- sql13.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing task
- processing objects [Integration Services]
ms.assetid: e5748836-b4ce-4e17-ab6b-617a336f02f4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92e0656fd3625f2b93a1e097d2f81291056d01cf
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298470"
---
# <a name="analysis-services-processing-task"></a>Procesamiento de Analysis Services, tarea

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] procesa objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como modelos tabulares, cubos, dimensiones y modelos de minería de datos.  
  
 Al procesar modelos tabulares, tenga en cuenta lo siguiente:  
  
-   No puede realizar análisis de impacto en modelos tabulares.  
  
-   Algunas opciones de procesamiento para el modo tabular no están expuestas como, por ejemplo, el proceso de desfragmentación y el proceso de recálculo. Puede llevar a cabo estas funciones mediante la tarea Ejecutar DDL.  
  
-   Las opciones Procesar índice y Procesar actualización no son adecuadas para los modelos tabulares y no deben usarse.  
  
-   Los valores de las operaciones por lotes se omiten para los modelos tabulares.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye diversas tareas que realizan operaciones de Business Intelligence, como la ejecución de instrucciones del lenguaje de definición de datos (DDL) y consultas de predicción de minería de datos. Para obtener más información sobre tareas de Business Intelligence relacionadas, haga clic en uno de los temas siguientes:  
  
-   [Tarea Ejecutar DDL de Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Tarea Consulta de minería de datos](../../integration-services/control-flow/data-mining-query-task.md)  
  
## <a name="object-processing"></a>Procesamiento de objetos  
 Pueden procesarse varios objetos a la vez. Cuando se procesan varios objetos, se definen valores de configuración que se aplicarán al procesamiento de todos los objetos del lote.  
  
 Los objetos de un lote pueden procesarse de manera secuencial o en paralelo. Si el lote no contiene objetos para los que el procesamiento secuencial sea importante, debe considerarse el procesamiento paralelo, ya que puede aumentar la velocidad de procesamiento. Si los objetos del lote se procesan en paralelo, se puede configurar la tarea de forma que determine automáticamente el número de objetos que se procesarán simultáneamente, aunque también se puede especificar manualmente este número. Si los objetos se procesan de forma secuencial, se puede establecer un atributo de transacción en el lote especificando todos los objetos de una transacción o utilizando una transacción independiente para cada objeto del lote.  
  
 Al procesar objetos de análisis, puede que también desee procesar los objetos que dependen de ellos. La tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye la opción de procesar los objetos dependientes, además de los seleccionados.  
  
 Normalmente, las tablas de dimensiones se procesan antes que las tablas de hechos. Puede producirse errores si intenta procesar las tablas de hechos antes que las tablas de dimensiones.  
  
 Esta tarea también permite configurar el control de errores en las claves de dimensión. Por ejemplo, la tarea puede omitir los errores o bien detenerse cuando se alcance un número especificado de errores. La tarea puede usar la configuración de errores predeterminada; también se puede definir una configuración de errores personalizada. En la configuración de errores personalizada, debe especificar el modo en que la tarea controla los errores, así como las condiciones de error. Por ejemplo, puede especificar que la tarea debe detenerse cuando se produzca el cuarto error o indicar cómo deben controlarse los valores **Null** en las claves. La configuración de errores personalizada puede incluir también la ruta de un archivo de registro de errores.  
  
> [!NOTE]  
>  La tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo puede procesar objetos de análisis creados mediante las herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Esta tarea se suele usar en combinación con una tarea de inserción masiva, que carga datos en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o con una tarea Flujo de datos que implementa un flujo de datos que carga datos en una tabla. Por ejemplo, la tarea Flujo de datos puede tener un flujo de datos que extraiga los datos de una base de datos transaccional en línea (OLTP) y los cargue en una tabla de hechos de un almacenamiento de datos, tras lo cual se realiza la llamada a la tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para que procese el cubo generado en el almacenamiento de datos.  
  
 La tarea Procesamiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa un administrador de conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para conectarse a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para más información, consulte [Analysis Services Connection Manager](../../integration-services/connection-manager/analysis-services-connection-manager.md).  
  
## <a name="error-handling"></a>Tratamiento de errores  
  
## <a name="configuration-of-the-analysis-services-processing-task"></a>Configuración de la tarea Procesamiento de Analysis Services  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el tema siguiente:  
  
-   [Página Expresiones](../../integration-services/expressions/expressions-page.md)  
  
 Para obtener más información sobre cómo configurar estas propiedades en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , haga clic en el siguiente tema:  
  
-   [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-analysis-services-processing-task"></a>Configuración mediante programación de la tarea Procesamiento de Analysis Services  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, haga clic en el tema siguiente:  
  
-   <xref:Microsoft.DataTransformationServices.Tasks.DTSProcessingTask.DTSProcessingTask>  
  
## <a name="analysis-services-processing-task-editor-general-page"></a>Editor de la tarea de procesamiento de Analysis Services (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea de procesamiento de Analysis Services** para describir y asignar un nombre a la tarea de procesamiento de Analysis Services.  
  
### <a name="options"></a>Opciones  
 **Nombre**  
 Escriba un nombre único para la tarea de procesamiento de Analysis Services. Este nombre se utiliza como etiqueta en el icono de tarea.  
  
> [!NOTE]  
>  Los nombres de tarea deben ser únicos en un paquete.  
  
 **Descripción**  
 Escriba una descripción de la tarea de procesamiento de Analysis Services.  
  
## <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Editor de la tarea de procesamiento de Analysis Services (página Analysis Services)
  Utilice la página **Analysis Services** del cuadro de diálogo **Editor de la tarea de procesamiento de Analysis Services** para especificar un administrador de conexiones de Analysis Services, seleccionar los objetos analíticos que se deben procesar y establecer opciones de procesamiento y control de errores.  
  
 Al procesar modelos tabulares, tenga en cuenta lo siguiente:  
  
1.  No puede realizar análisis de impacto en modelos tabulares.  
  
2.  Algunas opciones de procesamiento para el modo tabular no están expuestas como, por ejemplo, el proceso de desfragmentación y el proceso de recálculo. Puede llevar a cabo estas funciones mediante la tarea Ejecutar DDL.  
  
3.  Algunas opciones de procesamiento proporcionadas, como índices de proceso, no son adecuadas para los modelos tabulares y no deben utilizarse.  
  
4.  Los valores de las operaciones por lotes se omiten para los modelos tabulares.  
  
### <a name="options"></a>Opciones  
 **administrador de conexiones de Analysis Services**  
 Seleccione un administrador de conexiones de Analysis Services de la lista o haga clic en **Nuevo** para crear uno.  
  
 **Nueva**  
 Cree un administrador de conexiones de Analysis Services nuevo.  
  
 **Temas relacionados:** [Administrador de conexiones de Analysis Services](../../integration-services/connection-manager/analysis-services-connection-manager.md), [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones de Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Lista de objetos**  
 |Propiedad|Descripción|  
|--------------|-----------------|  
|**Nombre de objeto**|Enumera los nombres de los objetos especificados.|  
|**Tipo**|Enumera los tipos de los objetos especificados.|  
|**Opciones de proceso**|Seleccione una opción de procesamiento de la lista.<br /><br /> **Temas relacionados**: [Procesar un modelo multidimensional &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services)|  
|**Configuración**|Enumera los valores de configuración de procesamiento para los objetos especificados.|  
  
 **Agregar**  
 Agregue un objeto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a la lista.  
  
 **Quitar**  
 Seleccione un objeto y haga clic en **Eliminar**.  
  
 **Análisis de impacto**  
 Lleve a cabo el análisis de impacto en el objeto seleccionado.  
  
 **Temas relacionados:** [Impacto del cuadro de diálogo de análisis &#40;Analysis Services: datos multidimensionales&#41;](https://msdn.microsoft.com/library/208268eb-4e14-44db-9c64-6f74b776adb6)  
  
 **Resumen de configuración de lotes**  
 |Propiedad|Descripción|  
|--------------|-----------------|  
|**Orden de procesamiento**|Especifica si los objetos se procesan de manera secuencial o en un lote; si se utiliza el procesamiento paralelo, especifica el número de objetos que se deben procesar simultáneamente.|  
|**Modo de transacción**|Especifica el modo de transacción para el procesamiento secuencial.|  
|**Errores de dimensión**|Especifica el comportamiento de la tarea cuando se produce un error.|  
|**Ruta del registro de errores de claves de dimensiones**|Especifica la ruta de acceso del archivo en el que se registran los errores.|  
|**Procesar objetos afectados**|Indica si los objetos afectados o dependientes también se deben procesar.|  
  
 **Cambiar configuración**  
 Cambie las opciones de procesamiento y el control de errores en las claves de dimensiones.  
  
 **Temas relacionados:** [Cuadro de diálogo Cambiar configuración &#40;(Analysis Services: datos multidimensionales)&#41;](https://msdn.microsoft.com/library/0041e042-d7ce-48f9-a690-a6dc65471ff3)  
  
